# UIButton Configuration
버튼과 그 내용의 모양과 동작을 지정하는 구성입니다.
버튼 구성에는 `setTitle(_: for:)`과 같은 다른 메서드에서 사용할 수 있는 모든 사용자 지정 옵션이 포함되어 있으며 이러한 메서드를 대체할 수 있습니다.

iOS15로 업데이트되면서 기존에 UIButton을 정의하는 방법이 늘어났다.
```Swift
// 기존 버튼 객체 생성
let button = UIButton()
button.backgroundColor = .gray

// 업데이트 이후, UIButton.Configuration in iOS 15
// Configuration을 정의하여 담을 수 있는 변수를 생성하여 UIButton을 생성
var config = UIButton.Configuration.plain()
config.baseBackgroundColor = .blue
let button = UIButton(configuration: config)
```

## Creating configurations
```Swift
// 배경이 투명한 버튼 생성
static func plain() -> UIButton.Configuration   

// 회색 배경의 버튼 생성
static func gray() -> UIButton.Configuration  

// 색조가 있는 배경색으로 단추에 대한 구성을 만듬  
static func tinted() -> UIButton.Configuration    

// 버튼의 색조 색상으로 채워진 배경이 있는 버튼 생성
static func filled() -> UIButton.Configuration    

// 테두리 없는 스타일의 버튼 생성
static func borderless() -> UIButton.Configuration    

// 테두리 스타일이 있는 버튼 생성
static func bordered() -> UIButton.Configuration  

// 색조와 테두리가 있는 스타일의 단추에 대한 구성을 만듬 
static func borderedTinted() -> UIButton.Configuration    

// 눈에 띄는 테두리 스타일이 있는 버튼 생성
static func borderedProminent() -> UIButton   

// 주어진 버튼에 대해 업데이트된 구성의 복사본을 반환
func updated(for: UIButton) -> UIButton.Configuration 
```
  
## Configuring titles
```Swift
var title: String?
var subtitle: String?
var attributedTitle: AttributedString?
var attributedSubtitle: AttributedString?

// title과 subtitle 레이블 사이의 거리
var titlePadding: CGFloat

// 버튼이 title과 subtitle을 배치하는데 사용하는 텍스트 정렬
var titleAlignment: UIButton.Configuration.TitleAlignment

// 문자열의 시각적 모양에 영향을 줄 수 있는 텍스트 변환을 정의합니다.
struct UIConfigurationTextAttributesTransformer { 
    let transformer = UIConfigurationTextAttributesTransformer { incoming in
    var outgoing = incoming
    outgoing.foregroundColor = UIColor.black
    outgoing.font = UIFont.boldSystemFont(ofSize: 20)
    return outgoing
    }
}

// 버튼 상태가 변경될 때 속성이 지정된 title을 업데이트하는 구조
var titleTextAttributesTransformer: UIConfigurationTextAttributesTransformer?

// 버튼 상태가 변경될 때 속성의 subtitle을 업데이트하는 구조
var subtitleTextAttributesTransformer: UIConfigurationTextAttributesTransformer?

// 버튼의 title과 subtitle을 정렬하는 방법을 지정
enum UIButton.Configuration.TitleAlignment { 
    case automatic
    case center
    case leading
    case trailing
}
```

## Configuration images
```Swift
var image: UIImage?

// 버튼의 이미지와 텍스트 사이의 거리입니다.
var imagePadding: CGFloat

// 버튼이 이미지를 배치하는 가장자리입니다.
var imagePlacement: NSDirectionalRectEdge

// 버튼 상태가 변경될 때 이미지 색상을 변환하는 블록입니다.
var imageColorTransformer: UIConfigurationColorTransformer?

// 버튼 기호 이미지에 대해 요청된 구성 개체입니다.
var preferredSymbolConfigurationForImage: UIImage.SymbolConfiguration?
```

## Configuration layout
```Swift
// 버튼의 기본 크기를 요청하는 크기입니다.
var buttonSize: UIButton.Configuration.Size

// 버튼 요소에 대해 미리 정의된 크기입니다.
enum UIButton.Configuration.Size { 
    case large
    case medium
    case small
    case mini
}

// 버튼의 콘텐츠 영역에서 경계까지의 거리입니다.
var contentInsets: NSDirectionalEdgeInsets

// 기본 콘텐츠 삽입을 복원합니다.
func setDefaultContentInsets()
```

## Configuration button colors
```Swift 
// 백그라운드의 색상 변경
var baseBackgroundColor: UIColor?

// 포어그라운드의 색상 변경
var baseForegroundColor: UIColor?
```

## Configuration the button background
```Swift 
// 버튼 배경을 사용자 지정하는 구성입니다.
var background: UIBackgroundConfiguration

// 배경 모서리 반경의 표시 동작을 제어하는 ​​버튼 스타일입니다.
var cornerStyle: UIButton.Configuration.CornerStyle

// 배경 모서리 반경의 모양을 결정하는 설정입니다.
enum UIButton.Configuration.CornerStyle {
    case dynamic
    case fixed
    case capsule
    case large
    case medium
    case small
}
```

## Configuration the indicator
```Swift 

```
## Configuration selection behavior
```Swift 

```
## Configuration the appearance on macOS
```Swift 

```
## Conparing configurations
```Swift 

```

### Example
```Swift
import UIKit

class DrawingView:UIView {
    
    override init(frame: CGRect) {
        super.init(frame: CGRect(x: 0, y: 0, width: 1166, height: 1024))
        layout()
    }
    
    required init?(coder: NSCoder) {
        super.init(coder: coder)
        
    }
    
    let createRectButton: UIButton = {
        var config = UIButton.Configuration.gray()
        config.buttonSize = .large
        config.contentInsets = NSDirectionalEdgeInsets(top: 16, leading: 16, bottom: 16, trailing: 16)
        
        var titleAttr = AttributedString.init(" ▢ ")
        titleAttr.font = .systemFont(ofSize: 35.0, weight: .heavy)
        config.attributedTitle = titleAttr
        
        var subtitleAttr = AttributedString.init(" 사각형 ")
        subtitleAttr.font = .systemFont(ofSize: 15.0, weight: .regular)
        config.attributedSubtitle = subtitleAttr
        
        let rectButton = UIButton(configuration: config)
        rectButton.frame = CGRect(x: 583, y: 930, width: 150, height: 93)
        return rectButton
    }()
}

extension DrawingView {
    func layout() {
        self.addSubview(createRectButton)
    }
}

```

### 🌐 참고사이트  
[UIButton.Configuration | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uibutton/configuration)    
[[iOS] UIButton Configuration 사용해보기 in iOS 15](https://velog.io/@wannabe_eung/iOS-UIButton-Configuration-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0-in-iOS-15)   
[iOS) UIButton.Configuration in iOS 15](https://gyuios.tistory.com/126)