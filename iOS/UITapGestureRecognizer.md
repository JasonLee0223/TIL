# UITabGestureRecognizer
- User Interactions   
    - Standard gestures   
      - UITapGestureRecognizer   

위 하위 목록으로 확인할 수 있으며 `단일 또는 다중 탭을 해석하는 개별 제스처 인식기이다.`
UITapGestureRecognizer는 UIGestureRecognizer의 구체적인 하위 클래스(상속클래스)이다.   
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

## Configuring the gesture
```Swift
// 제스처 인식을 위해 사용자가 눌러야 하는 버튼의 비트마스크
var buttonMaskRequired: UIEvent.ButtonMask

// 제스처 인식에 필요한 탭 수
var numberOfTapsRequired: Int

// 제스처 인식을 위해 사용자가 탭해야 하는 손가락의 수
var numberOfTouchesRequired: Int
```

## 사용법1
UITapGestureRecognizer를 사용하기 위해서는 UIGestureRecognizerDelegate를 채택해야한다.   
제스처에 대한 처리를 ViewController에서 위임(delegate)받아 정의하기 위해서이다.
```Swift
extenstion ViewController: UIGestureRecognizerDelegate {
    func gestureRecognizer(_ gestureRecognizer: UIGestureRecognizer, shouldReceivetouch: UITouch) -> Bool {
        return true
    }
}
```
추가적으로 `viewDidLoad`에 TapGestureRecognizer를 추가해주는 작업을 설정한다.
```Swift
class ViewController: UIViewController {
    @IBOutlet weak var resultLabel: UILabel!

    override func viewDidLoad() {
        super.viewDidLoad()

        let tapGestureRecognizer = UITapGestureRecognizer()
        tapGestureRecognizer.delegate = self
        self.view.addGestureRecognizer(tapGestureRecognizer)
    }
}
```
이후 gestureRecognizer 메서드에 정의해주면 된다.
```Swift
extenstion ViewController: UIGestureRecognizerDelegate {
    func gestureRecognizer(_ gestureRecognizer: UIGestureRecognizer, shouldReceivetouch: UITouch) -> Bool {
        resultLabel.text = (self.view.hitTest(touch.location(in: self.view), with: nil) as? UILabel)?.text ?? "NONE"
        resultLabel.sizeToFit()
        return true
    }
}
```

## 사용법2
- UITapGestureRecognizer 인스턴스를 `init(target: action:)`메서드를 호출해 초기화한다.   
  🔴 초기화는 `UIGestureRecognizer`를 통해 작성된다.   

```Swift
// MARK: - View Life Cycle

override func viewDidLoad() {
    super.viewDidLoad()

    // Initialize Tap Gesture Recognizer
    let tapGestureRecognizer = UITapGestureRecognizer(target: self, action: #selector(didTapView(_:)))

    // Configure Tap Gesture Recognizer -> 다중탭을 지원하는 프로퍼티
    tapGestureRecognizer.numberOfTapsRequired = 2

    // Add Tap Gesture Recognizer
    tappableView.addGestureRecognizer(tapGestureRecognizer)
}

// MARK: - Actions

@objc func didTapView(_ sender: UITapGestureRecognizer) {
    print("did tap view", sender)
}
```

### 참고사이트 🌐
[UITapGestureRecognizer | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uitapgesturerecognizer)   
[UIGestureRecognizer | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uigesturerecognizer)   
[Working with Tap Gesture Recognizers in Swift](https://cocoacasts.com/swift-fundamentals-working-with-tap-gesture-recognizers-in-swift)   
[[iOS, Swift] UITapGestureRecognizer 탭 제스처 인식기](https://velog.io/@bibi6666667/iOS-Swift-UITapGestureRecognizer-%ED%83%AD-%EC%A0%9C%EC%8A%A4%EC%B2%98-%EC%9D%B8%EC%8B%9D%EA%B8%B0)   
[[iOS]UITapGestureRecognizer: 화면 탭 동작 인식하기](https://jeonyeohun.tistory.com/218)   