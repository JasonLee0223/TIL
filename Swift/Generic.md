# Generic
제네릭을 이용해 코드를 구현하면 어떤 타입에도 유연하게 대응할 수 있다.   
장점 `재사용이 용이`하다, 중복을 줄일 수 있어 `깔끔하고 추상적인 표현이 가능`하다.   
제네릭이 필요한 타입 또는 메서드의 이름 뒤의 홀화살괄호 기호(<>)사에이 제네릭을 위한 타입 매개변수를 써주어 제네릭을 사용함을 표시한다.   
```
제네릭을 사용하고자 하는 타입 이름 <타입 매개변수>

제네릭을 사용하고자 하는 함수 이름 <타입 매개변수> (함수의 매개변수...)
```
위 형식을 봐서는 이해가 안가니 예시를 통해 비교해보자!

```Swift
// 전위 연산자 구현과 사용
prefix func ** (value: Int) -> Int {
    return value * value
}
let minusFice: Int = -5
let sqrtMinusFive: Int = **minusFive
print(sqrtMinusFive) // 25

// Protocol과 Generic을 이용한 전위 연산자 구현과 사용
prefix operator **

// value 파라미터는 제네릭을 사용하여 앞에서 Int형만 가능했지만
// UInt 타입에 대해서도 해당 연산자를 사용할 수 있게 되었다.
prefix func ** <T: BinaryInteger> (value: T) -> T {
    return value * value
}
let minusFice: Int = -5
let five: UInt = 5

let sqrtMinusFive: Int = **minusFive    // 25
let sqrtFive: UInt = **five             // 25
```
BinaryInteger 프로토콜에 해당하는 값이면 해당 연산자를 사용할 수 있도록   
(제네릭을 이용하여) 구현해줄 수 있다.   

## 1️⃣ 제네릭 함수
같은 타입인 두 변수의 값을 교환한다는 목적을 타입에 상관없이 할 수 있도록   
단 하나의 함수로 구현할 수 있다.   
아래 예시를 확인해보자.   
```Swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temporaryA: T = a
    a = b
    b = temporaryA
}
swapTwoValues(&numberOne, &numberTwo)   // 10, 5
swapTwoValues(&stringOne, &stringTwo)   // "B, A"
swapTwoValues(&anyOne, &anyTwo)         // "Two", 1

swapTwoValues(&numberOne, &stringTOno)  // Error!! - 같은 타입끼리만 교환 가능
```
제네릭 함수는 실제 타입 이름(Int, String 등)을 써주는 대신에   
`플레이스홀더(위 함수에서는 T)를 사용`한다.
**`플레이스홀더(T)는 타입의 종류를 알려주지 않지만 말 그대로 어떤 타입이라는 것은 알려준다!`**   

즉, 매개변수로 플레이스홀더 타입이 T인 두 매개면수가 있으므로,   
두 매개변수는 같은 타입이라는 정도는 알 수 있다.   
`T의 실제 타입은 함수가 호출되는 그 순간 결정된다.`   

플레이스홀더 타입 T는 타입 매개변수의 한 예로 들 수 있다.   
타입 매개변수는 플레이스홀더 타입의 이름을 지정하고 명시하는 역할을 하며,   
함수의 이름 뒤 홀화살괄호 기호(<>) 안쪽에 위치한다. `<T>`처럼 말이다.   

하나의 타입 매개변수를 갖지 않고 여러 개의 타입 매개변수를 갖고 싶다면   
홀화살괄호 기호 안쪽에 쉼표로 분리한 여러 개의 타입 매개변수를 지정해줄 수 있다.   
<T, U, V>처럼 말이다.   

---
## 2️⃣ 제네릭 타입
제네릭 타입을 구현하면 사용자 정의 타입인 구조체, 클래스, 열거형 등이 어떤 타입과도 연관되어 동작할 수 있다.   
Stack이라는 제네릭 컬렉션 타입을 어떻게 만들어 가는지 살펴보자.   
스택은 컬렉션의 끝 부분에서만 요소를 추가하고 삭제할 수 있다.   
추가: 푸시(Pust), 삭제: 팝(Pop)이라 칭한다.   
```Swift
// Generic을 사용하지 않은 IntStack 구조체 타입
struct IntStack {
    var items = [Int]
    mutating func push(_ item: Int) {
        items.append(item)
    }
    mutating func pop() -> Int {
        return items.removeLast()
    }
}
var integerStack: IntStack = IntStack()
```
이제 모든 타입을 대상으로 동작할 수 있는 스택 기능을 구현해보려고한다.   
우리는 스택의 요소로 한 타입을 지정해주면 그 타입으로 계속 스택이 동작하길 바라며,   
처음 지정해주는 타입은 스택을 사용하고자 하는 사람 마음대로 지정할 수 있도록 제네릭을 사용한다는 것이다.

```Swift
// Generic을 사용한 Stack 구조체 타입
struct Stack<Element> {
    var items = [Element]
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
}
var doubleStack: Stack<Double> = Stack<Double>()
doubleStack.push(1.0)       // [1.0]
doubleStack.push(2.0)       // [1.0, 2.0]
doubleStack.pop()           // [1.0]

var stringStack: Stack<String> = Stack<String>()
stringStack.push("1")       // ["1"]
stringStack.push("2")       // ["1", "2"]
stringStack.pop()           // ["1"]

var anyStack: Stack<Any> = Stack<Any>()
anyStack.push(1.0)          // [1.0]
anyStack.push("2")          // [1.0, "2"]
anyStack.push(3)            // [1.0, "2", 3]
anyStack.pop()              // [1.0, "2"]
```
위 예제에서는 Element라는 `타입 매개변수`를 사용했다.   
> ⭐️ Stack의 인스턴스를 생성할 때 실제로 Element 대신 어떤 타입을 사용할지 명시해주는 방법은 `Stack<Type>`처럼 선언해주면 된다.   
그래서 Stack<Double>이라고 타입을 선언해준 doubleStack 인스턴스는 Element의 타입으로 Double을 사용한다.   
동일하게 Element의 타입을 정해주면 그 타입에만 동작하도록 제한할 수 있어 더욱 안전하고 의도한 대로 기능을 사용하도록 유도할 수 있다.

---
## 3️⃣ 타입 제약
제네릭 함수가 처리해야 할 기능이 특정 타입에 한정되어야만 처리할 수 있다던가,   
제네릭 타입을 특정 프로토콜을 따르는 타입만 사용할 수 있도록 제약을 두어야하는 상황이 발생할 수 있다.    
타입 제약은 **`타입 매개변수가 가져야 할 제약사항을 지정할 수 있는 방법`** 이다.   
**`타입 제약(Type Constraints)은 클래스 타입 또는 프로토콜로`** 만 줄 수 있다.   

예를 들어 제네릭 타입인 Dictionary의 키는 Hashable 프로토콜을 준수하는 타입만 사용할 수 있다.   
```Swift
// Dictionary 타입 정의
public struct Dictionary<Key : Hashable, Value>: Collection,
    ExpressibleByDictionaryLiteral { \* ... */ }
```
즉, Key로 사용할 수 있는 타입은 Hashable 프로토콜을 준수하는 타입이어야 한다는 것이다.   

여러 가지의 제약을 추가하고 싶다면 콤마로 구분해주는 것이 아니라 `where절`을 사용할 수 있다.   
```Swift
// 제네릭 타입 제약 추가
func swapTwoValues<T: BinaryInteger>(_ a: inout T, _ b: inout T) where T: FloatingPoint {
    // 함수 구현
}
```
위 코드를 보면 `where절을 사용`하여 FloatingPoint 프로토콜도 준수하는 타입만 사용할 수 있다.   

```Swift
// substractTwoValue 함수의 잘못된 구현
func substractTwoValue<T>(_ a: T, _ b: T) -> T {
    return a - b
}

// substractTwoValue 함수의 구현
func substractTwoValue<T: BinaryInteger>(_ a: T, _ b: T) -> T {
    return a - b
}
```
BinaryInteger 프로토콜을 준수하는 타입으로 한정해두니 뺄셈 연산이 가능하게 되었다.   
타입 제약은 함수 내부에서 실행해야 할 연산에 따라 적절한 타입을 전달받을 수 있도록 제약을 둘 수 있다.   

> 스위프트의 표준 라이브러리에 정의되어 있는 프로토콜 중 타입 제약에 자주 사용할 만한 프로토콜에는   
> Hashable, Equatable, Comparable, Indexable, IteratorProtocol, Error, Colleciton, CustomStringConvertible 등이 있다.

---
## 4️⃣ 프로토콜의 연관 타입 🤯
프로토콜을 정의할 때 `연관 타입(Associated Type)`을 함께 정의하면 유용할 때가 있다.   
제네릭에서는 어떤 타입이 들어올 지 모를 때, 타입 매개변수를 통해 '종류는 알 수 없지만, 어떤 타입이 여기에 쓰일 것이다'라고 표현해주었다면   
**`연관 타입은 타입 매개변수의 그 역할을 프로토콜에서 수행할 수 있도록 만들어진 기능`** 이다.

위 내용을 바탕으로 코드로 표현한다면
```Swift
class SomeType<T: Equtable> {
    var someProperty = T

    func someMethod<T>() {

    }
}
```
위와 같이 어떠한 타입이던 Equtable한 프로토콜은 받을 수 있다는 제네릭의 표현방법이 있다는 것이다. (앞서 확인한 내용)
그렇다면 `연관 타입`은 어떻게 쓰인다는 것일까?
```Swift
protocol Container {
    associatedtype ItemType

    var count: Int { get }

    mutating func append(_ item: ItemType)

    subscript(i: Int) -> ItemType { get }
}
```
위와 같이 Container 프로토콜안에서 `associatedtype`이라는 `ItemType`을 명시해준다면 (제네릭의 T와 같다)   
존재하지 않는 타입인 ItemType을 타입 이름으로 활용할 수 있다는 말이다.

다시 한 번 정리하면     
제네릭의 타입 매개변수(T)와 유사한 기능으로,    
프로토콜 정의 내부에서 사용할 타입이 **`'그 어떤 것이어도 상관없지만, 하나의 타입임은 분명하다.'`** 라는 의미이다.

그럼 실질적인 예제를 확인해보자.
```Swift
struct IntStack: Container {
    
    var items = [Int]()
    
    mutating func push(_ item: Int) {
        items.append(item)
    }
    
    /// Container 프로토콜 준수를 위한 구현
    mutating func append(_ item: Int) {
        self.push(item)
    }
    
    var count: Int {
        return items.count
    }
    
    subscript(i: Int) -> Int {
        return items[i]
    }
}
```
위의 경우 연관 타입 ItemType 대신에 실제 타입인 Int 타입으로 구현해주었고, 프로토콜의 요구사항을 충족하고 있다.
왜냐하면 프로토콜에서 ItemType이라는 연관 타입만 정의했을 뿐, 특정 타입을 지정하지 않았기 때문이다.
하지만 이렇게만 적으면 아래의 에러를 확인할 수 있을 것이다.
```
Type 'IntStack' does not confirm to protocol 'Container'
```
이 부분은 ItemType 대신 Int 타입을 사용하여 구현했을 뿐이기 때문이고, ItemType을 어떤 타입으로 사용할 지 조금 더 명확히 해주고 싶다면   
IntStack 구조체 구현부에 `typealias ItmeType = Int`라고 타입 별칭을 지정해줄 수 있다.
```Swift
struct IntStack: Container {
    typealias ItemType = Int
    
    var items = [ItemType]()
    
    mutating func push(_ item: ItemType) {
        items.append(item)
    }
    
    mutating func pop() -> ItemType {
        return items.removeLast()
    }
    
    /// Container 프로토콜 준수를 위한 구현
    mutating func append(_ item: ItemType) {
        self.push(item)
    }
    
    var count: Int {
        return items.count
    }
    
    subscript(i: Int) -> ItemType {
        return items[i]
    }
}
```
### 🔥 좀 더 나아가 봅시다!! 
프로토콜의 연관 타입에 대응하여 실제 타입을 사용할 수도 있지만,   
제네릭 타입에서는 연관 타입과 타입 매개변수를 대응시킬 수 있습니다.
```Swift
struct Stack<Element>: Container {
    /// 기존 Stack<Element> 구조체 구현
    
    var items = [Element]()
    
    mutating func push(_ item: Element) {
        items.append(item)
    }
    
    mutating func pop() -> Element {
        return items.removeLast()
    }
    
    /// Container 프로토콜 준수를 위한 구현
    mutating func append(_ item: Element) {
        self.push(item)
    }
    
    var count: Int {
        return items.count
    }
    
    subscript(i: Int) -> Element {
        return items[i]
    }
}
```
Container 프로토콜을 준수하기 위해 **`Stack 구조처에서 ItemType이라는 연관 타입 대신에`**   
`Element`라는 타입 매개변수를 사용했음을 볼 수 있습니다. 그럼에도 프로토콜을 완벽히 준수하게됩니다.