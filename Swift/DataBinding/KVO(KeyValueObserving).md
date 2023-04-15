# KVO (Key - Value Observing)
객체의 프로퍼티의 변경사항을 다른 객체에 알리기 위해 사용하는 코코아 프로그래밍 패턴.   
Model과 View와 같이 논리적으로 분리된 파트간의 변경사항을 전달하는데 유용하다.  
📍 `NSObject`를 상속한 클래스에서만 KVO를 사용할 수 있다.

## Pros and Cons
### Pros 👍🏻
- 두 객체 사이의 정보를 맞춰주는 것이 쉽다
- New / old value를 쉽게 얻을 수 있다.
- KeyPath로 옵저빙하기 때문에 nested objects도 옵저빙이 가능하다.
### Cons 👎🏻
- NSobject를 상속받는 객체에서만 사용이 가능하다.
- dealloc될 때 옵저버를 지워줘야 한다.
- 많은 value를 감지할 때는 많은 조건문이 필요하다.

## Observing을 위한 Setup
```Swift
class Address {
    var town: String

    init(town: String) {
        self.town = town
    }
}
```
위와 같이 클래스를 선언했을 떄 기본적인 형태이다.   

여기서 town이 변경하는 걸 다른 객체에게 알리고 싶다는 로직이 필요할 때 2가지 작업 방법이 있다.
1. NSObject 상속
   - `NSObejct`를 상속한 클래스에서만 KVO를 사용할 수 있기 때문   
   -> 상속이 필요함으로 class에서만 사용 가능하다.
2. Observe 하려는 프로퍼티에 `@objc` attribute와 dynamic modifier를 추가해해야한다.
    ```Swift
    class Address: NSObject {
        @objc dynamic var town: String

        init(town: String) {
            self.town = town
        }
    }
    ```

---

## Observer 정의
내가 Observe하려는 프로퍼티가 변경되는지 확인해야하기 때문에 해당 관찰 역할을 수행할 Observer를 정의해야합니다.   
```Swift
var address = Address(town: "어쩌구")

address.observe(\.town, options: [.old, .new]) { (object, change) in
    print(change.oldValue, change.newValue)
}
```
여기서 (\.town)은 KeyPath를 사용합니다.

KeyPath를 사용하여 프로퍼티 KeyPath에 observer를 추가할 수 있다.
- 관찰자 클래스의 인스턴스는 하나 이상의 속성에 대한 변경사항에 대한 정보를 관리한다.
- 관찰자를 만들 때 관찰하려는 속성을 참조하는 키 경로로 메서드를 호출하여 관찰을 시작한다.

```Swift
var address = Address(town: "어쩌구")
address.observe(\.town, options: [.old, .new]) { (object, change) in
    print(change.oldValue, change.newValue) // Optional("어쩌구") Optional("바보")
}
address.town = "바보"
```
1. town을 `바보`로 바꾼다.
2. 프로퍼티에 변경사항이 생긴다.
3. Observer의 ChangeHandler가 호출된다.
4. handler내에서 oldValue와 newValue를 가져올 수 있다.

```Swift
address.observe(\.town, options: [.old, .new]) { (object, change) in
    print(change.oldValue, change.newValue) // ✔️ Optional("어쩌구") Optional("바보")
}

// 변경사항이 필요하지 않는 경우의 Option을 주었을 때
var address = Address(town: "어쩌구")
address.observe(\.town) { (object, change) in
    print(change.oldValue, change.newValue) // ✔️ nil nil
}
address.town = "바보"
```

### Reference Site
[[iOS/Swift] KVO(Key-value observing)](https://leeari95.tistory.com/50)   
[Key-Value Observing(KVO) in Swift](https://zeddios.tistory.com/1220)   