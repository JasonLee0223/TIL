# Protocol Default Implimentations
특정 프로토콜을 정의하고 여러 타입에서 이 프로토콜을 준수하게 만들어 타입마다 구현해야한다면...??   
얼마나 많은 코드를 중복 사용해야 하며, 유지보수는 얼마나 힘들어질지 생각만해도 머리가 아플겁니다...   
이때 빛을 발하는 것이 바로 `extenstion`과 `Protocol`의 결합입니다.   

## 🅰️ 익스텐션을 통한 프로토콜의 실제 구현
```Swift
protocol Receiveable {
    func received(data: Any, from: Sendable)
}

extension Receiveable {
    // 메세지를 수신합니다.
    func received(data: Any, from: Sendable) {
        print("\(self) received \(data) from \(from)")
    }
}


protocol Sendable {
    var from: Sendable { get }
    var to: Receiveable? { get }
    
    func send(data: Any)
    
    static func isSendableInstance(_ instance: Any) -> Bool
}

extension Sendable {
    // 발신은 발신 가능한 객체, 즉 Sendable 프로토콜을 준수하는 타입의 인스턴스여야 합니다.
    var from: Sendable {
        return self
    }
    
    // 메세지를 발신합니다.
    func send(data: Any) {
        guard let receiver: Receiveable = self.to else {
            print("Message has no receiver")
            return
        }
        // 수신 가능한 인스턴스의 received 메서드를 호출합니다.
        receiver.received(data: data, from: self.from)
    }
    
    static func isSendableInstance(_ instance: Any) -> Bool {
        if let sendableInstance: Sendable = instance as? Sendable {
            return sendableInstance.to != nil
        }
        return false
    }
}
```
```Swift
// 수신, 발신이 가능한 Message 클래스
class Message: Sendable, Receiveable {
    var to: Receiveable?
}

// 수신, 발신이 가능한 Mail 클래스
class Mail: Sendable, Receiveable {
    var to: Receiveable?
}

// 두 Message 인스턴스를 생성합니다.
let myPhoneMessage: Message = Message()
let yourPhoneMessage: Message = Message()

// 두 Mail 인스턴스를 생성합니다.
let myMail: Mail = Mail()
let yourMail: Mail = Mail()

// 아직 수신받을 인스턴스가 없습니다.
myPhoneMessage.send(data: "Hello")      // Message has no receiver

// Message 인스턴스는 발신과 수신이 모두 가능하므로 메세지를 주고 받을 수 있습니다.
myPhoneMessage.to = yourPhoneMessage
myPhoneMessage.send(data: "Hello")      // Message received Hello from Message

myMail.send(data: "Hi")

// Message와 Mail 모두 Sendable, Receiveable 프로토콜을 준수하므로 서로 주고 받을 수 있습니다.
myMail.to = yourMail
myMail.send(data: "Hi")                 // Mail received Hi from Mail

myMail.to = myPhoneMessage
myMail.send(data: "Bye")                // Message received Bye from Mail

// String은 Sendable 프로토콜을 준수하지 않습니다.
Message.isSendableInstance("Hello")         // false

// Message와 Mail은 Sendable 프로토콜을 준수합니다.
Message.isSendableInstance(myPhoneMessage)  // true
```