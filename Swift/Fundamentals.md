# Fundamentals

## 📕 Fundamentals (핵심 개념)
- >**Clarity at the point of use** is your most important goal.   
    Entities such as methods and properties are declared only once but used repeatedly.   
    Design APIs to make those uses clear and concise.   
    When evaluating a design, reading a declaration is seldom sufficient;   
    always examine a use case to make sure it looks clear in context.

    API 설계의 가장 중요한 목적은 **사용하는 시점에서의 명확성(명료성)** 이다.   
    메서드나 프로퍼티와 같은 개체(Entity)는 한 번 선언해두면 반복적으로 사용이 가능하다.   
    API는 이러한 개체들을 명확하고 간결하게 사용할 수 있도록 설계해야한다.   
    API 설계를 평가할 때, 코드의 선언부를 읽는 것만으로는 충분하지 않다.   
    항상 문맥에 알맞도록 명확하게 설계하였는지 실질적인 사용 사례를 통해 검토하여 확인해보야아한다.

- >**Clarity is more important than brevity.**   
    Although Swift code can be compact, it is a non-goal to enable the smallest possible code with the fewest characters.   
    Brevity in Swift code, where it occurs, is a side-effect of the strong type system and features that naturally reduce boilerplate.

    **명확성(명료성)은 간결성보다 중요합니다.**   
    Swift 코드를 간결하게 작성할 수 있지만, 단순히 몇 개의 문자들만 사용하여 가장 적은 코드를 작성하는 것은 목표에 어긋납니다.   
    Swift 코드의 간결함은 강력한 타입 시스템의 부수 효과이고 반복되는 인용구를 자연스럽게 줄일 수 있는 기능입니다.   

- >**Write a documentation comment** for every declaration.   
    Insights gained by writing documentation can have a profound impact on your design, so don’t put it off.

    **모든 선언문에 문서 주석을 작성합니다.**   
    주석을 작성하면서 얻은 통찰력은 API 설계에 엄청난 영향을 미칠 수 있으므로 미루지 말고 주석을 작성하세요.   

- >If you are having trouble describing your API’s functionality in simple terms,   
  **you may have designed the wrong API.**

    만약 API 기능을 간단한 용어로 설명하는 데 어렵다면, 이는 **잘못된 API를 설계했을수도 있습니다.**   

### 🔎 More Detail
- >**Use Swift's** [dialect of Markdown](https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/).   

  Swift에서 지원하는 [마크다운 형식](https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/)을 이용하세요.

- >**Begin with a summary** that describes the entity being declared.   
    Often, an API can be completely understood from its declaration and its summary.

    선언된 개체를 설명하는 **요약부터 시작**하세요.
    종종, API는 선언과 요약을 읽는 것만으로도 이해가 되는 경우가 있습니다.

    ```Swift
    /// Returns a "view" of `self` containing the same elements in
    /// reverse order.
    func reversed() -> ReverseCollection
    ```
    - > Focus on the summary; it’s the most important part.   
        Many excellent documentation comments consist of nothing more than a great summary.
    
        **요약에 집중하세요.** 요약은 가장 중요한 부분입니다.   
        좋은 문서의 주석들은 훌륭한 요약으로 이루어져 있습니다.
    
    - >**Use a single sentence fragment** if possible, ending with a period.   
        Do not use a complete sentence.

        **가능하다면, 한 문장 구성 단위(구, 절)를 사용하고 끝에 마침표(.)로 끝내세요.**   
        완전한 문장을 사용하지 마십시오.

    - >**Describe what a function or method does and what it returns,**   
        omitting null effects and Void returns:

        **함수 또는 메서드가 하는 일은 무엇이고, 어떤 것을 반환하는지 설명하고**   
        null 효과와 Void 반환에 대한 설명은 생략합니다.

        ```Swift
        /// Inserts `newHead` at the beginning of `self`.
        /// 'self'의 시작부분에 'newHead' 삽입
        mutating func prepend(_ newHead: Int)

        /// Returns a `List` containing `head` followed by the elements
        /// of `self`.
        /// 'self'의 요소에 있는 'head'가 포함 된 'List' 반환
        func prepending(_ head: Element) -> List

        /// Removes and returns the first element of `self` if non-empty;
        /// returns `nil` otherwise.
        /// 비어있지 않다면 'self'의 첫 번째 요소를 반환 및 제거하고, 비어있다면 'nil' 반환
        mutating func popFirst() -> Element?
        ```
        Note: in rare cases like popFirst above, the summary is formed of multiple sentence fragments separated by semicolons.   
        주의: 위의 `popFirst`와 같이 드문 경우에서, 요약은 세미콜론(;)을 이용해 여러 문장 구성 단위(구, 절) 형태로 요약을 작성할 수 있습니다.
    
    - >**Describe what a subscript accesses:**   
        
        **subscript가 어디에 접근하는 지 설명합니다.**
        ```Swift
        /// Accesses the `index`th element.
        /// 'index' 번째 요소에 접근한다.
        subscript(index: Int) -> Element { get set }
        ```
    
    - >**Describe what an initializer creates:**

        **이니셜라이저가 무엇을 생성하는 지 설명합니다.**
        ```Swift
        /// Creates an instance containing `n` repetitions of `x`.
        /// 'x'를 'n'번 반복하는 인스턴스를 생성합니다.
        init(count n: Int, repeatedElement x: Element)
        ```

    - >For all other declarations, **describe what the declared entity is.**

        다른 모든 선언의 경우, 선언된 개체가 무엇인지 설명합니다.
        ```Swift
        /// A collection that supports equally efficient insertion/removal
        /// at any position.
        /// 어느 위치에서도 동일하고 효율적으로 삽입/제거가 가능한 컬렉션
        struct List {

        /// The element at the beginning of `self`, or `nil` if self is
        /// empty.
        /// 'self'의 첫 번째 요소가 비어있거나 self가 비어있다면 'nil'
        var first: Element?
        ...
        ```

- >**Optionally, continue** with one or more paragraphs and bullet items.   
    Paragraphs are separated by blank lines and use complete sentences.
  
  **경우에 따라, 한 개 이상의 단락(절)과 글머리 기호로 이어갈 수 있습니다.**   
  단락(절)은 빈 줄로 구분하고 완벽한 문장을 사용합니다.

  ```Swift
    /// Writes the textual representation of each    ← Summary
    /// element of `items` to the standard output.
    /// 표준 출력에 'items'의 각 요소에 대한 텍스트 표현을 작성합니다.
    ///                                              ← Blank line
    /// The textual representation for each item `x` ← Additional discussion
    /// is generated by the expression `String(x)`.
    /// 각 요소인 'x'에 대한 텍스트 표현은 'String(x)'표현식에 의해 만들어집니다.
    ///
    /// - Parameter separator: text to be printed    ⎫
    ///   between items.                             ⎟
    /// - 매개변수 separator: 요소 사이에 출력되는 텍스트     |
    /// - Parameter terminator: text to be printed   ⎬ Parameters section (매개변수 부분)
    ///   at the end.                                ⎟
    /// - 매개변수 terminator: 끝부분에 출력되는 텍스트      |
    ///                                              ⎭
    /// - Note: To print without a trailing          ⎫
    ///   newline, pass `terminator: ""`             ⎟
    /// - 주의: 줄 바꿈을 하지 않으려면 'terminater: ""'입력 |
    ///                                              ⎬ Symbol commands (기호 명령)
    /// - SeeAlso: `CustomDebugStringConvertible`,   ⎟
    ///   `CustomStringConvertible`, `debugPrint`.   ⎭
    public func print(
    _ items: Any..., separator: String = " ", terminator: String = "\n")
  ```
    ### 🔎 More Detail
    - >**Use recognized** [symbol documentation markup](https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/SymbolDocumentation.html#//apple_ref/doc/uid/TP40016497-CH51-SW1) **elements** to add information beyond the summary, whenever appropriate.   
    
        요약문 외에 추가적인 정보를 제공할 때는 적절하게 [심볼 문서 마크업](https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/SymbolDocumentation.html#//apple_ref/doc/uid/TP40016497-CH51-SW1)**요소들을 사용하세요.**
    
    - >**Know and use recognized bullet items with** [symbol command syntax](https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/SymbolDocumentation.html#//apple_ref/doc/uid/TP40016497-CH51-SW13).   
    Popular development tools such as Xcode give special treatment to bullet items that start with the following keywords:

        **글머리 기호와 [심볼 명령 구문](https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/SymbolDocumentation.html#//apple_ref/doc/uid/TP40016497-CH51-SW13)을 알고 사용합니다.**   
        Xcode처럼 인기있는 개발 도구는 아래의 키워드로 시작하는 글머리 기호를 특별하게 취급합니다.   
        |Attention|Author|Authors|Bug|
        |:---|:---|:---|:---|
        |Complexity|Copyright|Date|Experiment|
        |Important|Invariant|Note|Parameter|
        |Parameters|Postcondition|Precondition|Remark|
        |Requires|Returns|SeeAlso|Since|
        |Throws|ToDo|Version|Warning|
---

## 📗 Naming

## 📘 Conventions

## 📙 Special Instructions