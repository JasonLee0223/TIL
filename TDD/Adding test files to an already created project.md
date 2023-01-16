# Adding test files to an already created project
이미 생성된 프로젝트에서 Unit Test를 진행하려면 어떻게 해야할까??

<img src="https://user-images.githubusercontent.com/92699723/211239622-7c9a1e77-80cc-40b6-8c84-f9a783c1badd.png" width = 400>

## Info.plist는 왜 또 만들어지는 것일까??
Info.plist 파일은 실행 패키지에 관한 필수 설정 정보가 포함된 구조화된 텍스트 파일이다.   
App과 Test는 서로 다른 Target으로 생성되었기에 설정을 따로 관리해 줄 필요가 있기 때문이다.   
### 😱 Info.plist 파일이 없는데요??
Xcode 13 버전 이후론는 별도의 Info.plist가 생성되지 않는다.   
없어진 것이 아니라 Target 세팅으로 숨어버렸기 때문...!!

### 🌐 Reference Site
[Xcode iOS App 프로젝트에 Unit Test 추가하기](https://zdodev.github.io/ios/xctest/Xcode-iOS-App-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%97%90-Unit-Test-%EC%B6%94%EA%B0%80%ED%95%98%EA%B8%B0/)