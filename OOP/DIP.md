# 4️⃣ 의존성 역전 원칙(DIP: Dependency Inversion Principle)
- 상위 수준의 모듈은 하위 수준의 모듈에 의존해서는 안된다. → 구체적인 것은 잘 변한다.
  두 모듈 모두 추상화(abstract)에 의존하게 만들어야한다.
  풀어서 정리하면, 어떤 상위 모듈에서 하위 모듈을 가지고 있을 때, **`상위 모듈의 기능이 하위 모듈에 의존해서는 안된다는 뜻`** 으로,   
  **`추상화를 진행하여 각각의 모듈에 더 추상화된 것에 의존하게 만들어야한다는 뜻`** 이다.   
  이렇게 설계해야 재사용에도 유리하고 하나를 수정하더라도 더욱 수정사항이 많이 없는 훌륭한 프로그램을 설계할 수 있게된다.

- 구체적인 사항은 추상화에 의존해야한다. → 추상적인건 잘 안변한다.

- delegate가 가장 대표적인 예

예시를 통해 살펴보자.
```Swift
// DIP를 위반한 예시
class APIHandler {
    func request() -> Data {
        return Data(base64Encoded: "This Data")
    }
}

class LoginService {
    let apiHandler: APIHandler = APIHandler()

    func login() {
        let loginData = apiHandler.request()
        print(loginData)
    }
}
```
위 코드에서 상위 모듈인 `LoginService`가 하위 모듈인 `APIHandler`에 의존하고 있는 관계로   
만약 `APIHandler`의 구현 방법이 변화하게 되면 프로그램에 영향을 미치게 되고   
새롭게 `LoginService`라는 상위모듈을 수정하게되는 상황이 발생하게될 수 있다.   
이를 개선해보면...

```Swift
protocol APIHandlerProtocol {
    func requestAPI() -> Data
}

class LoginService {
    let apiHandler: APIHandlerProtocol

    init(apiHandler: APIHandlerProtocol) {
        self.apiHandler = apiHandler
    }

    func login() {
        let loginData = apiHandler.requestAPI()
        print(loginData)
    }
}

class LoginAPI: APIHandlerProtocol {
    func requestAPI() -> Data {
        return Data(base64Encoded: "User")!
    }
}

let loginAPI = LoginAPI()
let loginService = LoginService(apiHandler: loginAPI)
loginService.login()
```
위와 같이 작성하면 `LoginService`는 기존에 `APIHandler`에 의존하지 않고 `추상화 시킨 객체인 APIHandlerProtocol`에 의존하게 된다.   
그렇기 때문에 `APIHandlerProtocol`의 구현부는 외부에서 변화에 따라 지정해서 지정해주면 되기 때문에   
`LoginService`는 구현부에 상관없이 좀 더 변화에 민감하지 않은 DIP 원칙을 지킨 프로그램 설계에 다가갈 수 있다!

### ⭐️ 외부에서 내부의 변수를 초기화해서 의존관계를 가지는 경우를 의존성 주입이라고 하게 된다.   
### 이때, 의존성 주입을 추상화시켜 진행하게 되면 더욱 변화에는 안전한 프로그램을 설계할 수 있게 된다.