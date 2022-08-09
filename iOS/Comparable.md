# Comparable

보통 사용하는 비교 연산인 '>', '<', '>=', '<=' 이것들을 사용하기 위해서 Comparable Protocol을 준수하고 있어야한다.

```Swift
let num1 = 10
let num2 = 20

num1 > num2     // false
num1 <= num2    // true
```
위와 같이 **기본자료형은 자동으로 컴파일러가 Comparable을 준수**하여 따로 프로토콜을 채택하지 않고 잘 사용해왔었던 것이었다!!

String의 경우도 기본 자료형이라 Comparable을 자동채택하고 있어 당연하듯이 사용하고 있었지만   
**유니코드 값을 기준**으로 구분하였던 것이었다.

## Comparable Protocol
```Swift
public protocol Comparable: Equatable {
    static func < (lhs: Self, rhs: Self) -> Bool
    static func <= (lhs: Self, rhs: Self) -> Bool
    static func >= (lhs: Self, rhs: Self) -> Bool
    static func > (lhs: Self, rhs: Self) -> Bool
}
```
**Comparable을 직접 채택하고 필요시 구현도 해주어야**우리가 직접 만드는 Struct/Class/enum을 대소 비교 연산을 사용할 수 있게된다.

### 🌐 참고사이트   
[Swift) Comparable에 대해 알아보자](https://babbab2.tistory.com/150)   
[Swift의 기본 프로토콜 세 가지: Equatable, Comparable, Printable](http://seorenn.blogspot.com/2014/08/swift-equatable-comparable-printable.html)   
[Apple-Developer[Comparable]](https://developer.apple.com/documentation/swift/comparable)