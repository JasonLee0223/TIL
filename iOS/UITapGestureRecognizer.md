# UITabGestureRecognizer
- User Interactions   
    - Standard gestures   
      - UITapGestureRecognizer   

위 하위 목록으로 확인할 수 있으며 `단일 또는 다중 탭을 해석하는 개별 제스처 인식기이다.`
UITapGestureRecognizer는 UIGestureRecognizer의 구체적인 하위 클래스이다.   
제스처 인식의 경우 지정된 수의 손가락으로 지정된 횟수만큼 View를 탭해야한다.
`시스템은 제스처가 시작될 때 관련된 action message(작업 메시지)를 보낸 다음 제스처의 종료 상태까지(포함하는) 각 중간 상태에 대해 다시 보냅니다.`   
탭 제스처를 처리하는 코드는 제스처의 상태를 테스트해야한다. 예를 들면 아래와 같다.
```Swift
func handleTap(sender: UITapGestureRecognizer) {
    if sender.state == .ended {
        // handling code
    }
}
```

## 사용법

### 참고사이트 🌐
[UITapGestureRecognizer | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uitapgesturerecognizer)   
[UIGestureRecognizer | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uigesturerecognizer)   
[Working with Tap Gesture Recognizers in Swift](https://cocoacasts.com/swift-fundamentals-working-with-tap-gesture-recognizers-in-swift)   
[[iOS, Swift] UITapGestureRecognizer 탭 제스처 인식기](https://velog.io/@bibi6666667/iOS-Swift-UITapGestureRecognizer-%ED%83%AD-%EC%A0%9C%EC%8A%A4%EC%B2%98-%EC%9D%B8%EC%8B%9D%EA%B8%B0)   
[[iOS]UITapGestureRecognizer: 화면 탭 동작 인식하기](https://jeonyeohun.tistory.com/218)   