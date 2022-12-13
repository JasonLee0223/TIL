# Error Handling

프로그램 실행시 에러가 발생하면 그 상황에 대해 적절한 처리가 필요하다.   
Swift에서는 런타임에 에러가 발생한 경우 그것의 처리를 위해 에러의   
`발생(throwing), 감지(catching), 증식(propagating), 조작(manipulating)`을 지원하는 `1급 클래스(First-class)`를 제공한다.   

어떤 명령은 항상 완전히 실행되는 것이 보장되지 않는 경우도 있다.   
그런 경우에 옵셔널을 사용해 에러가 발생해 값이 없다는 것을 표시할 수 있지만,   
어떤 종류의 에러가 발생했는지 확인할 수는 없다.   
이럴 때는 구체적으로 발생한 에러를 확인할 수 있어야 코드를 작성하는 사람이   
각 에러의 경우에 따른 적절한 처리를 할 수 있다.   

## 🟢 에러의 표시와 발생 (Representing and Throwing Errors)
Swift에서는 Error 프로토콜을 따르는 타입의 값으로 표현된다.   
Swift의 열거형은 특별히 이런 관련된 에러를 그룹화(Grouping)하고 추가적인 정보를 제공하기에 적합하다.   
```Swift
enum VendingMachineError: Error {
    case invalidSelection
    case insufficientFunds(coinsNeeded: Int)
    case outOfStock
}
```

에러를 발생시킴으로써 무언가 기다하지 않았던 동작이 발생했고 작업을 계속 수행할 수 없다는 것을 알려줄 수 있다.   
에러를 발생시키기 위해 `throw`구문을 사용할 수 있다.   
```Swift
throw VendingMachineError.insufficientFunds(coinNeeded: 5)
```

## 🟢 에러 처리(Handling Errors)
에러가 발생하면 특정 코드영역이 해당 에러를 처리하도록 해야한다.   
**`Swift에서 4가지 에러를 처리 방법이 있다.`**   

1. 에러가 발생한 함수에서 리턴값으로 에러를 반환해 해당 함수를 호출한 코드에서 에러를 처리하는 방법
2. `do-catch`구문을 사용하는 방법
3. 옵셔널 값을 반환하는 방법
4. assert를 사용해 강제로 Crash(충돌)를 발생시키는 방법

### 🔴 1. 에러를 발생시키는 함수 사용하기 (Propagating Errors Using Throwing Functions)
어떤 함수, 메서드 혹은 초기자가 에러를 발생 시킬 수 있다는 것을 알리기 위해서 `throw 키워드`를 함수 선언부의 파라미터 뒤에 붙일 수 있다.   
`throw 키워드`로 표시된 함수를 `throwing function`이라고 부른다.   
만약 함수가 리턴 값을 명시했다면 throw 키워드는 리턴 값 표시 기호인 -> 전에 적는다.   
```Swift
func canThrowErrors() throws -> String

func cannotThrowErrors() -> String
```
`throwing function`은 함수 내부에서 에러를(throw)를 만들어 함수가 호출된 곳에 전달한다.   

```Swift
// Example1
struct Item {
    var price: Int
    var count: Int
}

class VendingMachine {
    var inventory = [
        "Candy Bar": Item(price: 12, count: 7),
        "Chips": Item(price: 10, count: 4),
        "Pretzels": Item(price: 7, count: 11)
    ]
    var coinsDeposited = 0

    // vend(itemNamed:) 메소드는 에러를 발생시키기 때문에 
    // 이 메소드를 호출하는 메소드는 반드시 do-catch, try?, try! 등의 
    //구문을 사용해 에러를 처리해야 합니다.
    func vend(itemNamed name: String) throws {
        guard let item = inventory[name] else {
            throw VendingMachineError.invalidSelection
        }

        guard item.count > 0 else {
            throw VendingMachineError.outOfStock
        }

        guard item.price <= coinsDeposited else {
            throw VendingMachineError.insufficientFunds(coinsNeeded: item.price - coinsDeposited)
        }

        coinsDeposited -= item.price

        var newItem = item
        newItem.count -= 1
        inventory[name] = newItem

        print("Dispensing \(name)")
    }
}
```
```Swift
// Example2
let favoriteSnacks = [
    "Alice": "Chips",
    "Bob": "Licorice",
    "Eve": "Pretzels",
]
func buyFavoriteSnack(person: String, vendingMachine: VendingMachine) throws {
     let snackName = favoriteSnacks[person] ?? "Candy Bar"

     // vend(itemNamed:) 메소드는 에러를 발생 시킬 수 있기 때문에 메소드 호출 앞에 try 키워드를 사용합니다.

     try vendingMachine.vend(itemNamed: snackName)
}

// PurchasedSnack 구조체의 초기자는 초기화 단계의 일부분으로써 에러를 발생시킬 수 있는 함수입니다. 
// 그리고 초기자가 실행될 때 발생한 에러는 이 초기자를 호출한 곳에 전달 됩니다.
struct PurchasedSnack {
    let name: String
    init(name: String, vendingMachine: VendingMachine) throws {
        try vendingMachine.vend(itemNamed: name)
        self.name = name
    }
}
```

### 🔴 2. Do-Catch를 이용해 에러를 처리하기 (Handling Error Using Do-Catch)
`do-catch`를 이용해 에러를 처리하는 코드 블럭을 작성할 수 있다.   
만약 에러가 do구문 안에서 발생한다면 발생하는 에러의 종류를 catch 구문으로 구분해 처리할 수 있다.   
```Swift
do {
    try expression
    statements
} catch pattern 1 {
    statements
} catch pattern 2 where condition {
    statements
} catch {
    statements
}
```
catch 구문 뒤에 어떤 에러인지 적고 그것을 어떻게 처리할 지 명시할 수 있고   
만약 catch 구문 뒤에 에러 종류를 명시하지 않으면 발생하는 모든 에러를 지역 상수인 error로 바인딩한다.   
```Swift
// Example
var vendingMachine = VendingMachine()
vendingMachine.coinsDeposited = 8
do {
    // 이 함수가 에러를 발생시킬 수 있기 때문에 에러가 발생하자마자 catch구문에 전달해
    // 적절한 처리를 할 수 있게 하기 위해서 try 표현 안에서 호출된다.
    try buyFavoriteSnack(person: "Alice", vendingMachine: vendingMachine)
    print("Success! Yum.")
} catch VendingMachineError.invalidSelection {
    print("Invalid Selection.")
} catch VendingMachineError.outOfStock {
    print("Out of Stock.")
} catch VendingMachineError.insufficientFunds(let coinsNeeded) {
    print("Insufficient funds. Please insert an additional \(coinsNeeded) coins.")
} catch {
    // 만약 발생한 에러 종류를 처리하는 catch 구문이 없다면 
    // 에러는 마지막 catch 구문에 걸리게 되서 지역 에러 상수인 error로 처리할 수 있다.
    print("Unexpected error: \(error).")
}
// Prints "Insufficient funds. Please insert an additional 2 coins."
```
- 만약 아무런 에러도 발생하지 않는다면 do 구문이 실행된다.   
  catch 구문에서 발생 가능한 모든 에러에 대해 반드시 종류 별로 처리할 필요는 없다.
- 만약 에러를 처리하는 적절한 catch 구문이 없다면 그 코드에 둘러 쌓인 곳에 에러가 발생한다.   
  하지만 발생되는 에러는 반드시 관련된 특정 코드 영역에서 처리되어야한다.
- 에러를 발생 시키지 않는 함수에서는 관련된 do-catch 구문에서 그 에러를 반드시 처리해야하고,   
  에러를 발생 시키는 함수에서는 에러를 do-catch 구문에서 처리하거나 함수를 호출한 곳에서 반드시 에러를 처리해야한다.   
- 만약 에러가 발생한 곳에서 에러에 대해 아무런 처리도 하지 않으면 런타임 에러가 발생하게 된다.   

### 🔴 3. 에러를 옵셔널 값으로 변환하기 (Converting Errors to Optional Values)
`try?` 구문을 사용해 에러를 옵셔널 값으로 반환할 수 있다.   
만약 에러가 try? 표현 내에서 발생한다면, 그 표현의 값은 `nil`이 된다.   
```Swift
// Example
func someThrowingFunction() throws -> Int {
    // ...
}

let x = try? someThrowingFunction()

let y: Int?
do {
    y = try someThrowingFunction()
} catch {
    y = nil
}
```
- 만약 `someThrowingFunction()`이 에러를 발생시키면 x와 y는 nil이 된다.   
  그렇지 않으면 x와 y는 함수의 리턴값을 갖게된다.
- x와 y는 `someThrowingFunction()`의 타입이 어떤 것이든 상관없이 옵셔널이 된다.   
- 이 함수에서는 Int를 리턴하기 때문에 x와 y는 `Int?`타입이 된다.   
- 💡 `try?`는 만약 발생하는 모든 에러를 같은 방법으로 처리하고 싶을 때 사용한다.
  
### 🔴 4. 에러 발생을 중지하기(Disabling Error Propagation)
함수나 메서드에서 에러가 발생하지 않을 것이라고 확신하는 경우 `try!`를 사용할 수 있다.   
혹은 `runtime assertion`을 사용하여 에러가 발생하지 않도록 할 수 있다.   
하지만 만약 에러가 발생하면 런타임 에러가 발생하게 된다.   

- 예를 들어, 다음 코드는 loadImage(atPath:) 함수를 사용해 주어진 경로에서   
  이미지 리소스를 불러오거나 이미지를 불러오는데 실패한 경우 에러를 발생 시킵니다.   
  이 경우에는 앱이 배포될 때 이미지가 포함되 배포되기 때문에   
  런타임에는 아무 에러도 발생되지 않을 것이라고 확신할 수 있어 try!를 사용하는 것이 적절하다.
```Swift
let photo = try! loadImage(atPath: "./Resources/JohnAppleseed.jpg")
```
---
## 🟢 정리 액션 기술(Specifying Cleanup Actions)
`defer` 구문을 이용해 함수가 종료 된 후 파일 스트림을 닫거나,   
사용했던 자원을 해지하는 등의 일을 할 수 있다.   
`defer`가 여러개 있는 경우 가장 마지막 줄부터 실행된다.   
즉, `bottom-up`순으로 진행된다.   
```Swift
func processFile(filename: String) throws {
    if exists(filename) {
        let file = open(filename)
        defer {
            close(file) // block이 끝나기 직전에 실행, 주로 자원 해제나 정지에 사용
        }
        while let line = try file.readline() {
            // Work with the file.
        }
        // close(file) is called here, at the end of the scope.
    }
}
```
- 위 예제는 defer 구문을 이용해 `open(:)`함수와 짝을 이루는 `close(:)` 함수를 실행한다.

### 🌐 Reference Site
[에러 처리(Error Handling) - The Swift Language Guide](https://jusung.gitbook.io/the-swift-language-guide/language-guide/17-error-handling)