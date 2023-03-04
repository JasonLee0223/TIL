# MetaType
## 🔴 Apple Documents
<img src="https://user-images.githubusercontent.com/92699723/222877382-ec48bd02-5ae9-4bbd-9f26-72d3de4bd0f7.png" width=1000>

메타타입 유형은 클래스 유형, 구조 유형, 열거 유형 및 프로토콜 유형을 포함하여 모든 유형의 유형을 나타냅니다.    
즉, MetaType이란 타입의 타입을 나타낸다.

> 클래스, 구조체 또는 열거형 유형의 메타 유형은 유횽의 이름 뒤에 .Type이 오는 것입니다.   
> 런타임에 프로토콜을 준수하는 구체적인 유형이 아닌 프로토콜 유형의 메타 유형은 해당 프로토콜의 이름 뒤에 
> .Protocol이 붙습니다.     
> 접미사 자체 표현을 사용하여 유형에 값으로 엑세스 할 수 있습니다.
> 또한 인스턴스와 함께 `type(of:)`함수를 호출하여 해당 인스턴스의 동적 런타임 유형에 값으로 엑세스 할 수 있습니다.

```Swift
// Example
class SomeBaseClass {
    class func printClassName() {
        print("SomeBaseClass")
    }
}

class SomeSubClass: SomeBaseClass {
    override class func printClassName() {
        print("SomeSubClass")
    }
}
let someInstance: SomeBaseClass = SomeSubClass()
// The Compile-time type of someInstance is SomeBaseClass,
// and the runtime type of someInstance is SomeBaseClass
type(of: SomeInstance).printClassName()
// Prints "SomeSubClass"
```
> initializer 표현식을 사용하여 해당 유형의 메타타입 값에서 유형의 인스턴스를 구헝할 수 있습니다.   
> 클래스 인스턴스의 경우 호출되는 이니셜라이저는 필수 키워드 또는 final 키워드로 표시된 전체 클래스로 표시되어야 합니다.
```Swift
class AnotherSubClass: SomeBaseClass {
    let string: String
    required init(string: String) {
        self.string = string
    }
    override class func printClassName() {
        print("AnotherSubClass")
    }
}
let metatype: AnotherSubClass.Type = AnotherSubClass.self
let anotherInstance = metatype.init(string: "some string")
```
## 🟢 Blog Article
```Swift
struct Human {
    static let name = "Jason"
    var age = 30
}
```
위와 같은 구조체에는 `타입 프로퍼티 name`과 `인스턴스 프로퍼티인 age`가 있다.   
그럼 아래와 같이 호출할 수 있다.
```Swift
let jason = Human.init()

Human.name      // Jason
jason.age       // 30
```
`타입 프로퍼티`는 **타입 이름만 알면 호출이 가능**하고 `인스턴스 프로퍼티`는 **인스턴스를 생성해야만 호출이 가능**하다.   
> 🤔 이럴 때 Human이란 타입 이름을 모른다고 가정하면, name 프로퍼티를 호출할 수 있을까??

이럴 때 사용하는 메서드가 `type(of:)` 메서드를 사용한다.   
**해당 타입의 인스턴스를 저장하는 게 아니라** `해당 타입 자체를 저장`할 수 있단 말이다.   
```Swift
let jasonType = type(of: jason)         // Human.Type
jasonType.name                          // Jason
```
> 💡 Jason이란 인스턴스를 type(of:)에 넣으면 Human 타입 자체를 반환받아서 저장할 수 있다.   
> 또한 반환받아 저장한 jasonType이란 변수는 `Human 타입 자체`이기 때문에    
> `타입 프로퍼티인 name에도 접근`할 수가 있는 것!

> `"타입 자체"`란 것이 `"메타 타입"`인 것이다!!

### MetyType은 언제 사용하면 좋을까?
generic 함수와 사용하면 인스턴스화를 시키거나 각 타입에 따라 작업할 수 있게된다.
```Swift
protocol Human {
    var job: String { get set }
    init(_ job: String)
}

struct Buddy: Hunman {
    var job: String
    
    init(_ job: String) {
        self.job = job
    }
}

struct Bud: Human {
    var job: String

    init(_ job: String) {
        self.job = job
    }
}

func create<T: Human>(type: T.Type) -> T {
    switch type {
    case is Buddy.Type:
        return T.init("buddy")
    case is Student.Type:
        return T.init("bud")
    default"
        fatalError("Type Error")
    }
}
```
이런 시그로 type이란 파라미터의 타입을 제네릭 T 타입의 타입, 즉 `T의 메타타입을 받아서` 해당 타입을 체크하여  
`각 타입에 맞는 작업을 한 인스턴스를 생성하여 반환`시킬 수도 있다는 말이다. 

### Static Metatype vs Dynamic Metatype
- Static MetaType: self를 이용해 만드는 것
  - `.self`는 `Static MetaType`이라 `컴파일 시점`에 타입이 정해진다.
- Dynamic MetyType: type(of:)를 이용해서 만드는 것
  - `type(of:)`는 `Dynamic MetaType`이라 `런타임 시점`에 정해진다.

```Swift
// .self를 이용해 메타타입 값을 얻어낼 경우
Buddy.self.init("")

// type(of:)를 이용해 값을 얻어낼 경우
let anyType: Any = 10
type(of: anyType)       // Int.Type
```

### 🌐 Reference Site

[Swift) Metatype(.self, .Type, .Protocol) 정복하기 (1/2) - 소들이](https://babbab2.tistory.com/151)   
[[Swift] Metatype 이란? (.Type, .self, .Protocol) (번역)](https://onelife2live.tistory.com/49)   
[Apple Document - Types](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/types/)   
[type(of:) | Apple Developer Documentation](https://developer.apple.com/documentation/swift/type(of:))