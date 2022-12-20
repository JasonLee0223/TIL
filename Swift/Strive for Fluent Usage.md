# Strive for Fluent Usage (자연스러운 사용을 위해 노력하기)

- >**Prefer method and function names that make user sites form grammartical English phrases.**

    사용되는 장소의 메서드와 함수의 이름은 영어 문법에 맞는 구가 되도록 하는 것이 좋습니다.   

    ## 🔎 MORE DETAIL
    ```Swift
    ✅
    x.insert(y, at: z)          “x, insert y at z”
    x.subViews(havingColor: y)  “x's subviews having color y”
    x.capitalizingNouns()       “x, capitalizing nouns”
    ```

    ```Swift
    ⛔️
    x.insert(y, position: z)
    x.subViews(color: y)
    x.nounCapitalize()
    ```

    > It is acceptable for fluency to degrade after the first argument or two when those   
    arguments are not central to the call's meaning:

    첫 번째 또는 두 번째 전달인자 이후의 전달인자가 호출 의미의 핵심이 아닌 경우에는 자연스러움이 떨어져도 괜찮습니다:

    ```Swift
    // Example
    AudioUnit.instantiate(
        with: description, 
        options: [.inProcess], completionHandler: stopProgressBar)
    ```

- >**Begin names of factory methods with** "make", e.g. x.makeIterator().

    예를 들어, `x.makeIterator()`와 같이, 팩토리 메서드 이름은 `"make"`로 시작합니다.   

- >The first argument to **initializer and** factory methods calls should not form a phrase starting with the base name, e.g. x.makeWidget(cogCount: 47)

    `x.makeWidget(cogCount:47)`의 예시처럼,   
    **이니셜라이저와 [팩토리 메서드](https://ko.wikipedia.org/wiki/%ED%8C%A9%ED%86%A0%EB%A6%AC_%EB%A9%94%EC%84%9C%EB%93%9C_%ED%8C%A8%ED%84%B4) 호출**에 대한 첫 번째 전달인자는 함수 이름으로 시작하는 구문으로 작성하면 안됩니다.   

    ## 🔎 MORE DETAIL
    > For example, the first arguments to these calls do not read as part of the same phrase at the base name:
    
    예를 들어, 이러한 호출에 대한 첫 번째 인수는 기본 이름에서 동일한 구의 일부로 읽히지 않습니다.

    ```Swift
    ✅
    let foreground = Color(red: 32, green: 64, blue: 128)
    let newPart = factory.makeWidget(gears: 42, spindles: 14)
    let ref = Link(target: destination)
    ```

    In the following, the API author has tried to create grammatical continuity with the first argument.   

    다음에서 API 작성자는 첫 번째 인수로 문법적 연속성을 만들려고 주의하였습니다.   

    ```Swift
    ⛔️
    let foreground = Color(havingRGBValuesRed: 32, green: 64, andBlue: 128)
    let newPart = factory.makeWidget(havingGearCount: 42, andSpindleCount: 14)
    let ref = Link(to: destination)
    ```

    In practice, this guideline along with these for argument labels means   
    the first argument will have a label unless the call is performing a value preserving type conversion.

    참고로, 전달인자 레이블에 대한 지침에는 함수를 호출하는 부분에서 값의 타입에 대해서   
    그 타입이 유지되지 않고 변경된다면 첫 번째 전달인자는 레이블을 생략해도된다.
    ```Swift
    let rgbForeground = RGBColor(cmykForeground)
    ```

- >**Name functions and methods according to their side-effects**   

    **함수와 메서드의 이름은 side-effects(부수 효과)에 따라 이름을 붙입니다.**

  - Those without side-effects should read as noun phrases,   
    e.g. **x.distance(to: y), i.successor()**   
    
    위 예시의 `x.distance(to: y), i.successor()`는,   
    부수 효과가 없는 함수 및 메서드는 명사 구로 읽어야한다.

  - Those with side-effects should read as imperative verb phrases,   
    e.g. **print(x), x.sort(), x.append(y)**  

    위 예시 `print(x), x.sort(), x.append(y)`와 같이,   
    부수 효과가 있는 함수 및 메서드는 명령형인 동사구로 읽어야한다.

  - **`Name Mutating/nonmutating method pairs`** consistently.   
    A mutating method will often have a nonmutating variant with similar semantics,   
    but that returns a new value rather than updating an instance in-place.   

    **`Mutating/nonmutating` 메서드 쌍**의 이름을 일관되도록 지정합니다.   
    Mutating 메서드는 종종 비슷한 의미를 가진 변경 불가능한 함수를 갖지만,   
    해당 메서드는 인스턴스를 자체를 업데이트하기 보다는 새로운 값을 반환합니다. 

    - When the operation is **`naturally described by a verb`**,   
      use the verb's imperative for the mutating method and apply the "ed" or "ing"   
      suffix to name its nonmutating counterpart.

      기능이 **`동사로 자연스럽게 설명`** 되는 경우,   
      Mutating 메서드는 동사의 명령형을 사용하고, "ed" 또는 "ing" 접미사를 붙여   
      그에 대응하는 nonMutating 메서드 이름에 적용합니다.

        |Mutating|Nonmutating|
        |---|---|
        |x.sort()|z = x.sorted()|
        |x.append(y)|z = x.appeinding(y)|
    
    ## 🔎 MORE DETAIL
    - Prefer to name the nonmutating variant using the verb's past participle(usually appending "ed"):   
      nonMutating 메서드는 동사의 과거분사형(보통 "ed" 추가)를 사용하여 이름을 지정하는 것이 좋습니다.
        ```Swift
        /// Reverses 'self' in-place.
        mutating func reverse()

        /// Returns a reversed copy of 'self'.
        func reversed() -> Self
        ...
        x.reverse()
        let y = x.reversed()
        ```

    - When adding "ed" is not grammatical   
      because the verb has a direct object,   
      name the nonmutating variant using the verb's present participle, by appending "ing".
      동사에 직접 목적어를 포함하고 있어 `"ed"`를 추가하는 것이 문법에 맞지 않는 경우,   
      nonMutating 형태는 `"ing"`를 붙여 동사의 현재 분사를 사용하여 이름을 지정합니다.   

        ```Swift
        /// Strips all the newlines from 'self'
        mutating func stripNewlines()

        /// Returns a copy of 'self' with all the newlines stripped.
        func strippingNewlines() -> String
        ...
        s.stripNewlines()
        let oneLine = t.strippingNewlines()
        ```

    - When the operation is **`naturally described by a noun`**,   
      use the noun for the nonmutating method and apply the "form"   
      prefix to name its mutating counterpart.

      기능이 **명사로 자연스럽게 설명**되는 경우,   
      nonMutating 메서드에 명사를 사용하고, `"form"` 접두어를 붙여 대응하는   
      mutating 메서드에 이름을 적용합니다.

      |Mutating|Nonmutating|
      |---|---|
      |y.formUnion(z)|x=y.union(z)|
      |c.formSuccessor(%i)|j = c.successor(i)
    
- >**Uses of Boolean methods and properties should read as assertions about the   
  receiver** when the use is nonmutating, e.g. x.isEmpty, line1. intersects(line2).

    위 예시 `x.isEmpty, line1. intersects(line2)`처럼, **`Bool 메서드 및 프로퍼티의 사용은`**   
    nonMutating 메서드일 때, **`수신자에 대한 주장처럼 읽어야한다.`**

- >**Protocols that describe what something is should read as nouns** (e.g. Collection).
  
  **무언가를 설명하는 프로토콜은 명사로 읽어야 한다.** (예를 들면, Collection)

- >**Protocols that describe a capability should be named using the suffixes** able, ible, **or** ing (e.g. Equatable, ProgressReporting).   
  
  **`능력을 설명하는 프로토콜`** 은 `able, ible 또는 ing` **접미사를 사용해서 이름을 지정해야한다.**

- >The names of other **types, properties, variables, and constrants should read as nouns.**   
  
  다른 **`타입, 프로퍼티, 변수 그리고 상수의 이름은 명사로 읽어야한다.`**