# Hashable
Set을 사용하다보니 접하게 된 Hashable...    

## Hashable?? 그럼 Hash가 뭔 뜻이야??
사전적의미를 알아보기위해 서칭한 결과   
<img src = "https://user-images.githubusercontent.com/92699723/209934047-50571903-cd3d-4165-ac6b-6e701e64dd33.png" width="300" height="100">   
설마.. 내가 아는 그 해쉬포테이토..?? 이 Hash를 알려고 한 건 아닌데..   

Hash란 `다양한 길이를 가진 데이터를 고정된 길이를 가진 데이터로 매핑(mapping)한 값`이다.   
이를 이용해 특정한 배열의 인덱스나 위치나 위치를 입력하고자 하는 데이터의 값을 이용해 저장하거나 찾을 수 있다.   
기존에 사용했던 자료 구조들은 탐색이나 삽입에 선형시간이 걸리기도 했던것에 비해,   
해시를 이용하면 `즉시 저장하거나 찾고자 하는 위치를 참조할 수 있으므로 더욱 빠른 속도로 처리할 수 있다.` 해시값이라고도 한다.   

## 그럼 Hash function은??
위에서 Hash의 뜻을 정의하다보니 의미가 중복되지만, `해시 함수는 문자열에 대해 숫자를 할당(Mapping)합니다.` 라는 뜻을 가지고 있다.   
해시 함수는 아래와 같은 요건을 갖추어야한다.   
- 해시 함수에는 일관성이 있어야한다.   
    즉, `같은 이름에 대해서는 항상 같은 인덱스를 할당합니다.`   
    예를 들어, 만약 "apple"을 넣었을 때 "4"를 반환한다면 "apple"을 넣을 때마다 반환되는 값은 항상 "4"이어야한다.
- 다른 단어가 들어가면 다른 숫자가 나와야한다.   
    즉, `다른 문자열에 대해서는 다른 인덱스를 할당합니다.`
    예를 들어, 어떤 단어를 넣어도 "1"만 나온다면 좋은 해시 함수가 아니다.   
    가장 좋은 경우는 서로 다른 단어에 대해 모두 서로 다른 숫자가 나와야한다.   

위 내용을 종합해보면, 해시 함수는 우리가 배열이 얼마나 큰지 알고 있어야 하며,   
유효한 인덱스만 반환해야한다.
이렇게 **`해시 함수와 배열을 합치면 해시 테이블(Hash table)이라고 하는 자료구조`** 를 얻을 수 있게된다.

## 타고.. 타고.. Hash Table??
이미 흔히 봤던 Swift에서의 Collection Type중에서 `Dictionary`와 `Set`을 떠올릴 수 있다.   
```Swift
// Dictionary
@frozen struct Dictionary<Key, Value> where Key : Hashable

// Set 
@frozen struct Set<Element> where Element : Hashable
```
2가지의 Collection Type 모두 Hashable 프로토콜을 채택하고있다.   
먼저 딕셔너리가 해시 테이블로 구현되어 있기 때문에, 해시 테이블도 당연히 Key - Value로 값을 저장하고 해시 테이블은 내부적으론 배열로 구현이 되어 있음!!   
즉 `Key 값을 해싱 함수에 넣어 해시하여 배열의 주소값(해시 주소값)을 얻고, 그 주소값에 맞는 index에 Value값을 저장`한다는 것이다.   

## 이제 진짜 Hashable!!!
Hashable 프로토콜은 아래와 같이 구성되어 있다.   
```Swift
public protocol Hashable: Equatable {
    var hashValue: Int { get }
    func hash(into hasher: inout Hasher)
}
```
- hashValue는 더이상 사용하지 않는 프로퍼티라고 하고, 필요할 경우 hash(into:) 함수를 직접 구현해야한다.
- Hashable은 자체적으로 Equtable이란 프로토콜을 준수하고 있다. (중요!)

## 🟢 Custom Type(struct, class, enum)에서의 Hashable 채택 방법
### 1️⃣ Struct의 경우
구조체의 경우 매우 간단하다.   
Equatable과 마찬가지로 만약 구조체 내 프로퍼티가 모두 기본 자료형이라면,   
Hashable을 채택하는 것만으로 추가 구현 없이 사용 가능하다.   
```Swift
struct ContactInformation: Hashable {
    let name: String
    let age: String
    let phoneNumber: String
}
```
정말 이게 다다.. 채택만 해주고 추가적인 구현은 없다!   
채택만 해주면 Dictionary와 Set에서 Hashable을 만족하기때문에 Key값으로 사용이 가능하다.   

### 2️⃣ Class의 경우
Equatable이 막 떠오른다...   
클래스는 Hashable이란 프로토콜을 준수하고!직접 hash함수를 구현해주어야 한다.   
```Swift
class ContactInformationContactInformation {
    let name = "jason"
    let age = 29
    let phoneNumber: 010-1111-1111
}
 
extension ContactInformationman: Hashable {
    func hash(into hasher: inout Hasher) {
        hasher.combine(name)
        hasher.combine(age)
        hasher.combine(phoneNumber)
    }
}
```
hash 메서드를 직접 구현해주는데, 이때 `hasher.combine`이란 메서드에 어떤 파라미터를 해시할 것인지를 넣어주는 것이다.   
주의사항을 보면 특별한 경우가 아니면 combine에는 해당 타입의 모든 저장 프로퍼티를 전달하는 것이다.   
또한, combine 파라미터로 전달하는 프로퍼티는 반드시 Hashable을 준수하고 있어야 한다.   
이게 끝인줄 알았다면... 첫 줄을 다시 보고와야한다...   
Hashable은 Equatable을 채택하고 있기 때문에, 자동으로 제공되지 않는 클래스의 경우 직접 구현해줘야한다.   
그럼 아래와 같이 최종적인 코드를 확인할 수 있게 된다.   
```Swift
class ContactInformation {
    let name = "jason"
    let age = 29
    let phoneNumber: 010-1111-1111
}
 
extension ContactInformationman: Hashable {
    static func == (lhs: ContactInformationman, rhs: ContactInformationman) -> Bool {
        return lhs.name == rhs.name && lhs.age == rhs.age && lhs.phoneNumber == rhs.phoneNumber
    }

    func hash(into hasher: inout Hasher) {
        hasher.combine(name)
        hasher.combine(age)
        hasher.combine(phoneNumber)
    }
}
```

### 3️⃣ Enum의 경우
Enum의 경우 2가지로 분리하여 볼 수 있다.   
1. 연관값이 있는 경우
Hashable을 채택하지 않고도 사용할 수 있다.   
```Swift
enum Gender {
    case male
}
```

2. 연관값이 없는 경우
```Swift
Hashable을 채택한다고 선언해주고, 연관값의 타입(Int)이 모두 Hashable을 채택(구현)하고 있어야한다.   
enum Gender: Hashable {
    case male(age: Int)
}
```

### 🌐 Reference Site
[해시 - 해시넷](http://wiki.hash.kr/index.php/%ED%95%B4%EC%8B%9C)   
[[Apple Developer] Hashable](https://developer.apple.com/documentation/swift/hashable)   
[Swift) 해시 테이블(Hash Table) 이해하기 - 개발자 소들이](https://babbab2.tistory.com/89)   
[Swift) Hashable에 대해 알아보자 - 개발자 소들이](https://babbab2.tistory.com/149)   