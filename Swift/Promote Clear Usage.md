# Promote Clear Usage (명확하게 사용하기)
- >**Include all the words needed to avoid ambiguity** for a person reading code where the name is used.   

    이름이 사용된 코드를 읽는 사람들을 위해 **모호함으로 혼동을 주지 않도록 필요한 모든 단어를 포함합니다.**
    
    ## 🔎 MORE DETAIL
    > For example, consider a method that removes the element at a given position within a collection.   

    예를 들어, 컬렉션 내 주어진 위치에 있는 요소를 제거하는 메서드를 고려합니다.   
    ```Swift
    ✅
    extension List {
        public mutating func remove(at position: Index) -> Element
    }
    employees.remove(at: x)
    ```
    If we were to omit the word at from the method signature,   
    it could imply to the reader that the method searches for and removes an element equal to x,   
    rather than using to x to indicate the position of the element to remove.   
    ```Swift
    ⛔️
    employees.remove(x) // unclear: are we removing x?
    ```
    메서드 서명에서 `at`이라는 단어를 생략한다면,   
    독자에게 제거할 요소의 위치를 나타내기 위해 x를 사용했다고 보여지기보다는   
    x와 같은 요소를 검색하고 제거하는다는 의미로 오역될 수 있습니다.   
---
- >**Omit needless words.**   
    Every word in a name should convery salient information at the use site.   

    **불필요한 단어는 생략합니다.**   
    이름의 모든 단어는 사용 장소에서 중요한 정보를 전달해야합니다.

    ## 🔎 MORE DETAIL
    > More words may be needed to clarify intent or disambiguate meaning,   
    but those that are redundant with information the reader already possesses should be omitted.   
    In particular, omit words that merely repeat type information.

    ```Swift
    ⛔️ 
    public mutating func removeElement(_ member: Element) -> Element?
    
    allViews.removeElement(cancelButton)
    ```

    > In this case, the word Element adds nothing salient at the call site.   
    This API would be better:

    ```Swift
    ✅
    public mutating func remove(_ member: Element) -> Element?

    allViews.remove(cancelButton)
    ```

    > Occasionally, repeating type information is necessary to avoid ambiguity,   
    but in general it is better to use a word that describes a parameter's role rather than its type.   
    See the next item for details.

---
- >**Name variables, parameters, and associated types according to their roles,** rather than their type constraints.   

    타입 제약이 아닌 **해당 역할에 따라 변수, 매개변수, 그리고 연관된 타입의 이름을 붙입니다.**

- >**Compensate for weak type information** to clarify a parameter's role.   

    매개변수의 역할을 명확하게 하기 위하여 **약한 정보 타입을 보완합니다.**

