# ~= Operator

`~= 연산자`는 대상이 특정 범위에 속하는지 `범위를 체크`하는 연산자이다.   
`switch 구문`에 바로 이 `~= 연산자`가 사용된다.   
`case`의 범위를 확인할 때 내부적으로 ~= 연산자가 불려져 사용되고 있던 것이다.   

## Example
```Swift
// Int 타입에서 사용했을 떄
var number = 5

// number가 앞의 Range안에 속했을 때 `*`연산을 실행해라.
if 0..<10 ~= number {
    n *= 10
}
print(number)   // 50

// String 타입에서 사용하였을 때
func checkLowercase(sentetnce: String) -> Bool {
    guard "a"..."z" ~= sentence else {
        return false
    }
    return true
}

checkLowercase(sentence: "a")    // true
checkLowercase(sentence: "aA")   // true
checkLowercase(sentence: "A")    // false
```

## 패턴 매칭 예제
앞서 switch구문에서 ~= 연산자가 사용된다고 말하였다.   
따라서 `~= 연산자`를 재정의하면 서로 다른 타입도 switch 연산으로 처리할 수 있다.

```Swift
struct Person {
    let name: String
}

func ~=(pattern: String, value: Person) -> Bool {
    return value.name == pattern
}
let person = Person(name: "Jason")

switch person {
    case "Jason":
        print("Hello Jason!")
    default:
        print("Sorry")
}
// Output: "Hello Jason!"

if case "Jason" == person {
    print("Hello Jason")
}
```

### 🌐 Reference Site
[~= 연산자 in Swift](https://woongsios.tistory.com/147)