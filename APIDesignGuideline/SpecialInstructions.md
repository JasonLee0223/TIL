# Special Instructions
- **`튜플 멤버에 레이블을, 클로저 매개변수에 이름을 표기하라.`**
  - 이렇게 이름을 붙이면 문서화를 위한 주석에 활용할 수 있고 튜플 멤버에 접근할 때도 편리하다.   
    ```Swift
    /// Ensure that we hold uniquely-referenced storage for at least
    /// `requestedCapacity` elements.
    ///
    /// If more storage is needed, `allocate` is called with
    /// `byteCount` equal to the number of maximally-aligned
    /// bytes to allocate.
    ///
    /// - Returns:
    ///   - reallocated: `true` iff a new block of memory
    ///     was allocated.
    ///   - capacityChanged: `true` iff `capacity` was updated.
    mutating func ensureUniqueStorage(
        minimumCapacity requestedCapacity: Int, 
        allocate: (_ byteCount: Int) -> UnsafePointer<Void>
    ) -> (reallocated: Bool, capacityChanged: Bool)
    ```
    클로저 매개변수에서 사용하는 이름은 최고 - 수준 함수의 **매개변수 이름** 수준과 맞춰서 선택한다.   
    호출 지점에서 표시하는 클로저 인자값 레이블은 지원하지 않는다.
- `Any`나 `AnyObject`, 제약없는 제네릭 매개변수처럼 **`제약없는 다형성(polymorphism)`** 은 오버로드할 때 혼동하지 않도록 주의하라.   
  - ⛔️ 다음과 같은 오버로드 형태는 좋지 않다.
    ```Swift
    struct Array {
    /// Inserts `newElement` at `self.endIndex`.
    public mutating func append(_ newElement: Element)

    /// Inserts the contents of `newElements`, in order, at
    /// `self.endIndex`.
    public mutating func append(_ newElements: S)
    where S.Generator.Element == Element
    }
    ```
  - ⛔️ 이런 메서드들은 의미상 동일한 형태를 갖고 인자값에 대한 타입이 명확하게 구분되는 것처럼 보인다.   
    하지만 `Element`가 `Any`인 경우에 하나의 요소 타입과 시퀀스 타입이 같은 타입일 수 있다.   
    ```Swift
    var values: [Any] = [1, "a"]
    values.append([2, 3, 4]) // [1, "a", [2, 3, 4]] or [1, "a", 2, 3, 4]?
    ```
  - ✅ 위처럼 모호한 경우를 피해가려면 두 번째 오버로드에 명시적으로 이름을 붙여주자.   
    ```Swift
    struct Array {
    /// Inserts `newElement` at `self.endIndex`.
    public mutating func append(_ newElement: Element)

    /// Inserts the contents of `newElements`, in order, at
    /// `self.endIndex`.
    public mutating func append(contentsOf newElements: S)
    where S.Generator.Element == Element
    }
    ```
    새로운 이름이 주석에 문서 내용과 얼마나 더 잘 일치하는지 살펴보라.   
    이처럼 주석에 설명을 작성하는 것도 API 작성자가 집중해야 하는 일이다.