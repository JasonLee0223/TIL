# UIView

> 화면의 사각형 영역에 대한 내용을 관리하는 개체입니다.

## Overview
View는 앱 사용자 인터페이스의 기본 빌딩 블록이며 UIView 클래스는 모든 View에 공통적인 동작을 정의합니다.   
View 개체는 경계 사각형 내에서 Contents를 렌더링하고 해당 Contents와의 모든 상호 작용을 처리합니다.     
UIView 클래스는 인스턴스화하고 고정된 배경색을 표시하는 데 사용할 수 있는 구체적인 클래스입니다.    
더 정교한 Contents를 그리기 위해 서브 클래싱할 수도 있습니다.   
앱에서 흔히 볼 수 있는 Label, Image, Button 및 기타 인터페이스 요소를 표시하려면 직접 정의하려고 시도하기보다는   
UIKit Framework가 제공하는 View 하위 클래스를 사용하도록 합니다.    

View 개체는 응용 프로그램이 사용자와 상호 작용하는 주요 방법이므로 많은 책임이 있습니다.    
아래는 몇 가지 예시입니다.

- Drawing and animation
  - View는 UIKit 또는 Core Graphics를 사용하여 사각형 영역에 Contents를 그립니다.
  - 일부 View 속성을 새 값으로 애니메이션화 할 수 있습니다.
- Layout and subview management
  - View에는 0개 이상의 하위 View가 포함될 수 있습니다.
  - View는 하위 View의 크기와 위치를 조정할 수 있습니다.
  - Auto Layout을 사용하여 View 계층 구조의 변경에 따라 View 크기를 조정하고 위치를 변경하는 규칙을 정의합니다.
- Event Handling
  - View는 UIResponder의 하위 클래스이며 Touch 및 기타 유형의 이벤트에 응답할 수 있습니다.
  - View는 일반적인 제스처를 처리하기 위해 Gesture Recognizer를 설치할 수 있습니다.

View는 다른 View 내부에 중첩되어 View 계층 구조를 생성할 수 있으며, 이는 관련 콘텐츠를 구성하는 편리한 방법을 제공합니다.   
View를 중첩하면 중첩된 하위 View와 상위 View(Superview) 간에 부모-자식 관계가 생성됩니다.   
상위 View에는 여러 개의 하위 View가 포함될 수 있지만 각 하위 View에는 하나의 Superview만 있습니다.  
기본적으로 하위 View의 가시 영역이 상위 View의 범위를 벗어나 확장되면 하위 View의 Contents의 클리핑이 발생하지 않습니다.    
그 동작을 변경하려면 clipsToBounds 속성을 사용합니다.   

Frame 및 bounds 속성은 각 View의 Geometry을 정의합니다.     
Frame 속성은 superview의 좌표계에서 View의 원점과 치수를 정의합니다.    
bounds 속성은 View의 내부 치수를 정의하며 사용자 정의 drawing code에서만 거의 독점적으로 사용됩니다.    
center 속성은 frame과 bounds 속성을 직접 변경하지 않고 View 위치를 변경하는 편리한 방법을 제공합니다.   

UIView 클래스 사용 방법에 대한 자세한 내용은 [View Programming Guide for iOS](https://developer.apple.com/library/archive/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009503)를 참고합니다.

---

## Draw views
View drawing는 필요에 따라 발생합니다.      
View가 처음 표시되거나 Layout 변경으로 인해 전체 또는 일부가 표시될 때 시스템은 View에 Contents를 그리도록 요청합니다.  
UIKit 또는 Core Graphics를 사용하는 custom Content를 포함하는 View의 경우 시스템은 View의 `draw(_:)` 메서드를 호출합니다.       
이 메서드의 구현은 이 메서드를 호출하기 전에 시스템에서 자동으로 설정한 현재 graphics content에 View의 contents를 그리는 일을 담당합니다.   
이렇게 하면 화면에 표시될 수 있는 View Contents의 정적인 시각적 표현이 생성됩니다.  

View의 실제 내용이 변경되면 View를 다시 그려야 함을 시스템에 알리는 것은 사용자의 책임입니다.   
View의 `setNeedsDisplay()` 또는 `setNeedDisplay(_:)` 메서드를 호출하여 이를 수행합니다.     
이러한 메서드를 통해 시스템은 다음 Drawing cycle동안 View를 업데이트해야 함을 알 수 있습니다.   
View를 업데이트하기 위해 다음 Drawing Cycle까지 기다리기 때문에 여러 View에서 이러한 메서드를 호출하여 동시에 업데이트할 수 있습니다.   
> Note  
> OpenGL ES를 사용하여 drawing을 그리는 경우 UIView를 서브클래싱하는 대신 GLKView 클래스를 사용해야 합니다.     
> OpenGL ES를 사용하여 그리는 방법에 대한 자세한 내용은 [OpenGL ES Programming Guide](https://developer.apple.com/library/archive/documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008793)를 참고합니다.

View drawing cycle 및 이 cycle에서 View의 역할에 대한 자세한 내용은 [View Programming Guide for iOS](https://developer.apple.com/library/archive/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009503)를 참조합니다.