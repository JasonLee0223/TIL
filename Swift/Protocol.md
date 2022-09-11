# Protocol
- 특정 클래스와 관련없는 프로퍼티, 메서드 **선언** 집합
    - 함수(메서드) 정의는 없음
    - 기능이나 속성에 대한 설계도
    - Class(Struct, Enum)에서 채택(adopt)하여 메서드를 구현해야 함
- 프로토콜은 정의를 하고 제시를 할 뿐이지 **스스로 기능을 구현하지 않는다!**
- **프로토콜 채택하여 프로토콜의 요구사항을 실제로 구현할 수 있다.**
    
    ```swift
    protocal 프로토콜 이름 {
    	// 프로토콜 정의
    }
    struct SomeStruct: AProtocal, AnotherProtocal {
    	// 구조체 정의
    }
    class SomeClass: AProtocal, AnotherProtocal {
    	// 클래스 정의
    }
     enum SomeEnum: AProtocal, AnotherProtocal {
    	// 열거형 정의
    }
    ```
    
- 어떤 프로토콜의 **요구사항을 모두 따르는 타입은 그 ‘프로토콜을 준수한다.(confirm)’**고 표현한다.
    
    ```swift
    protocal Runnable {
    	var x: Int { get set }
    	func run() 
    }
    
    class Man: Runnable {    //채택, adopt
    	var x: Int = 1         //준수, confirm
    	func run() {           //준수, confirm
    		print("달린다~")
    	}
    }
    
    ```

## 프로토콜 요구사항
### 1. Property 요구
프로토콜은 자신을 채택한 타입이 어떤 프로퍼티를 구현해야 하는지 요구할 수 있다.   
(ex. 프로토콜을 채택하면 프로토콜에 있는 변수를 채택한 곳에서 구현해야한다.)   
```Swift
protocol SomeProtocl {
    var settableProperty: String { get set }
    var notNeedToBeSettableProperty: String { get }
}

protocol SomeProtocl {
    static var settableProperty: String { get set }
    static var notNeedToBeSettableProperty: String { get }
}
```
**Property 요구사항은 `항상 var키워드`를 사용한 변수 프로퍼티로 정의합니다.**
Read & Write 모두 가능한 프로퍼티는 `{ get set }`이라고 명시.
Read만 가능한 프로퍼티는 `{ get }`이라고 명시.

### 2. Method 요구
프로토콜이 요구할 메서드는 프로토콜 정의에서 작성한다.  
다만 메서드의 실제 구현부인 `중괄호({})부분은 제외`하고 `메서드의 이름, 매개변수, 반환타입 등만 작성`하여 가변 매개변수도 허용한다. 
프로토콜의 메서드 요구에서는 매개변수 기본값을 지정할 수 없다.  
타입 메서드를 요구할 때는 타입 프로퍼티 요구과 마찬가지로 앞에 `static` 키워드를 명시한다.
```Swift
// 무언가를 수신받을 수 있는 기능
protocol Receiveable {
    func received(data: Any, from: Sendable)
}

// 무언가를 발신할 수 있는 기능
protocol Sendable {
    var from: Sendalbe { get }
    var to: Receiveable? { get }

    func send(data: Any)

    static func isSendableInstatnce(_ instance: Any) -> Bool
}
```

```Swift
// 수신, 발신이 가능한 Message 클래스
class Message: Sendalbe, Receiveable {
    // 발신은 가능한 객체
    // 즉 Sendable 프로토콜을 준수하는 타입의 인스턴스여야 한다.
    var from: Sendable { return self }

    // 상대방은 수신 가능한 객체
    // 즉 Receiveable 프로토콜을 준수하는 타입의 인스턴스여야 한다.
    var to: Receiveable?

    // 메세지를 발신합니다.
    func send(data: Any) {
        guard let receiver: Receiveable = self.to else {
            print("Message has no receiver")
            return
        }
        // 수신 가능한 인스턴스의 received 메서드를 호출합니다.
        receiver.received(data: data, from: self.from)
    }

    // 메세지를 수신합니다.
    func received(data: data, from: self.from) {
        print("Message received \(data) from \(from)")
    }

    // class 메서드이므로 상속이 가능합니다.
    class func is SendableInstance(_ instance: Any) -> Bool {
        if let sendableInstance: Sendable = instance as? Sendable {
            return sendableInstance.to != nil
        }
        return false
    }
}
```

```Swift
// 수신, 발신이 가능한 Mail 클래스
class Mail: Sendable, Receiveable {
    var from: Sendable { return self }
    var to: Receiveable?

    func send(data:Any) {
        guard let receiver: Receiveable = self.to else {
            print("Mail has no receiver")
            return
        }
        receiver.received(data: data, from: self.from)
    }

    func received(data: Any, from: Sendable) {
        print("Mail received \(data) from \(from)")
    }

    // static 메서드이므로 상속이 불가능합니다.
    static func isSendableInstance(_ instance: Any) -> Bool {
        if let sendalbeInstance: Sendable = instance as? Sendalbe {
            return sendableInstance.to != nil
        }
        return false
    }
}
```

```Swift
// 두 Message 인스턴스를 생성한다.
let myPhoneMessage: Message = Message()
let yourPhoneMessage: Message = Message()

// 아직 수신받을 인스턴스가 없다.
myPhoneMessage.send(data: "Hello")      // Message has no receiver

// Message 인스턴스는 발신과 수신이 모두 가능하므로 메시지를 주고 받을 수 있다.
myPhoneMessage.to - yourPhoneMessage
myPhoneMessage.send(data: "Hello")      // Message received Hello from Message

// 두 Mail 인스턴스를 생성한다.
let myMail: Mail = Mail()
let yourMail: Mail = Mail()

myMail.send(data: "Hi")         // Mail has no receiver

// Mail과 Message 모두 Sendalbe과 Receiveable 프로토콜을 준수하므로 서로 주고받을 수 있다.
myMail.to = yourMail
myMail.send(data: "Hi")         // Mail received Hi from Mail

myMail.to = myPhoneMessage
myMail.send(data: "Bye")        // Message received Bye from Mail

// String은 Sendable 프로토콜을 준수하지 않는다.
Message.isSendableInstance("Hello")         // false

// Mail과 Message는 Sendable 프로토콜을 준수한다.
Message.isSendalbeInstance(myPhoneMessage)  // true

// yourPhoneMessage는 to 프로퍼티가 설정되지 않아서 보낼 수 없는 상태이다.
Message.isSendableInstance(yourPhoneMessage)    // false
Mail.isSendableInstance(myPhoneMessage)         // true
Mail.isSendableInstance(myMail)                 // true
```

### 3. 가변(mutating) 메서드 요구
가끔 메서드가 인스턴스 내부의 값을 변경할 필요가 있다.  
값 타입(struct & enum)의 인스턴스 메서드에서 `자신 내부의 값을 변경하고자 할 때는 mutating 키워드`를 적어 메서드에서 인스턴스 내부의 값을 변경한다는 것을 확실히 해준다.
```Swift
protocol Resettable {
    mutating func reset()
}
```

### 4. 이니셜라이저 요구
특정한 이니셜라이저를 요구할 수도 있다. 메서드 요구와 마찬가지로 이니셜라이저를 `정의하지만 구현을 하지 않는다.`
```Swift
protocol Named {
    var name: String { get }

    init(name: String)
}
```

## 위임(Delegation)을 위한 프로토콜
- Delegation은 클래스나 구조체가 자신의 책임이나 임무를 다른 타입의 인스턴스에게 위임하는 디자인 패턴이다.
- 책무를 위임하기 위해 정의한 프로토콜을 준수하는 타입은 자신에게 위임될 일정 책무를 할 수 있다는 것을 보장한다.    
  그렇기 때문에 다른 인스턴스에게 자신이 해야할 일을 믿고 맡길 수 있다.
- Delegation은 사용자의 특정 행동에 반응하기 위해 사용되기도 하며, 비동기 처리에도 많이 사용한다.