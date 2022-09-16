# UIButton Configuration
버튼과 그 내용의 모양과 동작을 지정하는 구성입니다.
버튼 구성에는 `setTitle(_: for:)`과 같은 다른 메서드에서 사용할 수 있는 모든 사용자 지정 옵션이 포함되어 있으며 이러한 메서드를 대체할 수 있습니다.

### Creating configurations
- static func plain() -> UIButton.Configuration
- static func gray() -> UIButton.Configuration
- static func tinted() -> UIButton.Configuration
- static func filled() -> UIButton.Configuration
- static func borderless() -> UIButton.Configuration
- static func bordered() -> UIButton.Configuration
- static func borderedTinted() -> UIButton.Configuration
- static func borderedProminent() -> UIButton
- func updated(for: UIButton) -> UIButton.Configuration
  
### Configuring titles
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

### Configuration images
### Configuration layout
### Configuration button colors
### Configuration the button background
### Configuration the indicator
### Configuration selection behavior
### Configuration the appearance on macOS
### Conparing configurations

### 🌐 참고사이트  
[UIButton.Configuration | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uibutton/configuration)    