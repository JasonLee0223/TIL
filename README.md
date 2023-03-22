# TIL
매일매일 학습하여 커밋을 남겨보자!

## Git
|Subject|Link|Explain|
|:--|:--|:--|
|Git Commit|[Commit message style](Git/Commit%20message%20style.md)|

## API Design Guidelines
### 🪧 Agenda
|Section|Subject|Explain|   
|:--|:--|:--|   
|📕 Fundamentals|[Fundamentals](APIDesignGuideline/Fundamentals.md)|핵심개념|
|📗 Naming|[Promote Clear Usage](APIDesignGuideline/Promote%20Clear%20Usage.md)|명확하게 사용하기|
||[Strive for Fluent Usage](APIDesignGuideline/Strive%20for%20Fluent%20Usage.md)|자연스러운 사용을 위해 노력하기|
||[Use Terminology Well](APIDesignGuideline/Use%20Terminology%20Well.md)|적절한 기술 용어 사용하기|
|📘 Conventions|[General Conventions](APIDesignGuideline/GeneralConventions.md)|일반 규칙|
||[Parameters](APIDesignGuideline/Parameters.md)|매개변수|
||[Argument Labels](APIDesignGuideline/ArgumentLabels.md)|전달인자 레이블|
|📙 Special Instructions|[Special Instructions](APIDesignGuideline/SpecialInstructions.md)|특별 지침들|
|📖 Article|[✏️ Bool 변수 이름 제대로 짓기 위한 최소한의 영문법](Naming/BoolNaming.md)|
|🎬 Video|[✏️ 영어 변수명을 잘 지어보자](Naming/영어변수명을잘지어보자.md)|

# 🗂️ iOS
## 📗 UIKit
|Section|Title|Subject Link|Explain|
|:--|:--|:--|:--|   
|App and environment||[UIKit 설명, App and Environment](iOS/About%20App%20Development%20with%20UIKit.md)|
|App Structure|Managing your app's life cycle|[ViewController Life-Cycle](iOS/ViewController%20Life-Cycle.md)|

## 📕 User Interface
|Section|Title|Subject Link|Explain|
|:--|:--|:--|:--|   
|Views and controls|View fundamentals|UIView|
||Configuring the bounds and frame rectangles|[var frame vs var bounds](iOS/Frame%20vs%20Bounds.md)|
|||var bounds|Same as above|
||Container Views|CollectionViews|
|||TableViews|
|||[UIStackView](iOS/UIStackView.md)|
|||UIScrollView|
||Content Views|[UIImageView](https://github.com/JasonLee0223/TIL/blob/main/iOS/UIImageVIew.md)|
||Controls|[UIButton](iOS/UIButton.md)|
|||[UIButton.Configuration](iOS/UIButton.Configuration.md)|
|||[UISlider](iOS/UISlider.md)|
|||[UIStepper](iOS/UIStepper.md)|
||Text Views|[UILabel](iOS/UILabel.md)|
||Search Field|
||Bars|
||Content Viewer|
||Private Click Measurement (PCM)|
||SwiftUI|
|View controllers|
|View layout|
|Animation and haptics|
|Windows and screens|Windows|
||Scenes|
||Popovers|
||Alerts|
||Screens|[UIScreen](iOS/UIScreen.md)|

## 📕 User interactions
|Section|Title|Subject Link|Explain|
|:--|:--|:--|:--|   
|[Touches, presses, and gestures](iOS/UserInteractions/Touches,presses,andgestures.md)|[Using responders and respoder chain to handle events](iOS/UserInteractions/UsingRespondersAndResponderChainToHandleEvents.md)|
|||UIResponder|
|||UIEvent|
|||UITouch|
|||UIPress|
||Standard gestures|[Handling UIKit gestures](iOS/UserInteractions/HandlingUIKitGestures.md)|
|||UILongPressGestureRecognizer|
|||UIPanGestureRecognizer|
|||UIPinchGestureRecognizer|
|||UIScreenEdgePanGestureRecognzier|
|||UISwipeGestureRecognizer|
|||[UITapGestureRecognizer](iOS/UITapGestureRecognizer.md)|
||Custom gestures||
|||UIGestureRecognizer|
|||UIGestureRecognizerDelegate|
||Menus and shortcus|
|||[UIAction](iOS/UIAction.md)|
||Drags and drop|
||Pointer interactions|
||Focus-based navigation|
|Menus and shortcuts|
|Drag and drop|
|Pointer interactions|
|Pencil interactions|
|Focus-based navigation|
|Accessibility for UIKit|

# 🗂️ Core Graphics
|Section|Title|Subject Link|Explain|
|:--|:--|:--|:--|   
|Geometric Data Types||[CGPoint, CGSize, CGRect](iOS/CGPoint,CGSize,CGRect.md)|
|||CGSize|Same as above|
|||CGRect|Same as above|
|2D Drawing|
|Colors and Fonts|
|||CGColor|
|||CGFont|

# ETC
|Section|Title|Subject Link|Explain|
|:--|:--|:--|:--|   
|||[File System Basics](iOS/FileSystem.md)|
|||[Sandbox 정책과 Files 앱](iOS/SandBox.md)|
|Logs|Essentials|
||Log Messages|[Logger & OS_Log](iOS/Logger%20&%20OS_Log.md)|
|||
|||[VC간의 데이터 전송방법](iOS/Data%20Transfer%20Process.md)|
|||[Delegate](iOS/Delegate.md)|
|||[magnitude & abs()](iOS/magnitude.md)|절대값 구하기|
|||[pow() & sqrt()](iOS/pow.md)|제곱, 제곱근 구하기|
|Storyboard|
|||[3 ways to change the screen](iOS/StoryBoard/3%20ways%20to%20change%20the%20screen.md)|

# 🗂️ Swift
|Section|Title|Subject Link|Explain|
|:--|:--|:--|:--|   
|01|데이터 타입 고급|[typealias](Swift/typealias.md)|
|||[Tuple](Swift/Tuple.md)|
||Collection Types|Array|
|||[Dictionary](Swift/Dictionary.md)|
|||Set|
|||[Enumerations](Swift/Enum.md)|
|||Operator|
|||Control Flow|
|||Functions|
|||Optional|
|02|Object Oriented Programming with Swift|[🔥 Struct & Class](Swift/Struct%20vs%20Class.md)|
|||[🔥Choosing Between Structures and Class](Swift/ChoosingBetweenStructureAndClass.md)|
|||Property & Method|
|||Initialization|
|||Access Control|
|03|functional programming with Swift|[🔥 Closure](Swift/Closure.md)|
|||Optional Chaining|
|||Early-exit|
|||[Higher-order function](Swift/Higher-order%20function.md)|
|||Monad|
|04|Extension|[Subscript](Swift/Subscript.md)|
|||[🔥 Inheritance](Swift/Inheritance.md)|
|||Type Casting|
|||[🔥 Protocol](Swift/Protocol.md)|
|||Extension|
|||[🔥 Generic](Swift/Generic.md)|
|||[🔥 Protocol Default Implimentations](Swift/ProtocolDafaultImplimentation.md)|
|05|Swift High|Nested Type|
|||[Pattern](Swift/Pattern.md)|
|||[Where](Swift/Where.md)|
|||[🔥 ARC](Swift/ARC.md)|
|||[🔥 Error Handling](Swift/Error%20Handling.md)|
|||Memory Safe|
|etc||[~= Operator](Swift/~%3D%20Operator.md)|
|||[zip](Swift/zip.md)|
|||[readLine()](Swift/readLine().md)|
|||[🔥 @escaping Closure](Swift/@escaping%20closure.md)|
|||[🔥 CompletionHandler](Swift/CompletionHandler.md)|
|||[Handling Decimal Point](Swift/Handling%20Decimal%20Point.md)|
|||[First-Class Citizen](Swift/First-Class%20Citizen.md)|
|||[🔥 MetaType](Swift/MetaType.md)|
|||[ObjectIdentifier](Swift/ObjectIdentifier.md)|
|||[LocalizedError](Swift/LocalizedError.md)|
|||[Result](Swift/Result.md)
|||[🔥 CoW(Copy on Write)](Swift/CoW.md)|

## 🔥 OOP(Object Oriented Programming)
### 🪧 Table of Contents
- [SOLID](OOP/SOLID.md)
  - [SRP(Single-Responsibility Principle)](OOP/SRP.md)   
  - [OCP(Open-Close-Principle)](OOP/OCP.md)
  - [LSP(Liskov Substitution Principle)](OOP/LSP.md)   
  - [DIP(Dependency Inversion Principle)](OOP/DIP.md)   
  - [ISP(Interface Segregation Principle)](OOP/ISP.md)      
  - [Value type cannot have a stored property that recursively contains it](Swift/Value%20type%20cannot%20have%20a%20stored%20property%20that%20recursively%20contains%20it.md)

## Commonly used protocols in Swift
- [Equatable](iOS/Equatable.md)
- [Comparable](iOS/Comparable.md)
- [Hashable](Swift/Hashable.md)    
- [Sendable](Swift/Sendable.md) -> 추후 정리 예정
- [CaseIterable](Swift/CaseIterable.md)

# 🗂️ Foundation
## 📕 Networking - URL Loading System
- [REST API](Network/REST%20API.md)   

|Section|Subject|Explain|   
|:--|:--|:--|
|Essential|[Fetching Website Data into Memory](Network/FetchingWebsiteDataIntoMemory.md)|URLSession에서 데이터 작업을 생성하여 <br/>데이터를 메모리로 직접 수신한다.|
||URLSession|관련된 네트워크 데이터 전송 작업 그룹을 조정하는 개체|
||URLSessionTask|
||URLSessionConfiguration|
|Request and Response|URLRequest|
||MutableURLRequest|
||URLResponse|
||HTTPURLResponse|
|Cookies<br/>Storage|HTTPCookie|
||HTTPCookieStorage|
|Cache|URLCache|
||CacheURLRequest|
|Errors|URLError|
|Protocol Support|URLProtocol|
|Authentication &<br/>Credentials|URLProtectionSpace|
||URLCredential|
||URLCredentialStorage|
||URLAuthenticationChallenge|

## 📕 Low-Level Utilities - Process and Threads
|Section|Subject|Explain|
|:--|:--|:--|
|RunLoop Scheduling|||
||RunLoop|
||Timer|
|Threads and Locking||
||[Process vs Thread](Network/Process%20vs%20Thread.md)| 프로세스와 스레드의 차이|
||[Async vs sync](Network/Async%20vs%20sync.md)| 비동기와 동기의 차이|
||[Serial vs Concurrent](Network/Serial%20vs%20Concurrent.md)|단일 스레드와 다중 스레드(동시성) 차이|
|Operations|||
||OperationQueue|
||Operation|

## 📕 Dispatch
- [GCD(Grand Central Dispatch)](Network/GCD(Grand%20Central%20Dispatch).md)

## 📗 Design-Pattern
- [Singleton](Design-Pattern/Singleton.md)
- [Factory-method](Design-Pattern/Factory-method.md)
- [Producer-Consumer](Design-Pattern/Producer-Consumer.md)

## 📕 TDD (Test Driven Development)
- [Unit Test](TDD/UnitTest.md)
- [given-when-then](TDD/given-when-then.md)
- [XCTest](TDD/XCTest.md)
- [Adding test files to an already created project](TDD/Adding%20test%20files%20to%20an%20already%20created%20project.md)
- [🌐 Reference Site](TDD/ReferenceSite.md)

## 📗 Project - Setting
- [Device Setting](Project-Setting/Device%20Setting.md)
- [Install CocoaPods(M1 Error)](Project-Setting/Install%20Cocoapods.md)
- [Install RxSwift with CocoaPods(M1 Error)](Project-Setting/Install%20RxSwift%20with%20cocoapods.md)
- [UserInterfaceState.xcuserstate 제거하기](Project-Setting/UserInterfaceState%20xcuserstate.md)
- [How to hide my APIKEY](Project-Setting/HowToHideMyAPIKEY.md)

## App 배포와 출시
- [CI/CD란?](https://github.com/JasonLee0223/TIL/blob/main/App%20%EB%B0%B0%ED%8F%AC%EC%99%80%20%EC%B6%9C%EC%8B%9C/CI,%20CD%EB%9E%80?.md)   