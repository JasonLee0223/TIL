# Error Handling

프로그램 실행시 에러가 발생하면 그 상황에 대해 적절한 처리가 필요하다.   
Swift에서는 런타임에 에러가 발생한 경우 그것의 처리를 위해 에러의   
`발생(throwing), 감지(catching), 증식(propagating), 조작(manipulating)`을 지원하는 `1급 클래스(First-class)`를 제공한다.   

어떤 명령은 항상 완전히 실행되는 것이 보장되지 않는 경우도 있다.   
그런 경우에 옵셔널을 사용해 에러가 발생해 값이 없다는 것을 표시할 수 있지만,   
어떤 종류의 에러가 발생했는지 확인할 수는 없다.   
이럴 때는 구체적으로 발생한 에러를 확인할 수 있어야 코드를 작성하는 사람이   
각 에러의 경우에 따른 적절한 처리를 할 수 있다.   

## 에러의 표시와 발생 (Representing and Throwing Errors)
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

## 에러 처리(Handling Errors)
에러가 발생하면 특정 코드영역이 해당 에러를 처리하도록 해야한다.   
**`Swift에서 4가지 에러를 처리 방법이 있다.`**   

1. 에러가 발생한 함수에서 리턴값으로 에러를 반환해 해당 함수를 호출한 코드에서 에러를 처리하는 방법
2. `do-catch`구문을 사용하는 방법
3. 옵셔널 값을 반환하는 방법
4. assert를 사용해 강제로 Crash(충돌)를 발생시키는 방법

### 1. 에러를 발생시키는 함수 사용하기 (Propagating Errors Using Throwing Functions)
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