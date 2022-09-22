# Subscript

클래스, 구조체, 열거형에서 script(사전적의미: 대본)를 정의해서 사용할 수 있다.   
Subscript란 Collection, List, Sequence 등 집합의 특정 멤버 Element에 간단하게 접근할 수 있는 문법이다.   
즉, sequence의 멤버 요소에 접근하기 위한 바로가기 첨자로, 단일 타입에 여러 subscript를 정의할 수 있다.   

대표적으로, 배열과 딕셔너리를 사용하면서 각 멤버 요소의 값에 접근할 때
```Swift
// Array
let nums: [Int] = [1, 2, 3, 4]

nums[0]         // 1
nums[1]         // 2

// Dictionary
let dictionary: [String:Int] = ["one":1, "two":2]

dictionary["one"]       // 1
dictionary["two"]       // 2
```
위와 같이 `[ ]` 대괄호 안에 찾고자하는 index를 넣어줘서 멤버 요소에 접근하는데
이런 방식을 **Subscript**라고 표현된다.

```Swift
// Array의 [ ]의 정의
@inlinalbe public subscript(index: Int) -> Element

// Dictionary의 [ ]의 정의
@inlinable public subscript(key: Key) -> Value?
```
위 정의된 내용으로 `Array subscript는 parameter로 Int형을 index로 받고, 해당 index에 해당하는 Element를 반환하는 형태`라고 알 수 있게 된다.   
똑같이 `Dictionary subscript는 parameter로 Key를 받고, 해당 key에 해당하는 Value를 반환하는 형태`라고 볼 수 있다.   

## Subscript Syntax
Subscript 선언 문법은 인스턴스 메서드와 연산 프로퍼티를 선언하는 것과 비슷하다.   
다른 점은, `Subscript는 읽기-쓰기(Read-Write) 혹은 읽기전용(Read Only)만 가능하다는 점이다.`
```Swift
subscript(index: Int) -> Int {
    get {
        // 적절한 반환 값
    }
    set(newValue) {
        // 적절한 set 액션
    }
}
```

- subscript의 `set`에 대한 인자 값을 따로 지정하지 않는다면 기본 값으로 `newValue`를 사용한다.   
- Read Only로 선언하려면 `get`, `set`을 지우고 따로 지정하지 않으면 `get`으로 동작하게되서 Read Only로 선언된다.   
```Swift
subscript(index: Int) -> Int {
    // 적절한 반환 값   
}

// Example    
struct TimesTable {
let multiplier: Int

subscript(index: Int) -> Int {
    return multiplier * index
    }
}

let threeTimesTable = TimesTable(multiplier: 3)
print("\(threeTimesTable[6])")                  // 18
```
TimesTable 구조체의 multiplier를 3으로 설정하고 `threeTimesTable[6]`에서 6번째 값, 여기서는 `3 * 6`의 결과값이 출력된다.

- String도 배열처럼 [index]로 접근하고 싶을 때
```Swift
// 잘못된 예시
let accost = "Hello world"
accost[0]       // Error

// 올바른 에시
extension String {
    subscript(index: Int) -> String? {
        guard (0..<count).contains(index) else { return nil }
        
        let target = index(startIndex, offsetBy: index)
        return String(self[target])
    }
}

let accost = "Hello world"
accost[0]       // Optional("H")
accost[50]      // nil
```

## Subscript Usage
일반적인 예시는 위 코드를 참고하자.
```Swift
//Example
struct Stack {
    var stack: [Int] = [0, 1, 2, 3, 4, 5]

    subscript(index: Int) -> Int {
        get { return stack[index] }
        set { stack[index] = newValue}
    }
}
var stack: Stack = .init()
stack[0]        // getter 접근
stack[1] = 2    // setter 접근
```

### Subscript Options
- Subscript는 입력 인자의 숫자에 제한이 없고, 입력 인자의 타입과 반환 타입의 제한도 없다.
- **다만 In-Out Parameter나 기본 인자 값을 제공할 수는 없다.**
- 오버로딩(overloading)도 허용합니다.
  그래서 인자형, 반환형에 따라 원하는 수 만큼의 subscript를 선언할 수 있다.

## Type Subscript
오버라이딩이 불가하다면 `static` / 가능하다면 `class`로 선언해주면 Type Subscript가 되는 것이다.
```Swift
struct Stack {
    static var stack: [Int] = [0, 1, 2, 3]

    static subscript(index: Int) -> Int {
        return stack[index]
    }
}
Stack[0]    // 0
Stack[1]    // 1
```


### 참고사이트 🌐
[서브스크립트 (Subscripts) - The Swift Language Guide (한국어)](https://jusung.gitbook.io/the-swift-language-guide/language-guide/12-subscripts)   
[Swift) 서브스크립트(Subscript) 정복하기](https://babbab2.tistory.com/123)