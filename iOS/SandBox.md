# Sandbox 정책과 Files 앱

## 🤔 Sandbox란?
외부로부터 들어온 프로그램이 보호된 영역애서 동작해 시스템이 부정하게 조작되는 것을 막는 보안 형태   

Apple은 **`보안`** 에 아주 민감하게 생각을 하고있다.   
그래서 사용자 정보에 접근하려면 반드시!!! 사용자에게 명시적으로 허락을 받아야한다.   

Sandbox는 커널 수준에서 시행되는 **`접근 제어 기술`** 이다.   

왼쪽은 Sandbox가 없을 때 파일에 접근하는 모습이다.   
> 우리의 앱을 실행하는 사용자가 모든 권한을 가지며, 사용자가 접근할 수 있는   
모든 리소스에 접근할 수 있다면 어떠한 문제점이 발생할까??

해당 앱 또는 연결된 프레임워크에 보안적인 허점이 있는 경우,   
공격자는 해당 앱을 제어하기 위해 해당 취약점을 악용할 수 있으며, 사용자가 수행할 수 있는 모든 작업을 수행할 수 있게 된다.   
하여 이러한 문제를 완화해보도록 설계된 것이 바로 `App을 Sandbox화 하는 것`이다.   

## ♟️ App Sandbox 전략
1. App Sandbox를 사용하면, 앱이 시스템과 상호 작용하는 방식을 설명할 수 있다.   
   -> **`시스템에서 작업을 완료하는 데 필요한 접근권한을 앱에 부여하는 것이다.`**
2. App Sandbox를 사용하면, 열기 및 저장, 드래그 앤 드롭 및 친숙한 사용자 상호 작용을 통해   
앱에 투명하게 추가 접근 권한을 부여할 수 있다.   

iOS는 앱 설치 시 각 앱(환경설정 및 데이터 포함)을 Sandbox에 저장한다.   
Sandbox는 파일, 환경설정, 네트워크 리소스, 하드웨어 등에 대한 앱의 접근을 제한하는 세분화된 제어 집합이라고 볼 수 있다.   
이렇게 데이터를 분리하여 **`고립!!`** 시키고, 보안 침해의 가능성을 낮춰줄 수 있는 것이다.   
즉, **`📌 내 앱은 내 앱안에 있는 데이터 이외에는 접근을 못한다는 것이다.`**

사용자 데이터는 앱 "외부"에 있을 것이고! 이렇게 Sandbox화 된 내가 만든 앱은 사용자 데이터에 접근을 못하게된다.

### 🌐 Reference Site
[[Apple Develop] About App Sandbox](https://developer.apple.com/library/archive/documentation/Security/Conceptual/AppSandboxDesignGuide/AboutAppSandbox/AboutAppSandbox.html)   
[[ZeddiOS]iOS ) Apple의 Sandbox정책과 Files앱](https://zeddios.tistory.com/432)   