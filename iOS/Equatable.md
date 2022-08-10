# Equatable
Comparable을 먼저 접하였는데 학습 과정에서 Comparable 프로토콜은 먼저 Equtable을 채택되어있다는 사실을 알게되어 학습하게되었다.

### <span style="color:yellow">Equatable이란?</span>
Equatable은 타입끼리 비교(==)연산을 하기 위해서 필수적으로 구현해야하는 프로토콜이다.   
```Swift
publice protocol Equatable {
    static func == (lhs: Self, rhs: Self) -> Bool
}
```

## <span style="color:green"> Struct, Class, Enum 인스턴스끼리는 왜 비교할 수 없을까
기존에 코드를 작성하면서 '==(비교연산자)'를 무의식적으로 사용하여 원하는 Bool(true, false)값을 얻을 수 있었지만   
구조체 또는 클래스 인스턴스를 '=='의 비교연산자를 사용하려면 아래 에러메세지를 볼 수 있게된다.   
> Binary operator '==' cannot be applied to two ~~~ operands

### 에러메세지가 나타난 이유
**Int, Double, String이란 자료형은 가장 기본적인 자료형으로, 컴파일러가 Equtable이란 프로토콜을**   
**이미 모두 채택해놓아 자동으로 구현해주기 때문이었다.**   

## Struct, Class, Enum 에서 비교 연산을 쓰는 방법
### Struct
```Swift
struct Drink: Equtable {
    var name: water
    var price: 500
}
let Drink1 = Drink.init(name: milk, price: 700)
let Drink2 = Drink.init()

Drink1 == Drink2        // false
```
위와 같이 Drink 구조체에 프로토콜을 채택하면 Drink 인스턴스끼리 비교가 가능해진다.

#### 프로토콜 내부 메서드를 구현하지 않았는데 사용가능한가??
**열거형 내 모든 타입이 기본 타입(Int, String, 등)이라면 직접 메서드를 구현해주지 않아도**   
<span style="color:red"> Equatable을 채택하는 것만으로도 사용 가능하다!   

### Class
<span style="color:yellow"> 클래스의 경우 Equatable을 채택하는 것만으로 자동으로 구현해주지 않는다!   
따라서 직접 프로토콜 메서드를 구현해야한다.
```Swift
class Drink {
    var name: ""
    var price: 0

    static func == (lhs: Drink, rhs: Drink) -> Bool {
        return lhs.name == rhs.name && lhs.price == rhs.price
    }
}
let Drink1 = Drink.init()
let Drink2 = Drink.init()
Drink2.price = 700

Drink1 == Drink2        // false
```
### Enum
#### 연관값이 있는 경우
Equatable을 채택만 해줘도 자동으로 구현이 된다.
```Swift
enum Device: Equatable {
    case noteBook(name: String)
}
let device = Device.noteBook(name: "MacBookAir")
let device2 = Device.noteBook(name: "MacBookPro")
 
device == device2   // false
```
#### 연관값이 없는 경우
**Equatable을 채택하지 않아도 자동으로 구현된다.**
```Swift
enum Device {
    case noteBook
}
let device = Device.noteBook
let device2 = Device.noteBook
 
device == device2   // true
```
<span style="color:yellow">글자색 테스트</span>

### 🌐 참고사이트   
[Swift) Equatable에 대해 알아보자](https://babbab2.tistory.com/148?category=828998)