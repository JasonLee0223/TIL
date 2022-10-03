# Singleton
## 들어가며...
소프트웨어를 만들다보면 어떤 클래스의 객체가, 해당 프로세스내에서 `딱 하나`만 만들어져 있어야 할 때가 있다.   
사용자가 개발자가 만든 앱을 사용하는데 세팅해서 다크모드를 설정해놓으면 다른 페이지로 이동하더라도 이 다크모드가 그대로 유지되어   
있어야하는 예를 생각해보면 쉽다.   

어떤 페이지에 있던 이 세팅을 관리하는 객체는 반드시 같은 것을 사용해야한다는 것.   
그렇다면 당연히 이 객체가 하나만 만들어져있도록 해야한다.   

여기서 `static`으로 클래스 자기 자신을 Type화하여 객체를 하나 만들어낸다.   
클래스 안의 static이 아닌 변수나 메서드들은 객체가 생성될 때마다 메모리의 공간을 새로 차지하지만 `static`으로 선언된 것들은   
객체가 얼마나 만들어지든 메모리의 지정된 공간에 딱 하나씩만 존재하게 된다.   

컴파일 할 때부터 이 요소가 차지할 메모리 용량을 이미 알 수 있도록 딱 정해져 있기 때문에 이런 동적 요소들과 대비되는 개념으로   
`static`, 정적이라고 불리는 것.   

## 1. Singleton Pattern이란?
**특정 용도로 객체를 하나만 생성하여, 공용으로 사용하고 싶을 때 사용하는 디자인 유형**

### Example
```Swift
// 사용자의 정보를 저장하는 클래스
class UserInfo{
    var id: String?
    var password: String?
    var name: String?
}
```
이후   
`A - Viewcontroller 에서는 id`를,   
`B - ViewController 에서는 password`를,   
`C - ViewController에서는 name`을 입력받아   
**UserInfo**라는 클래스에 저장해야 한다고 가정하면

```Swift
// A - ViewController
let userInfo = UserInfo()
userInfo.id = "User_Id"
```

```Swift
// B - ViewController
let userInfo = UserInfo()
userInfo.password = "123"
```

```Swift
// C - ViewController
let userInfo = UserInfo()
userInfo.name = "User_name"
```
이런 식으로 A, B, C ViewController에서 **각각 UserInfo 객체를 만들어서** `저장`하면,   
<img src="https://user-images.githubusercontent.com/92699723/193549720-eced31bb-5864-4c89-9b17-1b2dc5e9ca36.png" width="600" height="300">   
위와 같이 `각 Instance의 프로퍼티에만 저장될 것`이고 원하는 것처럼 `하나의 Instance에 모든 정보가 저장`되지 않는다.   

### 💭 Singleton 방법이 아닌 다른 방법?   
인스턴스는 `참조` 타입이기 때문에, UserInfo 인스턴스를 **한 번 생성**한 후,   
이 인스턴스를 A -> B -> C로 필요할 때마다 `참조를 넘겨줄 수 있긴 하다.`   
하지만 이렇게 되면 App 안에서 어떤 클래스던 UserInfo 인스턴스가 참조되어야 할 때마다 매번 이 인스턴스를 넘겨주어야하는데...   
코드가 너무 지저분해진다...

🔴 그렇기 때문에, **이 클래스에 대한 Instance는 최초 생성될 때 딱 한 번만 생성해서 전역에 두고,   
그 이후로는 이 Instance만 접근 가능하게 하자**는 목표가 생겼고 `Singleton Pattern`이 만들어지게 된 계기이다.

<img src="https://user-images.githubusercontent.com/92699723/193551566-852f56b2-f613-4920-a8d3-5e34c0784984.png" width="400" height="300">   

이런 식으로 **한 Instance에 어디 클래스에서든 접근 가능**하게 하는 것이다.

## 2. Singleton Class 만드는 방법
### 2-1. static 프로퍼티로 Instance 생성하기
전역으로 저장될 것이기 때문에, `static`을 이용해 **Instance를 저장할 `프로퍼티`를 하나 생성**한다.
```Swift
class UserInfo {
    static let shared = UserInfo()

    var id: String?
    var password: String?
    var name: String?
}
```
### 2-2. init 함수 접근제어자를 private로 지정하기
혹시라도 **init 함수를 호출해 `Instance를 또 생성`하는 것을 막기 위해**,
private로 감춘다.
```Swift
class UserInfo {
    static let shared = UserInfo()

    var id: String?
    var password: String?
    var name: String?

    private init()
}
```
### 2-3. Singleton Class에 접근하는 방법
아까 생성해뒀던 `static 프로퍼티`를 이용하면 된다.
```Swift
// A ViewController
let userInfo = UserInfo.shard
userInfo.id = "User_Id"
```

```Swift
// B ViewController
let userInfo = UserInfo.shard
userInfo.password = "123"
```

```Swift
// C ViewController
let userInfo = UserInfo.shard
userInfo.name = "User_name"
```
어떤 클래스에서던 `shard`란 `staic 프로퍼티로 접근`하면, 하나의 Instance를 공유하는 것이다.

## Singleton 장단점

### 장점 👍🏻
- 한 번의 Instance만 생성하므로 메모리 낭비를 방지할 수 있음
- Singleton Instance는 전역 Instance로 다른 클래스들과 자원 공유가 쉬움
- DBCP(DataBase Connection Pool)처럼 공통된 객체를 여러개 생성해서 사용해야하는 상황에서 많이 사용   
(쓰레드풀, 캐시, 대화상자, 사용자 설정, 레지스트리 설정, 로그 기록 객체등)

### 단점 👎🏻
- Singleton Instance가 너무 많은 일을 하거나, 많은 데이터를 공유시킬 경우 다른 클래스의 Instance들 간 결합도가 높아져   
"개방=폐쇄" 원칙을 위배함 (객체 지향 설계 원칙 어긋남)
- 따라서 수정과 테스트가 어려워짐 

### 참고사이트 🌐
[객체지향 디자인패턴1 - 얄팍한 코딩사전](https://www.youtube.com/watch?v=lJES5TQTTWE)   
[Swift) 싱글톤 패턴(Singleton Pattern) - 개발자 소들이](https://babbab2.tistory.com/66)