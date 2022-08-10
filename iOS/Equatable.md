# Equatable
Comparable을 먼저 접하였는데 학습 과정에서 Comparable 프로토콜은 먼저 Equtable을 채택되어있다는 사실을 알게되어 학습하게되었다.

### <span style='background-color: #fff5b1'> Equatable이란?</span>
Equatable은 타입끼리 비교(==)연산을 하기 위해서 필수적으로 구현해야하는 프로토콜이다.   
```Swift
publice protocol Equatable {
    static func == (lhs: Self, rhs: Self) -> Bool
}
```

## Struct, Class, Enum 인스턴스끼리는 왜 비교할 수 없을까
기존에 코드를 작성하면서 '==(비교연산자)'를 무의식적으로 사용하여 원하는 Bool(true, false)값을 얻을 수 있었지만   
구조체 또는 클래스 인스턴스를 '=='의 비교연산자를 사용하려면 아래 에러메세지를 볼 수 있게된다.   
> Binary operator '==' cannot be applied to two ~~~ operands

### 에러메세지가 나타난 이유
**Int, Double, String이란 자료형은 가장 기본적인 자료형으로, 컴파일러가 Equtable이란 프로토콜을**   
**이미 모두 채택해놓아 자동으로 구현해주기 때문이었다.**





### 🌐 참고사이트   
[Swift) Equatable에 대해 알아보자](https://babbab2.tistory.com/148?category=828998)