# Closure
보통 `익명함수`를 뜻한다고 생각할텐데, 사실 `func 키워드`를 이용해 `이름을 붙여주는 함수`들도 모두 `클로저`이다.

## 클로저는 아래와 같이 2가지의 종류가 있다.
- Named Closure(함수) → 보통 선언해서 사용해왔던 이름이 있는 함수, 이를 **클로저라 부르지 않고**, 그냥 **함수**라고 부르는 것 뿐이다.
- Unnamed Closure(익명함수) → 보통 Closure라고 하면 이걸 뜻하는 말이긴하다.
    
## **클로저 표현식**      
클로저 표현식은 매개변수를 받거나, 값을 반환하도록 만들 수도 있다.
```Swift
{ (Parameters) -> Return Type in
    //실행 구문
}
```
**in**키워드를 통해 `클로저 헤드`와 `클로저 바디`로 구분할 수 있다.
> 클로저는 익명이긴 하지만 함수다!   
따라서 Swift에서 1급 객체이기 때문에, 다음과 같이 상수에 클로저를 대입할 수 있다.   

### **Parameter와 Return Type이 둘 다 없는 클로저** 
```swift
let closure = { () -> () in
    print("Closure")
}
```
      
### **Parameter와 Return Type이 있는 클로저**    
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

### 1급 객체로서 클로저
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
      
## **후행 클로저(trailing closure) → 많이 쓰임**
- 클로저가 함수의 마지막 argument라면 마지막 매개변수명(cl)을 생략한 후 함수 **소괄호 외부에**
클로저를 작성

```swift
func someFun(cl: **() -> Void**) {
}
//trailing closure를 사용 안하면   
someFun(cl: {
	// closure's body
})

// **trailing closure 사용**
someFun() {
	// trailing closure's body goes here
}
```

```swift
/* trailing closure 예제 */
let onAction = UIAlertAction(title: "On", style: 
UIAlertAction.Style.default) {
	ACTION in self.lampImg.image = self.imgOn
	self.isLampOn = true
}
let removeAction = UIAlertAction(title: "제거", style:
UIAlertAction.Style.destructive, handler: {
	ACTION in self.lampImg.image = self.imgRemove
	self.isLampOn = false
}
```

  ### 🌐 참고사이트   
  [Swift) 클로저(Closure) 정복하기(1/3) - 클로저, 누구냐 넌](https://babbab2.tistory.com/81)   
  [Swift) 클로저(Closure) 정복하기(2/3) - 문법 경량화 / @escaping / @autoclosure](https://babbab2.tistory.com/82)