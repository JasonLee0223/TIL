# UIScreen
An object that defines the properties associated with a hardware-based display.   
(하드웨어 기반 디스플레이와 관련된 속성을 정의하는 개체이다.)

iOS 기기에는 기본 화면과 0개 이상의 연결된 화면이 있다.   
객체는 콘텐츠를 표시하는 화면에 대한 화면 객체를 제공합니다.    
iOS8 이상에서 화면 속성은 화면의 인터페이스 방향을 고려합니다.  

- UIScreen
    기기에 연결되는 물리적인 화면을 정의하는 객체
- UIWindow
    화면 그리기 지원 도구를 제공하는 객체
- UIView
    그리기를 수행할 객체 세트

## main에 대한 고민
UIScreen.main.bounds를 통해 기기별 해상도(픽셀) 또는 인치(inch)를 구할 수 있는데 여기서 말하는 main이 정확히 어떤 걸 의미하는지 파악이 잘되지않아 찾아보게되었다.   
main은 이제 WWDC2022에서부터 `Deprecated`로 분류되어 잘사용하지 않게되는 것 같지만 아직까지 처음 iOS를 접할 때 많이 보게되었다.   
**main은 장치의 화면을 나타내는 화면 개체를 반환한다.**
<img src= "https://user-images.githubusercontent.com/92699723/186509428-3e8bf8a2-259c-4194-9c53-cd6c09d0dcb5.png" width="650" height="450">

### 자주사용되는 UIScreen Property
좌표 공간 얻기
- coordinateSpace
- fixedCoordinateSpace

Size(크기) 및 Scale 얻기
- bounds: 포인트로 측정된 화면의 경계 사각형
- nativeBounds: 픽셀 단위로 측정한 실제 화면의 경계 사각형
- nativeScale: 물리적 화면의 기본 배율
- scale: 화면과 관련된 자연 스케일 팩터   
    기본적으로 기기별의 사이즈를 구할 때는 UIScreen.main.bounds로 구할 수 있으나, 레티나 디스플레이가 나오면서   
    각각의 기기에 따라 scale변수가 추가되어, 실제 픽셀의 개수를 의미하는 해상도를 구할 수 있다.

밝기 관리
- brightness: 화면 밝기 수준
- wantsSoftwareDiming

화면 모드 관리
- currentMode: 화면과 연결된 현재 화면 모드
- preferredMode: 화면의 기본 표시 모드
- availableModes: 화면과 연관괼 수 있는 디스플레이 모드

## 앱 인터페이스와 구성요소
<img src = "https://user-images.githubusercontent.com/92699723/186512843-6a1ff143-c03b-4c8d-a298-cba9c6be646e.png" width="300" height="300">

## UIKit 프레임워크와 화면 구성요소의 관계
<img src = "https://user-images.githubusercontent.com/92699723/186512840-1622e101-3e1c-4636-b49d-785929d209b6.png" width="300" height="350">

## UIKit 프레임워크에서 화면 구성요소의 관계 속성
<img src = "https://user-images.githubusercontent.com/92699723/186512824-cc3f4ad8-1103-42a5-bac7-f4bc76d6fd37.png" width="650" height="300">

### 🌐 참고사이트   
[UIScreen | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uiscreen)   
[main | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uiscreen/1617815-main)
[[SWIFT] 기기별 해상도(픽셀) 및 인치 구하기](https://g-y-e-o-m.tistory.com/175)   
[[iOS] UIScreen Swift에서 디바이스 사이즈 인식하기(UIScreen Size)📱](https://borabong.tistory.com/10)   
[[iOS] UIScene, UIWindowScene, UISceneSession, UIScreen](https://velog.io/@leeyoungwoozz/iOS-UIWindowScene-UIScreen)   
[[iOS] UIScreen, UIWindowScene, UIWindow, UIView](https://velog.io/@loinsir/iOS-UIScreen-UIWindowScene-UIWindow-UIView)