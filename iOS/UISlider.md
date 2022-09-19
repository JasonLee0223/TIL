# UISlider
값의 연속 범위에서 단일 값을 선택하기 위한 컨트롤

슬라이더의 엄지를 움직이면, 업데이트된 값이 연결된 모든 작업에 전달된다.    
<img src="https://user-images.githubusercontent.com/92699723/190950515-e579111c-7e57-4a00-93b1-65ef652c5889.png" width="400" height="150">

인터페이스에 슬라이더를 추가하려면
- 슬라이더가 나타내는 값의 범위를 지정해야한다.(Minimum ~ Maximum)
- 선택적으로 적절한 색조 색상으로 슬라이더의 모양을 구성한다.
- 슬라이더에 하나 이상의 작업 방법을 연결한다.
- 슬라이더의 크기와 위치를 제어하는 Auto Layout 규칙을 설정한다.

## Accessing the slider's value
```Swift
// 슬라이더의 현재 값
var value: Float

// 슬라이더의 현재 값을 설정하여 변경 사항을 시각적으로 애니메이션을 준다.
func setValue(Float, animated: Bool)
```

## Accessing the slider's value limits
```Swift
// 슬라이더 최소값
var minimumValue: Float

// 슬라이더 최대값
var maximumValue: Float
```

## Modifying the slider's behavior (슬라이더 동작 수정)
```Swift
// 슬라이더 값의 변경이 지속적인 업데이트 이벤트를 생성하는지 여부를 나타내는 Bool 값.
var isContinuous: Bool

// 슬라이더가 작동하는 방식을 결정하는 스타일.
var behavioralStyle: UIBehavioralStyle

// 선호하는 행동 스타일.
var preferredBehavioralStyle: UIBehavioralStyle

// Mac Catalyst로 빌드된 앱에서 컨트롤이 작동하는 방식을 나타내는 상수.
enum UIBehavioralStyle {
    case automatic
    case pad
    case mac
}
```

## 🔴 Changing the slider's appearance (슬라이더 모양 변경)
```Swift
// 슬라이더의 최소값을 나타내는 이미지 설정.
var minimumValueImage: UIImage?

// 슬라이더의 최대값을 나타내는 이미지.
var maximumValueImage: UIImage?

// 기본 최소 트랙 이미지에 색조를 지정하는 데 사용되는 색상.
var minimumTrackTintColor: UIColor?

// 슬라이더를 렌더링하는 데 현재 사용 중인 최소 트랙 이미지.
var currentMinimumTrackImage: UIImage?

// 지정된 제어 상태와 관련된 최소 트랙 이미지를 반환한다.
func minimumTrackImage(for: UIControl.State) -> UIImage?

// 지정된 제어 상태에 최소 트랙 이미지를 할당한다.
func setMinimumTrackImage(UIImage?, for: UIControl.State)

// 기본 최대 트랙 이미지에 색조를 지정하는 데 사용되는 색상.
var maximumTrackTintColor: UIColor?

// 슬라이더를 렌더링하는 데 현재 사용 중인 최대 트랙 이미지를 포함한다.
var currentMaximumTrackImage: UIImage?

// 지정된 제어 상태와 관련된 최대 트랙 이미지를 반환한다.
func maximumTrackImage(for: UIControl.State) -> UIImage?

// 지정된 제어 상태에 최대 트랙 이미지를 할당한다.
func setMaximumTrackImage(UIImage?, for: UIControl.State)

// 기본 thumb(엄지모양) 이미지에 색조를 지정하는 데 사용되는 색상.
var thumbTintColor: UIColor?

// 슬라이더를 렌더링하는 데 현재 사용 중인 thumb(엄지모양) 이미지.
var currentThumbImage: UIImage?

// 지정된 제어 상태와 관련된 thumb(엄지모양) 이미지를 반환한다.
func thumbImage(for: UIControl.State) -> UIImage?

// 지정된 제어 상태에 thumb(엄지모양) 이미지를 할당한다.
func setThumbImage(UIImage?, for: UIControl.State)
```

## Overrides for subclasses (하위 클래스에 대한 재정의)
```Swift
// 최대값 이미지에 대한 그리기 사각형을 반환한다.
func maximumValueImageRect(forBounds: CGRect) -> CGRect

// 최소값 이미지에 대한 그리기 사각형을 반환한다.
func minimumValueImageRect(forBounds: CGRect) -> CGRect

// 슬라이더의 트랙에 대한 그리기 사각형을 반환한다.
func trackRect(forBounds: CGRect) -> CGRect

// 슬라이더의 썸 이미지에 대한 그리기 사각형을 반환한다.
func thumbRect(forBounds: CGRect, trackRect: CGRect, value: Float) -> CGRect
```

## Example
```Swift
let slider: UISlider = {
    // Create a Slider
    let slider = UISlider()
    // slider.backgroundColor = UIColor.yellow
    
    // Set the values
    slider.minimumValue = 1
    slider.maximumValue = 10
    
    // Set the position of Slider
    slider.value = 1
    slider.thumbTintColor = UIColor.black
    slider.maximumTrackTintColor = UIColor.lightGray
    slider.minimumTrackTintColor = UIColor.systemGray3
    
    // addTarget을 설정해줘야한다.
    slider.translatesAutoresizingMaskIntoConstraints = false
    return slider
}()
```

### 참고사이트
[UISlider | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uislider)    
[[iOS UIKit in Swift 4] UISlider 사용하기](https://calmone.tistory.com/entry/iOS-UIKit-in-Swift-4-UISlider-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)