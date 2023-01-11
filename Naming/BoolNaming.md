# ✏️ Bool 변수 이름 제대로 짓기 위한 최소한의 영문법

# Agenda
- is 용법
- 조동사 용법
- has 용법
- 동사원형 용법

## 🟢 is 용법
`is` 로 시작하는 변수명으로 가장 흔한 케이스
- is + 명사
- is + 현재진행형(~ing)
- is + 형용사

### 1️⃣ is + 명사
`(무엇)인가?`라는 뜻으로 쓰인다.

```swift
// UIView: "view의 자식인가?"
func isDescendant(of view: UIView) -> Bool
```
    
### 2️⃣ is + 현재진행형(~ing)
`~하는 중인가?` 라는 뜻이 필요할 때 쓰인다.

```swift
var isExecuting: Bool { get } // Operation: "오퍼레이션의 작업이 현재 실행중인가?"
var isPending: Bool { get } // MSMessage: "메세지가 보내지기 전 대기중인가?"
```
    
### 3️⃣ is + 형용사
- 이제부터 살짝 헷갈린다.
- 형용사도 2종류로 나뉘어진다.
    - `단어 자체가 형용사`인 것 - opaque, readable, visible 등
    - `과거분사 형태` - hidden, selected, highlighted, completed 등
- 과거분사(past participle)는 간단히 말해 `동사로 만든 형용사`

```swift
var isOpaque: Bool { get set }
var isSelected: Bool { get set }
var isHighlighted: Bool { get set }
var isHidden: Bool { get set }
```

### ❗️ 주의 ❗️   
**`가장 흔한 실수로 `is + 동사원형`을 사용하는 경우 (Ex. isAuthorize, isHide, isFind, etc...)`**

```swift
var isEdit: Bool
```
Edit이라는 단어가 명사로 쓰일수도 있어서 해석의 여지는 있지만 뜻이 명확하지 않아   
일반적으로 곧바로 해석하기 쉽지 않다. 하여 아래와 같이 적절하게 바꿔주면 해석이 더 쉽고 빠르다.   

```swift
var isEditable: Bool // 편집할 수 있는가?
var isEditing: Bool  // 편집 중인가?
var canEdit: Bool    //편집할 수 있는가?
```
---
## 🟢 조동사 용법    
`조동사(modal verb)`는 **`동사를 돕는 동사`** 란 뜻!   
can, should, will 등이 있고 주의할 점은 ‘조동사 + 동사원형’으로 써야한다는 것 하나 뿐이다.   

- can: “~할 수 있는가?”
- should, will: “~해야 하는가?” 혹은 “~할 것인가?”
- 등등

```swift
// UIResponder: first responder가 될 수 있는가?
var canBecomeFirstResponder: Bool { get }

// NSFetchRequest: 가져온 값을 refresh 할 것인가?
var shouldRefreshRefetchedObjects: Bool { get set }
```
--- 
## 🟢 has 용법
has로 시작하는 Bool 변수명은 상대적으로 빈도가 낮지만 뜻이 전혀 다르게 쓰이는 2가지가 있다.
- has + 명사
- has + 과거분사

has는 have의 3인칭 단수로, **has 다음 명사가 나오면 “~를 가지고 있는가?” 라는 뜻**이다.
```swift
// CKUserIdentity: 관련된 iCloud 계정을 가지고 있는가?
var hasiCloudAccount: Bool { get } 

// CXCallUpdate: 콜에 비디오가 포함되어 있는가?
var hasVideo: Bool { get set }
```
- has + 과거분사
모든 케이스를 통틀어 가장 덜 쓰이는 케이스 

---    
## 🟢 동사원형 용법
Bool 변수 짓기의 끝판왕...

### 주의❗️ 동사원형을 3인칭 단수로 써야한다는 것이다.
3인칭 단수는 보통 동사원형 뒤에 ‘-s’나 ‘-es’가 붙는 형태

- supports: ~을 지원하는가?
- includes: ~을 포함하는가?
- shows: ~을 보여줄 것인가?
- allows: ~을 허용할 것인가?
- accepts: ~을 받아 주는가?
- contains: ~을 포함하고 있는가?

```swift
var supportsVideo: Bool //CXProviderConfiguration: 비디오를 지원하는가?
var includesCallsInRecents: Bool //CXProviderConfiguration
var showsBackgroundLocationIndicator: Bool //CLLocationManager
var allowsEditing: Bool //CNContactViewController: 편집을 허용하는가?
var acceptsFirstResponder: Bool //NSResponder

var preservesSuperviewLayoutMargins: Bool //UIView
var returnsObjectsAsFaults: Bool //NSFetchRequest

//Core Location의 CLRegion 
var notifyOnEntry: Bool { get set }
var notifyOnExit: Bool { get set }
```

### ⚠️  3인칭 단수가 중요한 이유
코드 한 줄을 하나의 문장으로 비유하면 주어 역할을 하는 인스턴스가 3인칭 단수이기 때문에
문법적으로 꼭 써야하는 이유도 있지만,   
3인칭 단수로 쓰지 않을 경우 [스위프트 API 디자인 가이드](https://swift.org/documentation/api-design-guidelines/#strive-for-fluent-usage)
와의 일관성이 깨져서 코드를 읽는 사람을 혼란에 빠뜨릴 수 있다.

mutating 함수는 동사원형으로, nonmutating 함수는 동사 뒤에 -ed 또는 -ing를 붙여서 쓴다.

```swift
mutating func sort() -> Void //in-place sort
func sorted() -> [Element] //정렬된 새 배열을 리턴
```

```swift
let overlaps: Bool = region1.overlaps(region2) //region1과 region2가 겹치는가?
region1.overlap(region2) //region1을 region2와 겹치는 부분으로 mutate

let region3 = region1.overlapping(region2) 
//region1과 region2가 겹치는 부분만 새로운 region 인스턴스로 리턴
```

## 마무리
- is 용법
  - is + 명사
  - is + 현재진행형(~ing)
  - is + 형용사
  - `is + 동사원형 (절대 쓰면 안됨)`
- 조동사 용법
  - can, should, will 등
  - `조동사 + 동사원형`
- has 용법
  - has + 명사
  - has + 과거분사 (is + 과거분사와 의미 거의 동일)
- 동사원형 용법
  - `3인칭 단수`