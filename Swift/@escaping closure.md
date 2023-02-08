# @escaping
우리가 흔히 사용했던 클로저는 모두 non-escaping Closure이다.

> 함수 내부에서 직접 실행하기 위해서만 사용한다.   
> 따라서 파라미터로 받은 클로저를 변수나 상수에 대입할 수 없고,   
> 중첩 함수에서 클로저를 사용할 경우, 중첩함수를 리턴할 수 없다.   
> 함수의 실행 흐름을 탈출하지 않아, 함수가 종료되기 전에 무조건 실행되어야한다.

**함수의 흐름을 탈출하지 않는다는 말은** 함수가 종료되고 나서 클로저가 실행될 수 없다는 말이다.   
(조금만 생각해보면 함수는 호출되었을때 리턴이 있을때까지 혹은 함수안의 모든 코드가 실행되기까지 따로 탈출하는 방법은 없었다..!!)

## @escaping의 사용처
1. 함수 실행을 벗어나서 함수가 끝난 후에도 클로저를 실행하거나
2. 중첩함수에서 실행 후 중첩 함수를 리턴하고 싶거나
3. 변수 상수에 대입하고 싶은 경우
```Swift
// 변수나 상수에 파라미터로 받은 클로저를 대입할 때
func doSomething(closure: @escaping () -> ()) {
    lef function: () -> () = closure
}

// 함수가 종료된 후에도 클로저가 실행될 때
func doSomethingEnd(closure: @escaping () -> ()) {
    print("function start")

    DispatchQueue.main.ayncAfter(deadline: .now() + 10) {
        closure()
    }
    print("function end")
}
doSomethingEnd { print("closure") }
```

## 클로저에서 @escaping 키워드를 붙이는 상황은?
```Swift
Error) Escaping closure captures non-escaping parameter 'completion'
```
위 에러는 일반적으로 아무런 키워드 없이 파라미터로 받는 클로저는 모두 **non-escaping closure**이었고 이름 그래도 탈출이 불가능한 클로저란 뜻이다.
> 함수의 **'흐름'** 을 탈출하지 않는 클로저라는 뜻으로,
> 함수가 종료되고 나서 클로저가 실행될 수 없다는 말이다.
> 함수가 종료될 때, 클로저의 사용도 같이 종료되어서 같이 종료되어야한다는 뜻이다.

## ⚠️주의할 점
### 메모리 관리


## Swift Programming Language 발췌
> A closure is said to escape a function when the closure is passed as an argument to the function, but is called after the function returns.

클로저는 함수에 대한 인자로 전달되지만 함수가 반환된 후에 호출될 때 함수를 탈출한다고합니다.

> When you declare a function that takes a closure as one of its parameters, you can write @escaping before the parameter’s type to indicate that the closure is allowed to escape.

클로저는 매개 변수 중 하나로 사용하는 함수를 선언할 때 매개 변수의 앞에 `@escaping`을 작성하여 클로저가 탈출할 수 있음을 나타낼 수 있습니다.

> One way that a closure can escape is by being stored in a variable that’s defined outside the function.

클로저가 탈출할 수 있는 한 가지 방법은 함수 외부에 정의된 변수에 저장하는 것입니다.

> As an example, many functions that start an asynchronous operation take a closure argument as a completion handler.

예를 들어, 비동기 작업을 시작하는 많은 함수는 `completionHandler`로 클로저 인자를 사용합니다.

> The function returns after it starts the operation, but the closure isn’t called until the operation is completed—the closure needs to escape, to be called later.

함수는 작업을 시작한 후 반환되지만, 클로저는 작업이 완료될 때까지 호출되지 않습니다. 클로저는 나중에 호출하기 위해 탈출해야합니다.

```Swift
var completionHandlers: [() -> Void] = []

func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    completionHandlers.append(completionHandler)
}
```
> The someFunctionWithEscapingClosure(_:) function takes a closure as its argument and adds it to an array that’s declared outside the function.   
> If you didn’t mark the parameter of this function with @escaping, you would get a compile-time error.

`someFunctionWithEscapingClosure(_:)` 함수는 클로저를 인자로 받아 함수 외부에 선언된 배열에 추가합니다.   
이 함수의 매개변수를 `@escaping`으로 표시하지 않으면 컴파일 타임에 오류가 발생합니다.

> An escaping closure that refers to self needs special consideration if self refers to an instance of a class.

`self`가 클래스의 인스턴스를 참조하는 경우 `self`를 참조하는 탈출 클로저는 특별한 고려가 필요합니다.

> Capturing self in an escaping closure makes it easy to accidentally create a strong reference cycle.    
For information about reference cycles, see Automatic Reference Counting.

탈출 클로저에서 `self`를 캡처하면 실수로 강력한 참조 순환을 쉽게 만들어버릴 수 있습니다.   
참조 순환에 대한 자세한 내용은 ARC를 참조하십시오.

### 🌐 참고사이트   
[Swift) 클로저(Closure) 정복하기(2/3) - 문법 경량화 / @escaping / @autoclosure](https://babbab2.tistory.com/82)   
[Swift) closure와 @escaping 이해하기](https://babbab2.tistory.com/164)   
[The Swift Programming Language - Closure](https://docs.swift.org/swift-book/LanguageGuide/Closures.html)