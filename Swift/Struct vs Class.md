# Struct vs Class
Struct와 Class의 차이를 학습해서 제대로 이해해보자!!!

## 1️⃣ 차이점1: 초기화
### 📍 인스턴스의 프로퍼티에 값이 있다는 것이 보장되어야 한다.
> Note   
> 인스턴스: 메모리에 차지하는 것을 말한다.
```Swift
class StudentA { // error: Class 'PersonA' has no initializers
    var name: String
    var age: Int
}

struct StudentB {
    var name: String
    var age: Int
}
```
- 구조체: **`memberWise`라는 기능을 제공하기 때문에** 클래스와 같이 초기화 메서드가 없어도 에러가 발생하지 않는다.
- 클래스: 해당 클래스는 initializer를 가지고 있지 않다고 에러를 확인 할 수 있다.   
  StudentA는 정의된 프로퍼티에 초기화가 되어 있지 않아서 초기화 메서드를 따로 만들어주어야 한다.

### 🤔 그럼 왜 struct에만 MemberWise를 제공해줄까??
- struct는 상속이 불가능하기 때문에 해당 struct에서 init을 꼭 필요로 하게된다.   
  하여, Swift 자체에서 자동화된 기능을 제공하게되었다.   
  하지만 class의 경우 상속이 가능하므로, 설계상 해당 클래스가 서브 클래스에서만 초기화되어야할 필요성이 있을 수 있다.
- 즉, 위에서 언급한대로 간단히 말해서는 **`상속`** 의 문제이고,   
  조금 더 정확히 표현하면 **`'자동화된 초기화가 존재할 경우 상속의 상황에서 발생할 수 있는 오류를 개발자가 직접 변경하는 작업이 더 번거롭기 때문에'`**라고 정의할 수 있다고한다!

### 📍 deinit
Deinitializer는 클래스에서만 제공되는 메서드이다.   
클래스에서만 제공되는 이유는 메모리 위에서 관리되는 방식이 구조체와 클래스가 다르기 때문!

## 2️⃣ 차이점2: 상속
- Struct, Enum는 상속 ❌
- Class는 상속 ⭕️

## 3️⃣ 차이점3: mutating
구조체에서는 자신의 프로퍼티 값을 변경하는 메서드 앞에는 `Mutating` 키워드를 붙여주어야 컴파일 에러가 발생하지 않는다.

## 4️⃣ 차이점4: Value Type과 Reference Type
### 🅰️ Value Type (Struct, Enum)
- `Call by Value` (할당 또는 파라미터 전달 시 value copy가 일어난다.)
- 값을 **`복사`** 하여 전달
- Stack Memory 영역에 할당한다. (속도가 빠름)
  - `하나의 명령어(Pop, Push)`로 메모리를 할당, 해제할 수 있다.
  - Thread들이 각각 독립적인 Stack공간을 가지고 있기 때문에 상호 배제를 위한 자원이 필요하지 않다. (즉, T`hread로부터 안전하다.`)
  - Scope Based Lifetime: 컴파일 타임에 compiler가 `언제 메모리를 할당 / 해제`할 지 정확히 알고있다.
  - data locality: CPU Cash Hit Ratio가 높다.
### 🅱️ Reference Type (Class)
- `Call by Reference` (객체를 가리키고 있는 메모리 주소값만 복사된다.)
- 값의 **`메모리 위치를 참조`** 하여 전달
- Heap Memory 영역에 할당한다. (속도가 느림)
  - 하나의 명령어로 할당, 해제가 이루어지지 않는다 -> Reference Counting 때문!
  - Runtime(런타임)에 직접 Allocate하여 Reference Counting을 통해 DeAllocate가 필요하다.   
  - Memory fragmentation 등의 Overhead(오버헤드)가 존재한다.
  - ARC(Automatic Reference Count)를 사용하여 메모리 관리를 한다.
  - Type Casting을 통해 RunTime에서 클래스 인스턴스의 타입을 확인할 수 있다.
> Note   
> Overhead(오버헤드)란?   
> 프로그램의 실행흐름에서 나타나는 현상 중 하나로, 실행흐름 동중에 동떨어진 위치의 코드를 실행시켜야할 때, 
> 추가적으로 시간, 메모리, 자원이 사용되는 현상   
> 정리하면 `특정 기능을 수행하는데 드는 간접적인 시간, 메모리 등 자원을 말한다.`

## 🤯 Memory Model
<img src = "https://user-images.githubusercontent.com/92699723/209107428-98fce87d-86a8-4724-a814-753cbbdb319d.png" width = "300" height = "300">

<img src = "https://user-images.githubusercontent.com/92699723/209107441-29f00aa5-6280-4c13-8363-b890d22b6c6f.jpeg">   

- OS에 Process가 생길 때마다 가상 메모리에 영역이 생긴다.   
- 동적, Runtime 다 같은 맥락으로 실행했을 때라는 의미를 말한다.   
- 변수, 함수를 만들면 `Stack`에 쌓이고 Stack이 계속 쌓이다 보면 어떻게 될까요??
  충돌이 나는 시점이 생기고 넘어가면 안되는 시점에서 넘어가면 `💥Stack OverFlow`났다고 한다.   

## Value Type의 Copy-on-assignment, Copy-on-write
Value Type을 다른 변수에 할당하면 복사를 하게 된다.   
즉, 새로운 메모리 공간에 같은 값을 복사하게 되는데, 이를 `Copy-on-assignment`라고 한다.   
이와 다르게, `Copy-on-write`는 다른 변수에 할당하면 일단은 메모리를 할당하지 않고 같은 곳을 보게된다.   
그러다 `해당 값을 변경할 때` 실제로 메모리에 값을 복사하고 변경하게된다.   
이는 메모리를 최적화해주기 위함이며 `Int, Double, String, Array, Set, Dictionary`에서만 사용하고 있다.


## 구조체는 언제 사용될까?
- 의미있는 값을 사용하기 위해서
  - 상속이 필요하지 않고 모델의 사이즈가 그리 크지 않다면 사용
- 연관된 몇몇의 값들을 모아서 하나의 데이터타입으로 표현하고 싶을 때
- Apple Framework에서 프로그래밍을 할 때에는 주로 클래스를 많이 사용
- JSON의 필드와 1:1 mapping되는 간단한 모델이 필요하다면 사용

### 🌐 Reference Site
- [Choosing Between Structures and Classes](https://developer.apple.com/documentation/swift/choosing-between-structures-and-classes)   
- [Swift struct vs. class 차이점 비교 분석](https://www.letmecompile.com/swift-struct-vs-class-%EC%B0%A8%EC%9D%B4%EC%A0%90-%EB%B9%84%EA%B5%90-%EB%B6%84%EC%84%9D/)
- [[Swift] Class와 Struct의 차이점?](https://icksw.tistory.com/256)   
- [[스위프트(Swift) 프로그래밍] - 왜 Swift의 클래스(Class)에는 멤버와이즈 초기화(Memberwise Init)가 없을까?](https://jayb-log.tistory.com/258)   
- [오버헤드(overhead)란?](https://donggu1105.tistory.com/175)