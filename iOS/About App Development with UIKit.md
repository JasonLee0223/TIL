# About App Development with UIKit
> Apple의 통합 개발 환경인 Xcode에서 프로젝트를 생성하여 항상 iOS 또는 tvOS 앱 개발을 시작합니다.   
Xcode가 없으면 App Store에서 다운로드할 수 있습니다. [developer.apple.com](https://developer.apple.com/)에서 최신 버전을 다운로드할 수도 있습니다.   

> 앱을 빌드할 때 Xcode는 소스 파일을 컴파일하고 프로젝트에 대한 App Bundle들을 생성합니다.   
App Bundle들은 앱과 관련된 코드와 리소스를 포함하는 구조화된 디렉터리입니다.    

`Resource에는 코드를 지원하는 Image Asset, Storyboard files, string Files 및 App metaData가 포함됩니다.`   

- ☑️ Required App Metadata  
  모든 UIKit앱에는 아래의 resource가 필요합니다.
  - App icons   
    시스템은 홈 화면, 설정 및 앱을 다른 앱과 구별해야 하는 `App icon`을 표시합니다.   
    App icon은 사용자가 홈 화면에서 빠르게 앱을 식별할 수 있도록 고유해야합니다.
  - Launch screen storyboard   
    사용자가 App icon을 탭하면 시스템이 즉시 시작 화면을 표시하여 앱이 시작되고 있음을 알립니다.   
    시작 화면은 앱이 자체적으로 초기화되는 동안 앱에 대한 `cover를 제공합니다.   
    앱이 준비되면, 시스템은 시작 화면을 숨기고 앱의 실제 인터페이스를 표시합니다.

- ☑️ Required App Metadata  
    - 시스템은 App bundle의 정보 속성 목록(Info.plist)파일에서 앱의 구성 및 기능에 대한 정보를 가져옵니다.    
    - Info.plist 파일에 대한 일반적인 수정 사항 중 하나는 앱의 HW & SW 요구사항을 선언하는 것입니다.   
      이 요구 사항은 앱을 실행하는 데 필요한 사항을 시스템에 전달하는 방법입니다.   
      Info.plist 파일에 포함할 수 있는 키에 대한 정보는 다음 링크를 통해 확인할 수 있습니다.   
      [Information Property List Key Reference](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009247)

- ☑️ Code Structure of a UIKit App
  - UIKit은 `시스템과 상호 작용`하고 `앱의 메인 이벤트 루프를 실행`하고 `콘텐츠를 화면에 표시`하는 것을 포함하여 앱의 많은 핵심 객체를 제공합니다.
  - UIKit 앱의 구조는 MVC Design Pattern을 기반으로 하고, 객체는 목적에 따라 구분됩니다.
    - Model: 앱의 데이터와 비즈니스 로직을 관리
    - View: 데이터의 시각적 표현을 제공
    - Controller: Model과 View 객체 사이의 다리 역할을 하여 적절한 시간에 이들 사이에서 데이터를 이동
    <img src = "https://user-images.githubusercontent.com/92699723/189046549-71cdaeb3-4ce0-41cc-a243-9e7e3be81034.png" width = "300" height="200">
  - UIKit 및 Foundation framework는 앱의 모델 객체를 정의하는 데 사용하는 많은 기본 유형을 제공합니다.   
    - UIKit: 디스크 기반 파일(disk-based file)에 속하는 데이터 구조를 구성하기 위한 [UIDocument](https://developer.apple.com/documentation/uikit/uidocument)개체를 제공합니다.  
    앱의 controller 및 view layers에 있는 대부분의 개체를 제공합니다.   
    특히 UIKit은 일반적으로 콘텐츠를 화면에 표시하는 역할을 하는 UIView 클래스를 정의합니다.

    - Foundation framework: 문자열, 숫자, 배열 및 기타 데이터 유형을 나타내는 기본 개체를 정의합니다.   
      [Swift Standard Library](https://developer.apple.com/documentation/swift/swift-standard-library)는 Foundation framework에서 사용할 수 있는 동일한 유형을 많이 제공합니다.

    - [UIApplication](https://developer.apple.com/documentation/uikit/uiapplication)객체는 앱의 `main event loop`를 실행하고 앱의 전체 Life-cycle 주기를 관리합니다.


## 🟢 App and Environment

### ✔️ Life-Cycle

### ✔️ iPad

### ✔️ Device Environment

### ✔️ Adaptivity

### ✔️ Guided Access

### ✔️ Architecture


[About App Development with UIKit | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/about_app_development_with_uikit)    
[App and Environment | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/app_and_environment)