# readLine()
사용자가 입력하는 다양한 값을 받기 위한 메서드로 알고리즘 풀이 또는 과제 제출할 때 자주 사용되어 정리해보고자했다.   

💡 공식 문서를 확인해보면, 표준 입력을 받아 `"문자열"`로 반환한다는 것을 알 수 있다.   
여기서 핵심은 **사용자가 Int, Double 등 여러 타입으로 입력하던 간에, 모두 `String`으로 반환한다.**   
하여 이 점에 주의하여 입력한 데이터를 요구사항에 맞게 데이터 타입을 변환하여 사용해야한다.   

```Swift
// Declaration
func readline(strippingNewline: Bool = true) -> String?
```
또한 리턴타입이 `String?`으로 Optional 타입이여서 값을 입력하지 않아 발생하는 nil의 경우도 생각해야한다.   
하여 Unrapping을 해줘야하는데, 강제 언래핑이 아닌 Optional Binding을 활용한다.
```Swift
if let userInput = readLine() {
    print(input)
}

// Early Exit
guard let userInput = readLine() else {
    return
}
print(userInput)
```

### 🌐 Reference Site
[readLine(strippingNewline:) | Apple Developer Documentation](https://developer.apple.com/documentation/swift/readline(strippingnewline:))   
[[Swift] 스위프트 readLine() 파헤치기](https://leechamin.tistory.com/402)