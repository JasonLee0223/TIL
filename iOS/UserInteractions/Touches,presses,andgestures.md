# Touches, presses, and gestures

앱 전체에서 해당 코드를 재사용할 수 있도록 제스처 인식기에 앱의 이벤트 처리 논리를 캡슐화합니다.

## OverView

표준 UIKit View 및 Control을 사용하여 앱을 빌드하는 경우 UIKit은 터치 이벤트(멀티 터치 이벤트 포함)를 
자동으로 처리합니다.

그러나 사용자 지정 view를 사용하여 컨텐츠를 표시하는 경우 view에서 발생하는 모든 터치 이벤트를 처리해야합니다.

터치 이벤트를 직접 처리하는 방법에는 두 가지가 있습니다.

- 제스처 인식기를 사용하여 터치를 추적합니다. [UIKit 제스처 처리를](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/handling_uikit_gestures)(Handling UIKit gestures) 참조하십시오 .
- 하위 클래스 에서 직접 터치를 추적합니다 [UIView](https://developer.apple.com/documentation/uikit/uiview). [보기에서 터치 처리를](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/handling_touches_in_your_view)(Handling touches in your view) 참조하십시오.

### 🌐 Reference Site
[Touches, presses, and gestures | Apple Documents](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures)