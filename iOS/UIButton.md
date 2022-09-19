# UIButton
UIButton 클래스는 사용자의 상호 작용(Touch / Tab 등의 이벤트)에 반응해 미리 지정된 코드를 실행하는 컨트롤 요소이다.

💬 버튼 생성 3단계
1. 버튼을 생성하고 버튼의 유형을 선택한다.
2. 버튼을 나타내기 위한 Title을 입력하거나, 이미지를 설정한 뒤 크기를 조정한다.
3. 버튼에 특정 이벤트 발생 시 작동할 하나 이상의 method를 연결한다.

Button과 연결하는 방법
1. `addTarget(_: action: for:)` 메서드 사용
2. UIAction을 이용
3. 인터페이스 빌더(Storyboard)에서 연결(@IBAction)

## Creating buttons
```Swift
// 지정된 프레임으로 새 버튼을 생성한다.
init(frame: CGRect)

// 지정된 프레임으로 새 버튼을 생성하고, action 이벤트를 등록하여 title과 image를 액션에 맞게 설정한다.
init(frame: CGRect, primaryAction: UIAction?)

// unarchiver의 데이터로 새 버튼을 생성한다.
init?(coder: NSCoder)
```

## Creating buttons of a specific type (특정 유형)
```Swift
init(type: UIButton.ButtonType)

init(type: UIButton.ButtonType, primaryAction: UIAction?)

// 버튼의 스타일을 지정한다.
enum UIButton.ButtonType {
    case custom
    case system
    case detailDisclosure
    case infoLight
    case infoDark
    case contactAdd
    case plain
    case close
    static var roundedRect: UIButton.ButtonType
}
```

## Creating system buttons
```Swift
// 지정된 이미지, target 및 action으로 시스템 유형 버튼을 만들고 반환한다.
func systemButton(with: UIImage, target: Any?, action: Selector?) -> Self
```

## Creating buttons from a configuration object
```Swift
init(configuration: UIButton.Configuration, primaryAction: UIAction?)

struct UIButton.Configuration {
    // [UIButton.Configuration](UIButton.Configuration.md)
}
```

## 🔴 Managing the appearance with a configuration object
```Swift
var configuration: UIButton.Configuration?

// 버튼의 상태가 변경될 때 버튼 구성이 변경되는지 여부를 결정하는 Bool 값.
var automaticallyUpdatesConfiguration: Bool

// 시스템 업데이트 버튼 구성을 요청합니다.
func setNeedsUpdateConfiguration()

// 버튼 상태 변경에 대한 응답으로 버튼 구성을 업데이트합니다.
func updateConfiguration()

// 버튼 상태가 변경될 때 실행되는 클로저입니다.
var configurationUpdateHandler: UIButton.ConfigurationUpdateHandler?

typealias UIButton.ConfigurationUpdateHandler
```

## 🔴 Managing the title
```Swift
// 버튼의 currentTitle 속성 값을 표시하는 보기.
var titleLabel: UILabel?

// 지정된 상태와 관련된 제목을 반환.
func title(for: UIControl.State) -> String?

// 지정된 상태에 사용할 제목을 설정.
func setTitle(String?, for: UIControl.State)

// 지정된 상태와 관련된 스타일이 지정된 제목을 반환.
func attributedTitle(for: UIControl.State) -> NSAttributedString?

// 지정된 상태에 사용할 스타일이 지정된 제목을 설정.
func setAttributedTitle(NSAttributedString?, for: UIControl.State)

// 상태에 사용된 제목 색상을 반환.
func titleColor(for: UIControl.State) -> UIColor?

// 지정된 상태에 사용할 제목의 색상을 설정.
func setTitleColor(UIColor?, for: UIControl.State)

// 상태에 사용된 제목의 그림자 색상을 반환.
func titleShadowColor(for: UIControl.State) -> UIColor?

// 지정된 상태에 사용할 제목 그림자의 색상을 설정.
func setTitleShadowColor(UIColor?, for: UIControl.State)
```

## 🔴 Managing images and tint color
```Swift
// 버튼 상태에 사용되는 배경 이미지를 반환.
func backgroundImage(for: UIControl.State) -> UIImage?

// 버튼 상태에 사용되는 이미지를 반환.
func image(for: UIControl.State) -> UIImage?

// 지정된 버튼 상태에 사용할 배경 이미지를 설정.
func setBackgroundImage(UIImage?, for: UIControl.State)

// 지정된 상태에 사용할 이미지를 설정.
func setImage(UIImage?, for: UIControl.State)

// 버튼 상태에 대한 기본 기호 구성을 반환.
func preferredSymbolConfigurationForImage(in: UIControl.State) -> UIImage.SymbolConfiguration?

// 버튼 상태에 대한 기본 기호 구성을 설정.
func setPreferredSymbolConfiguration(UIImage.SymbolConfiguration?, forImageIn: UIControl.State)

// 버튼 제목과 이미지에 적용할 색조 색상.
var tintColor: UIColor!
```

## Specifying the role
```Swift
// 버튼의 역할
var role: UIButton.Role

enum UIButton.Role {
    case normal
    case primary
    case cancel
    case destructive
}
```

## Specifying the behavioral style
Mac Catalyst로 제작된 앱에서 버튼이 어떻게 나타나고 작동하는지 결정하십시오.
```Swift
var behavioralStyle: UIBehavioralStyle
var preferredBehavioralStyle: UIBehavioralStyle
enum UIBehavioralStyle { }
```

## 🔴 Getting the current state
```Swift
// 버튼 유형.
var buttonType: UIButton.ButtonType

// 버튼에 표시되는 현재 제목.
var currentTitle: String?

// 버튼에 표시되는 현재 스타일이 지정된 제목.
var currentAttributedTitle: NSAttributedString?

// 제목을 표시하는 데 사용되는 색상.
var currentTitleColor: UIColor

// 제목 그림자의 색상.
var currentTitleShadowColor: UIColor?

// 버튼에 표시된 현재 이미지.
var currentImage: UIImage?

// 버튼에 표시되는 현재 배경 이미지.
var currentBackgroundImage: UIImage?

// 현재 기호 크기, 스타일 및 무게.
var currentPreferredSymbolConfiguration: UIImage.SymbolConfiguration?

// 버튼의 이미지뷰.
var imageView: UIImageView?

// 서브타이틀을 표시하는 레이블.
var subtitleLabel: UILabel?
```

## Supporting pointer interactions
```Swift
// 포인터 상호 작용을 가능하게 하는 Bool 값.
var isPointerInteractionEnabled: Bool

// 포인터 효과가 활성화되었는지 여부를 나타내는 Bool 값.
var isHovered: Bool

// 포인터가 버튼 위에 있을 때 사용할 포인터 스타일을 반환하는 클로저.
var pointerStyleProvider: UIButton.PointerStyleProvider?

// 버튼에 적용할 포인터 스타일을 반환하는 클로저를 정의하는 유형 별칭.
typealias UIButton.PointerStyleProvider

// 버튼에 적용할 포인터 스타일을 반환하는 블록을 정의하는 유형 별칭.
typealias UIButtonPointerStyleProvider
```

## Supporting menu and toggle buttons
```Swift
// 버튼이 표시하는 메뉴.
var menu: UIMenu?

// 버튼 메뉴가 표시되는지 여부를 나타내는 Bool 값.
var isHeld: Bool

// 버튼이 메뉴 또는 토글을 통해 선택 항목을 추적하는지 여부를 나타내는 Bool 값.
var changesSelectionAsPrimaryAction: Bool

// 메뉴에 대한 기본 메뉴 요소 순서 지정 전략.
var preferredMenuElementOrder: UIContextMenuConfiguration.ElementOrder
```
---

## 🔴 addTarget Method
PockerGame 프로젝트를 진행하면서 UIButton의 sender를 통해 사용자의 Touch Event에 대해
처리하는 addTarget을 사용해보게되었다.
```Swift
func addTarget(
    _ target: Any?,
    action: Selector,
    for controlEvents: UIControl.Event
)
```
### Parameters
- target   
대상 개체, 즉 action method가 호출된 개체입니다.   
nil을 지정하면 UIKit은 지정된 작업 메시지에 응답하는 개체에 대한 응답자 체인을 검색하고 해당 개체에 메시지를 전달합니다.

- action   
호출할 작업 메서드를 식별하는 선택기입니다.   

- controlEvents   
작업 메서드가 호출되는 컨트롤별 이벤트를 지정하는 비트 마스크입니다. 

### Selector
처음 Selector를 보았을 때 뭘 선택하라는걸까??   
함수를 직접 지정해서 실행할 때 사용되는 함수 선택 지정자?선택자?로서 본래 Object-C에서 @selector(Method-Name)라는 형식으로 사용되었었다.   
하여 Selector에서 사용될 함수는 앞에 @objc 키워드를 붙여줘야한다.

## 실습
```Swift
//MARK: - 선언
self.addSubview(sevenStudButton)
        sevenStudButton.translatesAutoresizingMaskIntoConstraints = false
        sevenStudButton.widthAnchor.constraint(equalToConstant: 70).isActive = true
        sevenStudButton.heightAnchor.constraint(equalToConstant: 30).isActive = true
        sevenStudButton.topAnchor.constraint(equalTo: self.topAnchor, constant: 100).isActive = true
        sevenStudButton.leadingAnchor.constraint(equalTo: self.leadingAnchor, constant: 125).isActive = true
        sevenStudButton.addTarget(self, action: #selector(receiveInput(value:)), for: .touchUpInside)

//MARK: - addTarget Method
    @objc func receiveInput(value sender: UIButton) {
        guard let digit = sender.currentTitle?.first else { return }
        guard let convertToInt = Int(String(digit)) else { return }
        if digit != " " {
            inputValue.append(convertToInt)
        }
        
        switch digit {
        case "7":
            sevenStudButton.backgroundColor = .white
            sevenStudButton.setTitleColor(.black, for: .normal)
        case "5":
            fiveStudButton.backgroundColor = .white
            fiveStudButton.setTitleColor(.black, for: .normal)
        ...
            fourPeopleButton.setTitleColor(.black, for: .normal)
        default:
            print("This value is outside the set range.")
        }
    }
```

### 🌐 참고사이트   
- Related to UIButton   
[UIButton | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uibutton)    
[[iOS] UIButton, UISlider, UILabel](https://kingso.netlify.app/posts/boostcourse-project1-UIButton/)    
[[iOS][Swift] - 코드로 UI 구현하기 (part.1 UILabel, UIButton, UISlider)](https://velog.io/@lina0322/iOSSwift-%EC%BD%94%EB%93%9C%EB%A1%9C-UI-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-part.1-UILabel-UIButton)   

- Related to addTarget  
[addTarget(_:action:for:) | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uicontrol/1618259-addtarget)   
[[Swift]UIButton 버튼 눌러서 함수 호출 addTarget(처음부터 차근차근)](https://youbidan-project.tistory.com/152)   
[ERROR) UIButton.addTarget이 작동 안 될 때 In Code](https://hururuek-chapchap.tistory.com/165)   
[[iOS]addTarget, @objc, #selector](https://hyunndyblog.tistory.com/161)   