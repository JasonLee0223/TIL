# Device Setting
그동안 프로젝트를 빌드하였을 때 시뮬레이터만 거의 사용하여 확인하였다가 이번에 Shake Event를 사용하게되어 실제 기기에 연결하였을때 겪었던 내용을 바탕으로 정리하였다.

## Build Fail
실제 기기에 연결하여 홈화면에 아이콘이 다운로드되고 신뢰할 수 없다는 에러 메세지를 마주치게된다.   
<img src = "https://user-images.githubusercontent.com/92699723/183831292-fbd159f1-09d8-4452-8248-bb35374cce31.jpg" width="300" height="300">   
<img src = "https://user-images.githubusercontent.com/92699723/183831326-0167b808-cf0b-45a3-a835-f6d78104e1c1.png" width="600" height="400">

### Error Message
**Failure Reason**
Could not launch "ProjectName"
The operation couldn’t be completed. Unable to launch opendoorLife.NavigationBarCheck because it has an invalid code signature, inadequate entitlements or its profile has not been explicitly trusted by the user.

## Solution
(조건)에러메세지가 나온 프로젝트 App이 설치되어있어야한다.
1. 실제 디바이스의 '설정(Settings)' -> '일반(General)'까지 들어간다.
2. 'VPN 및 기기관리' 항목으로 들어간다.
3. 해당 "앱" 클릭
4. 개발자 신뢰를 위해 파란 텍스트 클릭 후 팝업이 뜨면 '신뢰' 클릭
5. '확인 완료' 버튼 확인 뒤 해당 프로젝트가 문제없이 실행됨을 확인할 수 있다.

<img src = "https://user-images.githubusercontent.com/92699723/183835659-2dc80724-6b2a-4398-9409-2020aa11ea16.jpg" width="400" height="500">   
<img src = "https://user-images.githubusercontent.com/92699723/183835649-ad0020b0-875d-4c2a-80ad-71fdbcfe7f88.jpg" width="400" height="500">   
<img src = "https://user-images.githubusercontent.com/92699723/183835640-b54a8181-69e5-4c63-b874-468279ec705f.jpg" width="400" height="300">   

## 실제기기(아이폰)에서 시뮬레이터 화면 녹화하기
어플을 사용할 수 있지만 기존에 맥에 내장되어있는 QuickTime Player를 사용하여 녹화할 수 있다.
여기서 주의할 점이 **현재 맥미니를 사용하는데 외부캠을 사용하다보니 연결되어있으면 아이폰을 인식하지 못하는 현상이 발생했었다.**   
하여 맥미니에서 캠을 연결해제(포트에서 제거)한 후 작동하여보니 잘되었다.

### 🌐 참고사이트   
[Xcode :: 실제 디바이스 빌드 실패 해결 (Invalid code signature, inadequate entitlements or its profile has not been explicitly trusted by the user)](https://opendoorlife.tistory.com/11)   
[[iOS] Xcode 시뮬레이터 녹화하기, 아이폰 화면 녹화하기 (동영상, GIF로 저장하기)](https://lxxyeon.tistory.com/35)