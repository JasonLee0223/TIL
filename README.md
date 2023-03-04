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

# iOS
|Section|Title|Subject Link|Explain|
|:--|:--|:--|:--|   
|UIKit|
|App and environment||[UIKit 설명, App and Environment](iOS/About%20App%20Development%20with%20UIKit.md)|
|App Structure|Managing your app's life cycle|[ViewController Life-Cycle](iOS/ViewController%20Life-Cycle.md)|
|User Interface|UIView|
||Configuring the bounds and frame rectangles|[var frame vs var bounds](iOS/Frame%20vs%20Bounds.md)|
|||var bounds|Same as above|
||Container Views|[UIStackView](iOS/UIStackView.md)|
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
|Windows and screens|Windows|
||Scenes|
||Popovers|
||Alerts|
||Screens|[UIScreen](iOS/UIScreen.md)|
|Touches, presses, and gestures||[UITapGestureRecognizer](iOS/UITapGestureRecognizer.md)|
|Menus and shortcuts||[UIAction](iOS/UIAction.md)|
|Core Graphics|
|Geometric Data Types||[CGPoint, CGSize, CGRect](iOS/CGPoint,CGSize,CGRect.md)|
|||CGSize|Same as above|
|||CGRect|Same as above|
|OS|
|Logs|Essentials|
||Log Messages|[Logger & OS_Log](iOS/Logger%20&%20OS_Log.md)|
|Accessibility for UIKit|
|||[File System Basics](iOS/FileSystem.md)|
|||[Sandbox 정책과 Files 앱](iOS/SandBox.md)|
|Etc|
|||[VC간의 데이터 전송방법](iOS/Data%20Transfer%20Process.md)|
|||[Delegate](iOS/Delegate.md)|
|||[magnitude & abs()](iOS/magnitude.md)|절대값 구하기|
|||[pow() & sqrt()](iOS/pow.md)|제곱, 제곱근 구하기|
|Storyboard|
|||[3 ways to change the screen](iOS/StoryBoard/3%20ways%20to%20change%20the%20screen.md)|


# Swift
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
|02|Object Oriented Programming with Swift|[Struct & Class](Swift/Struct%20vs%20Class.md)|
|||Property & Method|
|||Initialization|
|||Access Control|
|03|functional programming with Swift|[Closure](Swift/Closure.md)|
|||Optional Chaining|
|||Early-exit|guard-let|
|||[Higher-order function](Swift/Higher-order%20function.md)|고차함수: map, filter, reduce|
|||Monad|
|04|Extension|[Subscript](Swift/Subscript.md)|
|||[Inheritance](Swift/Inheritance.md)|
|||Type Casting|as, is|
|||[Protocol](Swift/Protocol.md)|
|||Extension|
|||[Generic](Swift/Generic.md)|
|||[Protocol Default Implimentations](Swift/ProtocolDafaultImplimentation.md)|프로토콜 초기구현|
|05|Swift High|Nested Type|
|||[Pattern](Swift/Pattern.md)|
|||[Where](Swift/Where.md)|
|||ARC|
|||[Error Handling](Swift/Error%20Handling.md)|
|||Memory Safe|
|etc||[~= Operator](Swift/~%3D%20Operator.md)|
|||[zip](Swift/zip.md)|
|||[readLine()](Swift/readLine().md)|
|||[@escaping Closure](Swift/@escaping%20closure.md)|미완성|
|||[Handling Decimal Point](Swift/Handling%20Decimal%20Point.md)|
|||[First-Class Citizen](Swift/First-Class%20Citizen.md)|1급 객체|
|||[MetaType](Swift/MetaType.md)|메타타입<br/>Dynamic MetaType, <br/>Static MetaType|
|||[LocalizedError](Swift/LocalizedError.md)|Error Handling|

## OOP(Object Oriented Programming)
### 🪧 Table of Contents
- [SOLID](OOP/SOLID.md)
  - [SRP(Single-Responsibility Principle)](OOP/SRP.md)   
  - [OCP(Open-Close-Principle)](OOP/OCP.md)
  - [LSP(Liskov Substitution Principle)](OOP/LSP.md)   
  - [DIP(Dependency Inversion Principle)](OOP/DIP.md)   
  - [ISP(Interface Segregation Principle)](OOP/ISP.md)      
  - [Value type cannot have a stored property that recursively contains it](Swift/Value%20type%20cannot%20have%20a%20stored%20property%20that%20recursively%20contains%20it.md)

## POP (Protocol-Oriented Language)
### 🪧 Table of Contents

## Commonly used protocols in Swift
- [Equatable](iOS/Equatable.md)
- [Comparable](iOS/Comparable.md)
- [Hashable](Swift/Hashable.md)    
- [Sendable](Swift/Sendable.md) -> 추후 정리 예정
- [CaseIterable](Swift/CaseIterable.md)

## Network
- [REST API](Network/REST%20API.md)   
- [Process vs Thread](Network/Process%20vs%20Thread.md)
- [Async vs sync](Network/Async%20vs%20sync.md)
- [Serial vs Concurrent](Network/Serial%20vs%20Concurrent.md)
- [GCD(Grand Central Dispatch)](Network/GCD(Grand%20Central%20Dispatch).md)

## Design-Pattern
- [Singleton](Design-Pattern/Singleton.md)
- [Factory-method](Design-Pattern/Factory-method.md)

## TDD (Test Driven Development)
- [Unit Test](TDD/UnitTest.md)
- [given-when-then](TDD/given-when-then.md)
- [XCTest](TDD/XCTest.md)
- [Adding test files to an already created project](TDD/Adding%20test%20files%20to%20an%20already%20created%20project.md)
- [🌐 Reference Site](TDD/ReferenceSite.md)

## Project - Setting
- [Device Setting](Project-Setting/Device%20Setting.md)
- [Install CocoaPods(M1 Error)](Project-Setting/Install%20Cocoapods.md)
- [Install RxSwift with CocoaPods(M1 Error)](Project-Setting/Install%20RxSwift%20with%20cocoapods.md)
- [UserInterfaceState.xcuserstate 제거하기](Project-Setting/UserInterfaceState%20xcuserstate.md)

## App 배포와 출시
- [CI/CD란?](https://github.com/JasonLee0223/TIL/blob/main/App%20%EB%B0%B0%ED%8F%AC%EC%99%80%20%EC%B6%9C%EC%8B%9C/CI,%20CD%EB%9E%80?.md)   