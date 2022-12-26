# Pattern
Swift에는 문법에 응용할 수 있는 다양한 종류의 패턴이 있다.   
Pattern(패턴)은 `'단독 또는 복합 값의 구조를 나타내는 것`이고   
패턴 매칭은 **`'코드에서 어떤 패턴의 형태를 찾아내는 행위'`** 라고 할 수 있다.   
대부분의 패턴은 `switch`, `if`, `guard`, `for` 등의 키워드와 친밀하며 2개 이상의 키워드가 합을 이뤄 동작합니다.   
그 중 switch 구문에서 강력한 힘을 발휘합니다.

Swift 패턴은 크게 두 종류로 나뉩니다.   
- 값을 **`해체(추출)`** 하거나 **`무시`** 하는 패턴
  - 와일드카드
  - 식별자
  - 값 바인딩
  - 튜플
- **`패턴 매칭`** 을 위한 패턴
  - 열거형 케이스
  - 옵셔널
  - 표현
  - 타입캐스팅

## 1️⃣ 와일드카드(_) 패턴 (Wildcard Pattern)
와일드카드 식별자(`_`)를 사용한다는 것은 **`'이 자리에 올 것이 무엇이든간에 상관하지 마라'`** 는 뜻이다.   
즉, 와일드카드 식별자가 위치한 곳의 값은 무시한다.   
```Swift
// Switch-case 구문에서의 와일드카드 예문

// 어떤 값이 와도 상관없기에 항상 실행됩니다.
let string: String = "ABC"
switch string {
    case _: print(string)
}

let optionalString: String? = "ABC"
switch optionalString {
    // optionalString이 Optional("ABC")일 때만 실행됩니다.
    case "ABC"?: print(optionalString)
    // optionalString이 Optional("ABC")외의 값이 있을 때만 실행됩니다.
    case _?: print("Has value, but not ABC")
    // 값이 없을 때 실행됩니다.
    case nil: print("nil")
}
// Result: Optional("ABC")

let yagom = ("yagom", 99, "Male")
switch yagom {
    // 첫 번째 요소가 "yagom"일 때만 실행됩니다.
    case ("yagom", _, _): print("Hello yagom!!!")
    // 그 외 언제든지 실행됩니다.
    case (_, _, _): print("Who cares~")
}
// Result: Hello yagom!!!

// For-in 구문에서의 와일드카드 예문
for _ in 0..<2 {
    print("Hello")
}
// Hello
// Hello
```
## 2️⃣ 식별자 패턴 (Identifier Pattern)
식별자 패턴은 변수 또는 상수의 이름에 알맞는 값을 어떤 값과 매치시키는 패턴   
```Swift
let someValue: Int = 42
```
someValue의 타입인 Int와 할당하려는 42의 타입이 매치된다면 someValue는 42라는 값의 식별자가 되므로 식별자 패턴이 성립됩니다.

## 3️⃣ 값 바인딩 패턴 (Value-Binding Pattern)
값 바인딩 패턴은 **변수 또는 상수의 이름에 매치된 값을 바인딩**하는 것입니다.   
값 바인딩 패턴의 일종인 식별자 패턴은 매칭되는 값을 새로운 이름의 변수 또는 상수에 바인딩합니다.   
```Swift
let yagom = ("yagom", 99, "Male")
switch yagom {
    // name, age, gender를 yagom의 각각의 요소와 바인딩합니다.
    case let (name, age, gender) : print("Name: \(name), Age: \(age), Gender: \(gender)")
}
// Result: Name: yagom, Age: 99, Gender: Male

switch yagom {
    case (let name, let age, let gender): print("Name\(name), Age: \(age), Gender: \(gender)")
}
// 결과값이 위와 동일

// 값 바인딩 패턴은 와일드카드 패턴과 결합하여 유용하게 사용될 수도 있습니다.
switch yagom {
    case (let name, _, let gender): print("Name\(name), Gender: \(gender)")
}
// Result: Name: yagom, Gender: Male
```

## 4️⃣ 튜플 패턴 (Tuple Pattern)
튜플 패턴은 소괄호(**`()`**) 내에 쉼표로 분리하는 리스트입니다.   
예를 들어, `let(x, y): (Int, Int) = (1, 2)`와 같이 상수를 선언한다면   
`(x, y) = (Int, Int)`라고 사용된 튜플 패턴은 요소가 모두 Int 타입인 튜플하고만 매치된다는 뜻입니다.

## 5️⃣ 열거형 케이스 패턴 (Enumeration Case Pattern)
열거형 케이스 패턴은 값을 열거형 타입의 case와 매치시킵니다.   
열거형 케이스 패턴은 switch 구문의 case 레이블과 `if, while, guard, for-in 구문`의 case 조건에서 볼 수 있습니다.

```Swift
enum MainDish {
    case pasta(taste: String)
    case pizza(dough: String, topping: String)
    case chicken(withSauce: Bool)
    case rice
}

var dishes: [MainDish] = []
var dinner: MainDish = .pasta(taste: "크림")  // 크림 파스타
dishes.append(dinner)

if case .pasta(let taste) = dinner {
    print("\(taste) 파스타")
}

dinner = .pizza(dough: "치즈크러스트", topping: "불고기")    // 치즈크러스트 불고기 피자 만들기
dishes.append(dinner)

func whatIsThis(dish: MainDish) {
    guard case .pizza(let dough, let topping) = dish else {
        print("It's not a Pizza")
        return
    }
    print("\(dough) \(topping) 피자")
}
whatIsThis(dish: dinner)                   // 치즈크러스트 불고기 피자
```

## 6️⃣ 옵셔널 패턴 (Optional Pattern)
옵셔널 패턴은 옵셔널 또는 암시적 추출 옵셔널 열거형에 감싸져 있는 값을 매치시킬 때 사용합니다.   
옵셔널 패턴은 식별자 패턴 뒤에 물음표를 넣어 표기하며 열거형 케이스 패턴과 동일한 위치에 자리합니다.   
```Swift
var optionalValue: Int? = 100
if case let value? = optionalValue {
    print(value)
    // 100
}

func isItHasValue(_ optionalValue: Int?)  {
    guard case .some(let value) = optionalValue else {
        print("none")
        return
    }
    print(value)
}
isItHasValue(optionalValue)             // 100
```

## 7️⃣ 타입캐스팅 패턴 (Type-Casting Pattern)
타입캐스팅 패턴에는 `is 패턴`과 `as 패턴`이 있습니다.   
- is 패턴은 switch의 case 레이블에서만 사용할 수 있습니다.
  - is 패턴은 is (TYPE_NAME)과 같이 쓸 수 있고
- as 패턴은 SomePattern as (TYPE_NAME)과 같이 쓸 수 있습니다.

타입캐스팅 패턴은 타입캐스팅을 하거나 타입을 매치시킵니다.
```Swift
let someValue: Any = 100

switch someValue {
    // 타입이 Int인지 확인하지만 캐스팅된 값을 사용할 수는 없습니다.
    case is String: print("It's String!")

    // 타입 확인과 동시에 캐스팅까지 완료되어 value에 저장됩니다.
    // 값 바인딩 패턴과 결합된 모습입니다.
    case let value as Int: print(value + 1)
    default: print("Int도 String도 아닙니다.")
}
// Result: 101
```

## 8️⃣ 표현 패턴 (Expression Pattern)
표현 패턴은 표현식의 값을 평가한 결과를 이용하는 것입니다.   
그리고 switch 구문의 case 레이블에서만 사용할 수 있습니다.   

표현 패턴은 스위프트 표준 라이브러리의 패턴 연산자인 `~= 연산자`의 연산 결과가 `true`를 반환하면 매치시킵니다.