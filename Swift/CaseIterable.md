# CaseIterable
Swift4.2 버전부터 `CaseIterable` 프로토콜을 지원해주면서 아래와 같은 번거러운 코드 작성을 피할 수 있게 되었다.   

```Swift
// CaseIterable 지원 X
enum Fruits {
    case strawberry
    case kiwi
    case mango
    case pineapple

    static var allFruits: [Fruits] {
        return [.strawberry, .kiwi, .mango, .pineapple]
    }
}

// CaseIterable 채택 시
enum Fruits: CaseIterable {
    case strawberry
    case kiwi
    case mango
    case pineapple
}

let caseList = Fruits.allCases.map({ "\($0)" }).joined(separator: ", ")
// caseList = "strawberry, kiwi, mango, pineapple"
```

## 그렇다면 CaseIterable의 역할은??
"어떤 컬렉션의 모든 값들을 제공하는 타입"의 프로토콜로 CaseIterable 프로토콜을 채택하면,   
`allCases`라는 프로퍼티를 통해 모든 케이스의 값을 가져올 수 있다.   
하여, 코드를 작성하다가 케이스를 누락할 일이 없다!

### 🌐 Reference Site
[CaseIterable | Apple Developer Documentation](https://developer.apple.com/documentation/swift/caseiterable)   
[[Swift] CaseIterable](https://hello-developer.tistory.com/67)   