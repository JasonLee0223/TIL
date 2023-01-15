# UIStepper
> A control for incrementing or decrementing a value.   
값을 늘리거나 줄이는 컨트롤입니다.

## Declartaion
```Swift
@MainActor class UIStepper: UIControl
```
## OverView
기본적으로, Stepper의 버튼을 누르면 값이 반복적으로 증가하거나 줄어듭니다.   
**`변경 비율은 사용자가 컨트롤을 계속 누르고 있는 시간에 따라 달라집니다.`**   
위 동작을 해제하려면 `autorepeat` 속성을 `false`로 변경해야합니다.   

Stepper의 Maximum과 Minimum의 범위를 지정할 때 최대값은 최소값보다 크거나 같아야 합니다.   

## Configuring the stepper
```Swift
// 사용자가 버튼 누르고 있거나 손을 떼서 상호 작용이 종료된 후
// 값 변경 사항을 보낼지 여부를 결정하는 Bool값이다.
var isContinuous: Bool

// 사용자가 stepper 컨트롤 버튼을 누르고 있으면 stepper 값을 반복적으로
// 변경할 지 여부를 결정하는 Bool값이다. (위에서 언급)
var autorepeat: Bool

// 값을 늘리거나 줄일 때 stepper가 해당 값을 최소값 또는 최대값으로
// 래핑할 수 있는지 여부를 결정하는 Bool값이다.
var wraps: Bool

var minimumValue: Bool

var maximumValue: Bool

// stepper의 단계 또는 증가하는 값입니다.
var stepValue: Bool
```

## Accessing the stepper's value
```Swift
// stepper의 숫자 값입니다.
var value: Double
```

### 🌐 Reference Site
[UIStepper | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uistepper)   
[[iOS/UIKit] UIStepper Tutorial - 아리의 iOS 탐구생활 - 티스토리](https://leeari95.tistory.com/58)   