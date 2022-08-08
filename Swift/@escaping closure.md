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

## ⚠️주의할 점
### 메모리 관리

### 🌐 참고사이트   

[Swift) 클로저(Closure) 정복하기(2/3) - 문법 경량화 / @escaping / @autoclosure](https://babbab2.tistory.com/82)   
