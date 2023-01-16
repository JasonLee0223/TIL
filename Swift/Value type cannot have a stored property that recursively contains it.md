# Value type cannot have a stored property that recursively contains it
값 유형(Value type)은 재귀적으로 포함하는 저장 프로퍼티를 가질 수 없습니다.

## Linked List를 사용해보면서 생긴 오류
Linked List를 학습해보다 `Node`를 `class`를 사용하여 많이 구현하여   
struct으로 구현해보려고 시도하다 운이 좋게? class와 struct의 메모리 구조에 대해   
한 번 더 고민해볼 수 있게되었다.
```Swift
struct Node {
    var next: Node?
    var data: Double
}
```
위와 같이 구현해보려고 하였더니 아래의 에러 메세지를 확인 할 수 있었다.
<img src = "https://user-images.githubusercontent.com/92699723/212640907-20a583ad-5937-45af-a9d8-8f564cc37ff0.png">

## Article 정리
Swift에서 위 오류는 자신을 재귀적으로 호출하는 Value type을 빌드하려고 할 때 발생합니다.   
Value Type은 고정된 구조이기 때문에 불가능합니다.   
**`즉, 메모리의 고정된 위치에 저장되며 컴파일러는 Compile Time에 고정 구조의 값을 계산할 수 있을 것으로 예상합니다.`**   

위 처럼 자신을 재귀적으로 호출하는 Value Type을 사용하면   
`컴파일 시간 전에 초기화되지 않기 때문에 컴파일러는 해당 형식에 대한 재귀적으로 호출된 참조의 값을 계산할 수 없습니다.`   
컴파일러는 Value Type의 속성이 포함할 공간의 크기를 알아야 합니다!   

### 🤔 무엇을 수정해야할까??
위 에러를 해결하려면 구조가 메모리에 저장되는 위치를 알아야 합니다.   
**`구조체는 Heap이 아닌 Stack에 저장됩니다.`**   
**Stack은 정적 메모리(Static Memory)할당에 사용되는 반면 Heap은 동적 메모리(Dynamic Memory)할당에 사용됩니다.**   

Stack은 Compile Time에 메모리를 할당하므로 구조의 값이 알려질 것으로 예상됩니다.   
그러하여 메모리를 적절하게 할당할 수 있습니다.   
수정하면 Struct 대신에 class를 사용하는 것입니다!   

위에 언급했듯이 Dynamic Memory Allocation로 사용되는 class가 Heap에 저장됩니다.   
Heap은 Runtime Memory를 할당하므로 Swift 컴파일러는 값이 차지하는 공간을 알 필요가 없습니다.   

### 🌐 Refercen Site
[Value type cannot have a stored property that recursively contains it](https://andrew-lundy.medium.com/value-type-cannot-have-a-stored-property-that-recursively-contains-it-6e6128e24d1d)   

추후 좀 더 학습해볼 내용   
[Struct cannot have stored property that references itself but it can have an array of the same type [duplicate]](https://stackoverflow.com/questions/53626802/struct-cannot-have-stored-property-that-references-itself-but-it-can-have-an-arr)