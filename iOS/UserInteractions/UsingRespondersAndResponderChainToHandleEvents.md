# Using responders and responder chain To handle events

## Overview

앱은 응답자 객체(Responder objects)를 사용하여 이벤트를 수신하고 처리한다.  
응답자 객체는 UIResponder 클래스의 인스턴스이며 일반적인 하위 클래스에는 UIView, UIViewController 및 UIApplication이 포함된다.  
응답자는 raw 이벤트 데이터를 수신하고 이벤트를 처리하거나 다른 응답자 객체로 전달해야한다.     
앱이 이벤트를 수신하면 UIKit은 해당 이벤트를 첫 번째 응답자로 알려진 가장 적절한 응답자 객체로 자동으로 보낸다.     
처리되지 않은(Unhandled) 이벤트는 활성(active) 응답자 체인의 응답자에서 응답자로 전달되며 이는 앱 응답자 개체의 동적 구성이다.

<img src = "https://user-images.githubusercontent.com/92699723/222882685-0b1643f8-4bf3-49a9-a582-ba38ea17284d.png" width=500>

위 그림에서 텍스트 필드가 이벤트 처리되지 않는 경우 UIKit은 이벤트를 텍스트 필드의 부모 UIView 객체로 보낸 다음 window의 rootView로 보낸다.     
root view에서 응답자 체인은 이벤트를 window로 보내기전에 소유한 뷰컨트롤러로 전환합니다.    
window가 이벤트를 처리할 수 없는 경우 UIKit은 이벤트를 UIApplication 객체로 전달하고 해당 객체가 UIResponder의 인스턴스이고 아직 응답자 체인의 일부가 아닌 경우 app delegate에게 전달할 수 있다.    

## Determine an event’s first responder (이벤트 첫번째 응답자 결정)
UIKit은 해당 이벤트 유형에 따라 이벤트에 대한 첫 번째 응답자로 개체를 지정합니다.   
아래의 표를 참고합니다.

| Event type | First Responder |
| --- | --- |
| Touch events | The view in which the touch occurred. |
| Press events | The object that has focus. |
| Shake-motion events | The object that you (or UIKit) designate(지정하다) |
| Remote-control events | The object that you (or UIKit) designate(지정하다) |
| Editing menu message | The object that you (or UIKit) designate(지정하다) |

> 💡 가속도계, 자이로스코프 및 자력계와 관련된 모션 이벤트는 응답자 체인을 따르지 않습니다.     
> 대신 **Core Motion**은 이러한 이벤트를 지정된 객체에 직접 전달합니다.     
> 자세한 내용은 Core Motion Framework를 참조합니다.     

컨트롤은 작업 메시지를 사용하여 연결된 대상 개체와 직접 통신합니다.     
사용자가 컨트롤과 상호 작용할 때 컨트롤은 대상 객체에 작업 메시지를 보냅니다.   
액션(Action) 메시지는 이벤트가 아니지만 여전히 응답자 체인을 활용할 수 있습니다.    

**컨트롤의 대상 객체가 nil이면 UIKit은 대상 객체에서 시작하여 적절한 작업 메서드를 구현하는 객체를 찾을 때까지 응답자 체인을 순회합니다.**      

> 예를 들어, UIKit 편집 메뉴는 cut(_ :), copy(_ :) 또는 paste(_ :)와 같은 이름을 가진 메서드를 구현하는
응답자 객체를 검색합니다.

제스쳐(Gesture) 인식기는 View보다 먼저 터치 및 누리기 이벤트를 수신합니다.      
View의 제스처 인식기가 일련의 터치를 인식하지 못하면 UIKit이 터치를 View로 보냅니다.    
View가 터치를 처리하지 않으면 UIKit은 응답자 체인 상위로 터치를 전달합니다.     
제스처 인식기를 사용하여 이벤트를 처리하는 방법에 대해서는 Handling UIKit gestures를 참고합니다.

## Determine which responder contained a touch event
UIKit은 View 기반 적중(hit)테스트를 사용하여 터치 이벤트가 발생하는 위치를 결정합니다.      
특히 UIKit은 터치 위치를 View 계층 구조의 View 객체 경계와 비교합니다.      
UIView의 `hitTest(_ : with: )`메서드는 View 계층을 순회하여 터치 이벤트에 대한 첫 번째 응답자가 되는 지정된 터치를 포함하여 가장 깊은 View를 찾습니다.      

> 💡 터치 위치가 View의 범위 밖에 있는 경우 hitTest(_: with:) 메서드는 해당 View와 모든 하위 View를 무시합니다.     
> 결과적으로 View의 clipToBounds 속성이 true이면 해당 View의 경계 외부에 있는 하위 View는 터치를 포함하더라도 반환되지 않습니다.    
> 자세한 설명은 UIView의 hitTest(_ : with: ) 메서드를 참조하세요.


> 터치가 발생하면 UIKit은 UITouch 객체를 생성하고 View와 연결합니다.    
> 터치 위치 또는 기타 매개변수가 변경되면 UIKit은 동일한 UITouch 객체를 새로운 정보로 업데이트합니다.   
> 터치가 끝나면 UIKit은 UITouch 객체를 해제합니다.

## Alter the responder chain (응답자 체인 대체)
[next](https://developer.apple.com/documentation/uikit/uiresponder/1621099-next) 응답자 개체의 속성을 재정의하여 응답자 체인을 변경할 수 있습니다 . 이렇게 하면 다음 응답자는 반환하는 개체입니다.

많은 UIKit 클래스가 이미 이 속성을 재정의하고 다음을 포함한 특정 개체를 반환합니다.
- [UIView](https://developer.apple.com/documentation/uikit/uiview)사물. 보기가 보기 컨트롤러의 루트 보기인 경우 다음 응답자는 보기 컨트롤러입니다. 그렇지 않으면 다음 응답자는 뷰의 슈퍼뷰입니다.
- [UIViewController](https://developer.apple.com/documentation/uikit/uiviewcontroller)사물.
    - 보기 컨트롤러의 보기가 창의 루트 보기인 경우 다음 응답자는 창 개체입니다.
    - 뷰 컨트롤러가 다른 뷰 컨트롤러에 의해 제시된 경우 다음 응답자는 제시하는 뷰 컨트롤러입니다.
- [UIWindow](https://developer.apple.com/documentation/uikit/uiwindow)사물. 창의 다음 응답자는 [UIApplication](https://developer.apple.com/documentation/uikit/uiapplication)개체입니다.    
- [UIApplication](https://developer.apple.com/documentation/uikit/uiapplication)물체.  
- [UIResponder](https://developer.apple.com/documentation/uikit/uiresponder)다음 응답자는 앱 델리게이트이지만 앱 델리게이트 가 뷰, 뷰 컨트롤러 또는 앱 객체 자체가 아닌 인스턴스인 경우에만 가능합니다 .

### 🌐 Reference Site
[Using responders and responder chain To handle events | Apple Documents](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/using_responders_and_the_responder_chain_to_handle_events)