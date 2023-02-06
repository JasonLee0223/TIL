# Argument Labels
```Swift
func move(from start: Point, to end: Point)
x.move(from: x, to: y)
```
- **`레이블이 인자값을 구분하는데 도움이 되지않으면 모든 레이블을 생략하라.`**   
  예시) min(number1, number2), zip(sequence1, sequence2)
- **`초기화 생성함수에서 다른 타입 값을 받아서 변환하고 보관하는 (값보존 변환) 경우에는 첫 번째 인자 레이블을 생략하라.`**   
  예시) Int64(someUInt32)   
  - 첫 번째 인자값은 항상 변환할 값을 전달하라.
    ```Swift
    extension String {
    // Convert `x` into its textual representation in the given radix
      init(_ x: BigInt, radix: Int = 10)   ← Note the initial underscore
    }

    text = "The value is: "
    text += String(veryLargeNumber)
    text += " and in hexadecimal, it's"
    text += String(veryLargeNumber, radix: 16)
    ```
  - 정밀한(narrowing) 타입 변환은 레이블에 정밀도를 표현하라.   
    (아래 코드에서 64bit에서 32bit로 그냥 줄어들 때는 truncating를, 64bit에서 32bit 근사값을 처리할 때는 saturating로 표기하고 있다.)
    ```Swift
    extension UInt32 {
    /// Creates an instance having the specified `value`.
    init(_ value: Int16)            ← Widening, so no label
    /// Creates an instance having the lowest 32 bits of `source`.
    init(truncating source: UInt64)
    /// Creates an instance having the nearest representable
    /// approximation of `valueToApproximate`.
    init(saturating valueToApproximate: UInt64)
    }
    ```
    **값 보존 변환은 (입력값에 따라 1:1로 고유한 결과값에 매칭되는) 모노모피즘(monomorphism)방식이다.**   
    `Int8`값을 `Int64`로 변환할 때는 모든 `Int8`값이 그대로 `Int64`값으로 보존된다.   
    반대 경우에는 `Int8`보다 `Int64`가 더 표현할 수 있는 값이 많기 때문에 `Int64`값이 보존되지 않는다.   
    Note: 원래 값을 가져올 수 있느냐는 변환할 때 값을 보존하는 지와 관련이 없다.   
    값을 보존하지 않더라도 원래 값을 그대로 가져올 수 있는 경우도 있고 값에 따라 다를 수 있다.
- **`첫 번째 인자값이 (영어에서) 전치사 형태라면 인자값 레이블을 표기하라.`**   
  `x.removeBoxes(havingLength: 12)`처럼 인자값 레이블은 보통 전치사보다 앞에 표시한다.   
  - ⛔️ 처음 두 인자값이 동일한 추상화 수준인 경우에 전치사를 붙이면 예외(exception) 처리가 된다.
    ```Swift
    a.move(toX: b, y: c)
    a.fade(fromRed: b, green: c, blue: d)
    ```
  - ✅ 이런 경우는 인자값 레이블을 전치사 다음에 표기해서, 추상화 수준을 유지한다.
    ```Swift
    a.moveTo(x: b, y: c)
    a.fadeFrom(red: b, green: c, blue: d)
    ```
- 첫 번째 인자값이 (전치사가 아니라) 다른 문법상의 구문이라면 레이블은 생략하고, `x.addSubView(y)`처럼 기본 이름에 의미있는 단어를 뒤에 붙여도 된다.
  - ✅ 첫 번째 인자값이 문법상의 구문이 아니라면, 레이블은 표기한다.
  ```Swift
    view.dismiss(animated: false)
    let text = words.split(maxSplits: 12)
    let studentsByName = students.sorted(isOrderedBefore: Student.namePrecedes)
  ```
  - ⛔️ 문장이 올바른 의미를 전달하고 있는지가 중요하다. 아래 코드는 문법상으로 정확하지만 의미상으로 잘못된 내용을 표현한다.
    ```Swift
    view.dismiss(false)   // 사라지는게 실패한건가? Bool 값이 사라져야 하는걸까?
    words.split(12)       // 숫자 12를 나눠야 하는건가?
    ```
  - 기본값이 있는 인자값은 생략가능해서 문법상 의미있는 역할을 하지못하기 때문에 반드시 레이블이 있어야한다.
- **`그 외에 모든 경우는 레이블을 표기하라.`**