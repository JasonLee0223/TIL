# Closure
보통 `익명함수`를 뜻한다고 생각할텐데, 사실 `func 키워드`를 이용해 `이름을 붙여주는 함수`들도 모두 `클로저`이다.

## 🟢 클로저는 아래와 같이 2가지의 종류가 있다.
- Named Closure(함수) → 보통 선언해서 사용해왔던 이름이 있는 함수, 이를 **클로저라 부르지 않고**, 그냥 **함수**라고 부르는 것 뿐이다.
- Unnamed Closure(익명함수) → 보통 Closure라고 하면 이걸 뜻하는 말이긴하다.
    
## 🟢 **클로저 표현식**      
클로저 표현식은 매개변수를 받거나, 값을 반환하도록 만들 수도 있다.
```Swift
{ (Parameters) -> Return Type in
    //실행 구문
}
```
**in**키워드를 통해 `클로저 헤드`와 `클로저 바디`로 구분할 수 있다.
> 클로저는 익명이긴 하지만 함수다!   
따라서 Swift에서 1급 객체이기 때문에, 다음과 같이 상수에 클로저를 대입할 수 있다.   

### 🔴 **Parameter와 Return Type이 둘 다 없는 클로저** 
```swift
let closure = { () -> () in
    print("Closure")
}
```
      
### 🔴 **Parameter와 Return Type이 있는 클로저**    
```swift
let closure = { (name: String) -> String in
return "Hello, \(name)"
}
```
    
> 주의❗️ - **함수 때 배운 대로 Parameter의 “name”은 단독으로 쓰였으니, Argument Label이자, Parameter Name이겠네요?**   
>👉🏻  **클로저에서는 Argument Label을 사용하지 않음,** 따라서 name은 **Argument Label이 아니고** 오직 Parameter Name이다!
```Swift
closure("sodeul")
closure(name: "Sodeul") // error!
```

### 🔴 1급 객체로서 클로저
1. 클로저를 변수(var) 또는 상수(let)에 대입할 수 있다.
    ```Swift
    // 대입과 동시에 클로저 작성시
    let closure = { () -> () in
        print("Closure")
    }
    let closure2 = closure // 새로운 변수 또는 상수에 대입도 가능
    ```
2. 함수의 파라미터 타입으로 클로저를 전달할 수 있다.
    ```Swift
    // 함수를 파라미터로 전달받는 doSomething함수
    // 여기서 closure:() -> () 는 파라미터
    func doSomething(closure: () -> ()) {
        closure()
    }
    ```
    위처럼 파라미터로 함수를 넘겨줘도 되지만,
    ```Swift
    // 클로저로 함수를 넘겨줄 때
    doSomething(closure: { () -> () in
        print("Hello!")
    })
    ```
    `{ }` 안의 코드영역이 클로저로 작성된 부분이고,
    closure란 Argument Label의 **Parameter로 전달**된 것이다!!
3. 함수의 반환 타입으로 클로저를 사용할 수 있다.
   ```Swift
   func doSomething() -> () -> () { 
        return { () -> () in 
        print("Hello Return Closure")
        }
   }
   //호출
   let closure = doSomething()
   closure()
   ```
   위처럼 `클로저를 리턴`할 수 있다.
      
## 🟢 **후행 클로저(trailing closure)**
>`클로저`가 함수의 마지막 Parameter라면   
이를 파라미터 값 형식이 아닌 함수 뒤에 붙여 작성하는 문법   
이때, Argument Label은 생략된다

### 🔴 1. Parameter가 클로저 하나인 함수
```Swift
func doSomething(closure: () -> ()) {
    closure()
}
```
위 함수를 호출하기 위해서는 아래와 같이 작성해야했다.
```Swift
doSomething(closure: { () -> () in
    print("Hello!")
})
```
`함수 호출 구문()`에 클로저가 파라미터의 값 형식으로 작성되어야한다.   
이러한 방식을 `Inline Closure`라고 부른다.   
하지만 위 방식은 좀처럼 보기가 힘들어 Trailing Closure 표현식을 사용하면   
```Swift
doSomething() { () -> () in
    print("Hello!")
}

// 조금 더 진화해서 호출() 부분도 생략가능하다.
doSomething{ () -> () in
    print("Hello!")
}
```
이렇게 표현할 수 있다.   

여기서 중요한 핵심!
1. 파라미터가 `클로저 하나`일 경우, 이 클로저는 `첫 파라미터이자 마지막 파라미터`이므로 트레일링 클로저가 가능
2. "closure"라는 ArgumentLabel은 트레일링 클로저에선 생략됨   

### 🔴 2. Parameter가 여러 개인 함수
아래와 같이 2개의 파라미터로 클로저를 받는 함수가 있다고하면
```Swift
func fetchData(success: () -> (), fail: () -> ()) {
    // do something...
}
```
- **Inline Closure**
```Swift
fetchData(success: { () -> () in
    print("Success!")
}, fail: { () -> () in
    print("Fail")
})
```
- **Trailing Closure**
```Swift
fetchData(success: { () -> () in
    print("Success!")
}) { () -> () in
    print("Fail!")
}
```
**파라미터가 여러 개일 경우, `함수 호출 구문()`을 마음대로 생략해선 안되는데**   
success란 파라미터는 파라미터의 Value Tyle으로 넘겨줘야하기 때문이다.

### 🔴 **Closure 경량문법**
아래의 예시를 통하여 경량 문법이 적용되는 5가지의 케이스를 확인할 수 있다.
```Swift
func doSomething(closure: {(a: Int, b: Int, c: Int) -> Int in
    return a + b + c
})
```
1. Parameter & Return 형식을 생략할 수 있다.
```Swift
doSomething(closure: {(a, b, c) in
    return a + b + c
})
```
2. Parameter Name은 `Shortand Argument Names`으로 대체하고, 이 경우 `Parameter Name`과 `in` 키워드를 삭제한다.   
Shortand Argument Names는 Parameter Name 대신 사용할 수 있는 것으로   
`a, b, c`라는 Parameter Name 대신   
`a -> $0`   
`b -> $1`   
`c -> $2`   
이런 식으로 `$`와 `index를 이용해 Parameter에 순서대로 접근하는 것을 말한다.
Shorted Argument Names를 적용하면 아래와 같이 표현할 수 있다.
```Swift
doSomething(closure: {
    return $0 + $1 + $2
})
```
3. 단일 리턴문만 남을 경우, return도 생략한다.   
`단일 리턴문`이란, 클로저 내부에 코드가 **return 구문 하나만** 남은 경우를 말한다.   
그렇다면 `return` 키워드도 생략하게 된다면
```Swift
doSomething(closure: {
    $0 + $1 + $2
})
```
4. 클로저 파라미터가 마지막 파라미터면, Trailing Closure로 작성한다.
```Swift
doSomething() {
    $0 + $1 + $2
}
```
또한 파라미터가 하나인 경우 `함수 호출 구문()`도 생략 가능하다.
5. `()`안에 값이 없다면 생략 가능하다.
```Swift
doSomething {
    $0 + $1 + $2
}
```

### 🌐 참고사이트   
[Swift) 클로저(Closure) 정복하기(1/3) - 클로저, 누구냐 넌](https://babbab2.tistory.com/81)   
[Swift) 클로저(Closure) 정복하기(2/3) - 문법 경량화 / @escaping / @autoclosure](https://babbab2.tistory.com/82)