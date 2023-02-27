# LocalizaedError
오류에 대한 발생 이유를 설명하는 오류 프로토콜   
해당 프로토콜을 준수하고, 아래 computed property를 정의하면 호출부에서 .localizedDescription 사용이 가능

```Swift
extension LocalizedError {

    /// A localized message describing what error occurred.
    public var errorDescription: String? { get }

    /// A localized message describing the reason for the failure.
    public var failureReason: String? { get }

    /// A localized message describing how one might recover from the failure.
    public var recoverySuggestion: String? { get }

    /// A localized message providing "help" text if the user requests help.
    public var helpAnchor: String? { get }
}
```

## 프로젝트에 적용하여 실습
```Swift
enum Errors: LocalizedError {
    case invalidUserInput
    case failOfFormatToString
    
    var errorDescription: String? {
        return NSLocalizedString("Error Type: \(self)", comment: "")
    }
}
```

```Swift
guard let totalSpend = numberFormatter.string(for: totalLeadTime) else {
            return Errors.failOfFormatToString.localizedDescription
        }
```

### 🌐 Reference Site
[[iOS - swift] Error, LocalizedError, localizedDescription 개념](https://ios-development.tistory.com/849)   
[LocalizedError | Apple Developer Documentation](https://developer.apple.com/documentation/foundation/localizederror)