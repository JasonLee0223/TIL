# Parameters

```Swift
func move(from start: Point, to end: Point)
```
- **`문서화 할 수 있는 매개 변수 이름을 선택하라.`**   
  함수나 메서드를 사용할 때 매개변수가 감춰져있더라도 여전히 중요한 역할을 한다.
  - ✅ 다음과 같은 이름은 문서화해도 읽기 편하고, 문서로 만들어도 자연스럽다.
    ```Swift
    /// Return an `Array` containing the elements of `self`
    /// that satisfy `predicate`.
    func filter(_ predicate: (Element) -> Bool) -> [Generator.Element]

    /// Replace the given `subRange` of elements with `newElements`.
    mutating func replaceRange(_ subRange: Range, with newElements: [E])
    ```
  - ⛔️ 반면, 아래와 같은 표현은 문법도 안맞고, 불분명하다.
    ```Swift
    /// Return an `Array` containing the elements of `self`
    /// that satisfy `includedInResult`.
    func filter(_ includedInResult: (Element) -> Bool) -> [Generator.Element]

    /// Replace the range of elements indicated by `r` with
    /// the contents of `with`.
    mutating func replaceRange(_ r: Range, with: [E])
    ```
- **`매개변수 기본값을 지정해서 편리함을 더하라.`**   
  매개 변수에 흔히 넘기는 값 자체를 기본값으로 활용하라.
  - ⛔️ 불필요한 정보를 숨겨서 가독성을 높인다.
    ```Swift
    let order = lastName.compare(
    royalFamilyName, options: [], range: nil, locale: nil)
    ```
  - ✅ 위 코드를 아래와 같이 간단하게 표현할 수 있다.
    ```Swift
    let order = lastName.compare(royalFamilyName)
    ```
  - ✅ 기본 인자값을 사용하면 여러 메서드 패밀리를 표현하는 것보다 API를 이해하는데 더 낮은 비용이 들기 때문에 도움이 된다.
    ```Swift
    extension String {
    /// ...description...
    public func compare(
    _ other: String, options: CompareOptions = [],
    range: Range? = nil, locale: Locale? = nil
    ) -> Ordering
    }
    ```
  - ⛔️ 위 코드가 간단하지 않지만 아래보다 훨씬 간단합니다.
    ```Swift
    extension String {
    /// ...description 1...
    public func compare(_ other: String) -> Ordering
    /// ...description 2...
    public func compare(_ other: String, options: CompareOptions) -> Ordering
    /// ...description 3...
    public func compare(
    _ other: String, options: CompareOptions, range: Range) -> Ordering
    /// ...description 4...
    public func compare(
    _ other: String, options: StringCompareOptions,
    range: Range, locale: Locale) -> Ordering
    }
    ```
  - 이런 경우 메서드 패밀리의 모든 메서드를 각각 문서화하고 따로 이해해야 하는 부담이 생긴다.   
    `foo(bar: nil)`과 `foo()`는 동일한 표현이 아니라서 작은 차이로 문서로 확인해야 하는 불편함을 초래한다.   
    기본 인자값이 있는 하나의 메서드로 만드는게 더 좋은 개발 경험을 제공합나다.
- **`기본 인자값은 매개 변수 목록에서 마지막 위치부터 넣어라`**   
    기본 인자값이 없는 매개변수는 메서드에서 더 중요한 역할을 하고, 메서드를 호출하는 곳에서 안정적으로 초기화하는 형태로 사용할 수 있다.