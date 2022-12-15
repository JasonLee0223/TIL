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
    > For example, the first arguments to these calls do not read as part of the same phrase   
    at the base name:

    ```Swift
    ✅
    let foreground = Color(red: 32, green: 64, blue: 128)
    let newPart = factory.makeWidget(gears: 42, spindles: 14)
    let ref = Link(target: destination)
    ```

    In the following, the API author has tried to create grammatical continuity with the first argument.   

    ```Swift
    ⛔️
    let foreground = Color(havingRGBValuesRed: 32, green: 64, andBlue: 128)
    let newPart = factory.makeWidget(havingGearCount: 42, andSpindleCount: 14)
    let ref = Link(to: destination)
    ```

    In practice, this guideline along with these for argument labels means   
    the first argument will have a label unless the call is performing a value preserving type conversion.

    ```Swift
    let rgbForeground = RGBColor(cmykForeground)
    ```


- >**Name functions and methods according to their side-effects**

- >**Uses of Boolean methods and properties should read as assertions about the receiver** when the use is nonmutating, e.g. x.isEmpty, line1. intersects(line2).

- >**Protocols that describe what something is should read as nouns** (e.g. Collection).

- >**Protocols that describe a capability should be named using the suffixes** able, ible, **or** ing (e.g. Equatable, ProgressReporting).

- >The names of other **types, properties, variables, and constrants should read as nouns.**

