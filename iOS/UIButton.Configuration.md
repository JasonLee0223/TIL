# UIButton Configuration
버튼과 그 내용의 모양과 동작을 지정하는 구성입니다.
버튼 구성에는 `setTitle(_: for:)`과 같은 다른 메서드에서 사용할 수 있는 모든 사용자 지정 옵션이 포함되어 있으며 이러한 메서드를 대체할 수 있습니다.

## Creating configurations
- static func plain() -> UIButton.Configuration
- static func gray() -> UIButton.Configuration
- static func tinted() -> UIButton.Configuration
- static func filled() -> UIButton.Configuration
- static func borderless() -> UIButton.Configuration
- static func bordered() -> UIButton.Configuration
- static func borderedTinted() -> UIButton.Configuration
- static func borderedProminent() -> UIButton
- func updated(for: UIButton) -> UIButton.Configuration
  
## Configuring titles
- var title: String?
- var subtitle: String?
- var attributedTitle: AttributedString?
- var attributedSubtitle: AttributedString?
- var titlePadding: CGFloat
- var titleAlignment: UIButton.Configuration.TitleAlignment
- struct UIConfigurationTextAttributesTransformer
- var titleTextAttributesTransformer: UIConfigurationTextAttributesTransformer?
- var subtitleTextAttributesTransformer: UIConfigurationTextAttributesTransformer?
- enum UIButton.Configuration.TitleAlignment

## Configuration images
## Configuration layout
## Configuration button colors
## Configuration the button background
## Configuration the indicator
## Configuration selection behavior
## Configuration the appearance on macOS
## Conparing configurations

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