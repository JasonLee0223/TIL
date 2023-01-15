# TIL
매일매일 학습하여 커밋을 남겨보자!

## Git
|Subject|Link|Explain|
|:--|:--|:--|
|Git Commit|[Commit message style](Git/Commit%20message%20style.md)|

## CS10
|Subject|Link|Explain|
|:--|:--|:--|
|Introduce|[Introduce](CS10/Introduce%20CS10.md)|
|Binary|[Half-Adder](CS10/Half-Adder.md)|

## API Design Guidelines
### 🪧 Agenda
|Section|Subject|Explain|   
|:--|:--|:--|   
|📕 Fundamentals|[Fundamentals](APIDesignGuideline/Fundamentals.md)|(핵심개념)|
|📗 Naming|[Promote Clear Usage](APIDesignGuideline/Promote%20Clear%20Usage.md)|(명확하게 사용하기)|
||[Strive for Fluent Usage](APIDesignGuideline/Strive%20for%20Fluent%20Usage.md)|(자연스러운 사용을 위해 노력하기)|
||[Use Terminology Well](APIDesignGuideline/Use%20Terminology%20Well.md)|(적절한 기술 용어 사용하기)|
|📘 Conventions|General Conventions|(일반 규칙)|
||Parameters |(매개변수)|
||Argument Labels|(전달인자 레이블)|
|📙 Special Instructions|Special Instructions|(특별 지침들)|
|📖 Article|[✏️ Bool 변수 이름 제대로 짓기 위한 최소한의 영문법](Naming/BoolNaming.md)|

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
|Storyboard|
|||[3 ways to change the screen](iOS/StoryBoard/3%20ways%20to%20change%20the%20screen.md)|


# Swift
- [~= Operator](Swift/~%3D%20Operator.md)
- [zip](Swift/zip.md)
- [Dictionary](Swift/Dictionary.md)
- [Enum](Swift/Enum.md)   
- [readLine()](Swift/readLine().md)
- [Handling Decimal Point](Swift/Handling%20Decimal%20Point.md)
- [@escaping Closure](Swift/@escaping%20closure.md) -> 미완료

## OOP(Object Oriented Programming)
### 🪧 Table of Contents
- [SOLID](OOP/SOLID.md)
  - [SRP(Single-Responsibility Principle)](OOP/SRP.md)   
  - [OCP(Open-Close-Principle)](OOP/OCP.md)
  - [LSP(Liskov Substitution Principle)](OOP/LSP.md)   
  - [DIP(Dependency Inversion Principle)](OOP/DIP.md)   
  - [ISP(Interface Segregation Principle)](OOP/ISP.md)   
- [Struct vs Class](Swift/Struct%20vs%20Class.md)   

## POP (Protocol-Oriented Language)
### 🪧 Table of Contents
- [First-Class Citizen(1급 객체)](Swift/First-Class%20Citizen.md)
- [Closure Syntax](Swift/Closure.md)
- [Higher-order function (고차함수)](Swift/Higher-order%20function.md)

## Extension (확장)
- [Subscript](Swift/Subscript.md)
- [Inheritance](Swift/Inheritance.md)
- [Protocol Syntax](Swift/Protocol.md)   
- [Generic](Swift/Generic.md)
- [Protocol Default Implimentations(프로토콜 초기구현)](Swift/ProtocolDafaultImplimentation.md)   

## Swift High Class (고급)
- [Pattern](Swift/Pattern.md)
- [Error Handling](Swift/Error%20Handling.md)   

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