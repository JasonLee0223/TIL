# Factory method
## 들어가며...
예를 들어 감기에 걸려서 약국에 갔다.   
감기약을 사러 왔다고 하니까 약사가 약 열몇가지를 집어와서 계산대에 늘어놓더니   
"이건 OO제약의 OO이고, 이건 어디의 뭐고요..."   
하나하나 집어들고 설명하고 있으면 답답할것이다.   
이런 경우를 탈피하기 위해 Factory method를 사용하게된다.   

Factory Pattern에는 크게 2가지 효용을 가진다.
1. 객체를 생성하는 코드는 여러 곳에 있을 수 있다. 그런데 만약 생성자가 변경되거나 하면 이 코드를 하나하나 찾아내서   
새 생성자 형식에 맞게 코드들을 변경해줘야한다.   
**객체를 생성하는 코드들이 많으면 많을수록 객체의 생성자를 변경하거나, 사용되는 객체 자체를 변경하는데 있어 부담이 커지게된다.**   
`이 역할을 팩토리 클래스가 대신하도록 하면 이제 이 메서드 내부만 변경시키면 된다.`

2. 조건에 따라 객체를 생성해 가져오는 일을 팩토리 클래스에 위임해버림으로써 상위클래스를 구현하는 개발자들로 하여금   
하위 클래스에 대해 알 필요가 없도록 하는 것이다. 이미 현존하는 프레임워크 위에서 기존에 만들어진 라이브러리, 클래스들을 활용한다.   
**특정 종류의 기능들에 사용될 수 있는 클래스들의 종류가 많고 복잡할 때 이를 사용하는 개발자 측에서 이들을 다 알 필요 없이   
`사용할 객체의 조건들만 인자로 넘겨주면 이에 적절한 클래스를 찾아 객체로 생성해 넘겨주는 일은 팩토리가 알아서 처리하는 것.`**   
또한 단순히 클래스를 골라주는 것 뿐아니라 간단한 팩토리 클래스로 필요에 따라 넘겨주는 조건에 맞춰 여러가지 조합의 결과물을 만들어낼 수 있다.   

## 1. Factory Method란?
Factory 패턴은 객체를 생성하는 모듈인 `Factory`를 만들어놓고 요청에 따라 객체를 생성하는 패턴이다.   
생성 관점의 디자인 패턴(Creational Design Patterns)의 일종으로, 인스턴스 생성을 팩토리 타입의 메서드에 위임하는 방식이다.   
객체를 만들기 위한 인터페이스를 정의하지만, 어떤 클래스의 인스턴스를 생성할지에 대한 결정은 하위클래스가 정하도록 하는 방법이다.   
간단하게 말해 **`객체 생성을 서브 클래스가 하도록 처리하는 패턴`** 이다.   
즉, **`객체 생성을 처리하는 팩토리를 프로토콜로 관리하여 실질적인 생성을 캡슐화할 수 있으며`**   
**`이로 인해 부모 클래스는 자식 클래스가 어떤 객체를 생성하는지 몰라도 된다.`**   
(개발자들에게 이용하는 타입에 대한 정보를 숨기고 인스턴스 생성을 용이하게 해준다.)

## 1-1. Factory Method의 구조
Factory method는 아래와 같은 구조를 갖게된다.   
<img src="https://user-images.githubusercontent.com/92699723/193657704-81f558ff-364d-4cbf-8773-6493b5db66e3.png" width="500" height="300">   

- Product   
    Creator와 하위 클래스가 생성할 수 있는 모든 객체에 동일한 인터페이스를 선언합니다.
    ```Swift
    // Product
    protocol Product {
        func hello()
    }
    ```

- Concrete Product(구체적인 객체)   
    Product가 선언한 인터페이스로 만든 실제 객체이다.
    ```Swift
    // Concrete Product
    class A: Product {
        func hello() {
            print("Hello, I'm A")
        }
    }

    class B: Product {
        func hello() {
            print("Hello, I'm B")
        }
    }
    ```

- Creator   
    새로운 객체를 반환하는 팩토리 메서드를 선언한다. (= Factory의 역할을 정의한다.)   
    여기서 반환되는 객체는 Product 인터페이스를 준수하고 있어야한다.
    ```Swift
    // Creator
    protocol Factory {
        func createProduct() -> Product
    }
    ```

- Concrete Creator   
    기본 팩토리 메서드를 override하여(또는 프로토콜 준수) 서로 다른 Product 객체를 만든다.
    ```Swift
    // Concrete Creator
    class AFactory: Factory {
        func createProduct() -> Product {
            return A()
        }
    }

    class BFactory: Factory {
        func createProduct() -> Product {
            return B()
        }
    }
    ```
- Client는 Factory를 활용해 Product를 생성하고 활용한다.
  ```Swift
  class Client {
    func order(factory: Factory) {
        let electronicsProduct = factory.createProduct()
        electronicsProduct.hello()
    }
  }

  var client = Client()
  client.order(factory: AFactory()) // Hello, I'm A   

  client.order(factory: BFactory()) // Hello, I'm B
  ```

## 2. Factory Method Pattern은 언제 사용하는가?
객체를 직접 만드는 것이 아닌 팩토리 메서드를 통해서 만드는 것.   
새로운 객체가 생기거나 객체에 대한 수정이 생겨도, 클라이언트가 아닌 Factory만 수정하면 되기 때문에 코드 간 결합성을 낮출 수 있기 때문입니다.   
이는 코드 사용에 강력한 유연성을 제공합니다. 


### 참고사이트 🌐
[객체지향 디자인패턴2 - 얄팍한 코딩사전](https://www.youtube.com/watch?v=q3_WXP9pPUQ&t=74s)
[[Swift 디자인 패턴] Factory Method Pattern(팩토리 메서드) - 디자인 패턴 공부 4](https://icksw.tistory.com/237)   
[[디자인 패턴] Factory pattern in Swift](https://velog.io/@ryan-son/%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4-Factory-pattern-in-Swift)   
[[iOS Design Pattern] Factory Method](https://inuplace.tistory.com/1170)