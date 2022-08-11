# 1급 객체(First-Class Citizen)
Closure를 학습하다 1급 객체를 많이 들어보았지만 정확히 어떤 의미에서 함수를 1급 객체라고 명칭하는지 이해하기 힘들었다...   
Swift는 객체지향 + 함수형 + 프로토콜형 프로그래밍이 혼재되어있는데   
그 중 함수형 프로그래밍이 가능한 이유는 바로 함수가 1급 객체이기 때문입니다.   

## 1급 객체란 무엇일까요? 
1급 객체는 3가지 특징이 있습니다.
> 변수나 상수에 함수를 대입할 수 있다.   
> 함수의 반환 타입으로 함수를 사용할 수 있다.   
> 함수의 인자값으로 함수를 사용할 수 있다.   

## 1. 변수나 상수에 함수를 대입할 수 있다.
단순하게 함수를 호출하고 호출한 결과 값을 변수 또는 상수에 할당하는 게 아니라, 함수 자체를 할당할 수 있습니다.
```Swift
func getName(name: String) -> String {
    return name
}

let name = getName(name: "개발이 취미인 사람") // 상수에 함수가 호출 된 결과 값을 할당
let nameFun: (String) -> () = getName(name:) // 상수에 함수 자체를 할당
```
## 2. 함수의 반환 타입으로 함수를 사용할 수 있다.
일급 객체인 함수는 반환 값으로 데이터가 아닌 함수 자체를 반환할 수 있습니다.
```Swift
//덧셈 함수 선언
func plus( a:Int, b: Int) -> Int {
    return a+b
}

// Int형태에 a와 b 값을 전달 받고 (Int,Int) 파라미터를 받는 함수를 반환한다. 
// 그리고 두번째 호출을 통해 그 결과 자료 형태는 Int 타입이라고 선언하는 함수
func setPlus(a:Int, b: Int) -> (Int, Int) -> Int {
    
    return plus
}

//사용법
let onPlus = setPlus(a: 1, b:2) // 함수를 반환

onPlus(1, 2) // 결과 값은 3

//바로 호출 가능
setPlus(a: 1, b: 2)(3, 2) // 결과 값 5
```
## 3. 함수의 인자값으로 함수를 사용할 수 있다.
일급 객체인 함수는 인자(파라미터) 값으로 변수 또는 상수가 아닌 함수를 전달할 수 있습니다.
```Swift
//덧셈 함수 선언
func plus( a:Int) -> Int {
    print("3")
    return a + 1
}

//(Int) -> Int 형태에 파라미터를 받는다.
func setPlus(a:Int, fn: (Int) -> Int) -> Int {
    print("2")
    return fn(a) //값 2 반환
}

print("1")

//plus 함수를 전달한다.
setPlus(a: 1, fn: plus) // 2값 반환
print("4")

// 실행 순서 1 -> 2 -> 3 -> 4 
```

[[iOS] First Class Citizen(1급 객체)](https://velog.io/@hope1053/iOS-First-Class-Object1%EA%B8%89-%EA%B0%9D%EC%B2%B4)   
[[Swift] Swift 일급 객체 개념 및 사용법](https://any-ting.tistory.com/82)   
[About Swift – “first class object, 1급 객체”](https://gdsanadev.com/695)   