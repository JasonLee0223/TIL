# UILabel
한 줄 또는 여러 줄의 텍스트를 보여주는 뷰로, UIButton 등의 컨트롤의 목적을 설명하기 위해 사용하는 경우가 많다.

레이블의 생성 단계
1. 레이블을 생성
2. 레이블이 표시할 문자열을 제공
3. 레이블의 모양 및 특성을 설정

## 🔴 Accessing the text attributes
- var text: String?   
  레이블이 표시할 문자열

- var attributedText: NSAttributedString?   
  레이블이 표시할 속성 문자열

- var font: UIFont!   
  글자 폰트

- var textColor: UIColor!   
  텍스트 색상

- var textAlignment: NSTextAlignment    
  문자열의 가로 정렬 방식

- var lineBreakMode: NSLineBreakMode    
  레이블의 경계선을 벗어나는 문자열에 대응하는 방식

- var lineBreakStrategy: NSParagraphStyle.LineBreak
- var isEnabled: Bool
- var enablesMarqueeWhenAncestorFocused: Bool
- var showsExpansionTextWhenTruncated: Bool

## Sizing the label's text
- var adjustsFontSizeToFitWidth: Bool
- var allowsDefaultTighteningForTruncation: Bool
- var baselineAdjustment: UIBaselineAdjustment
- var minimumScaleFactor: CGFloat
- var numberOfLines: Int    
  문자를 나타내는 최대 라인 수  
  문자열을 모두 표시하는 데 필요한 만큼 행을 사용하려면 '0'으로 설정. 기본값은 1    
  설정한 문자열이 최대 라인 수를 초과하면 lineBreakMode 프로퍼티의 값에 따라 적절히 잘라서 표현한다.

## Managing highlight values
- var highligntedTextColor: UIColor?
- var isHighlighted: Bool

## Drawing a shadow
- var shadowColor: UIColor?
- var shadowOffset: CGSize

## Drawing and positioning overrides
- func textRect(forBounds: CGRect, limitedToNumberOFLines: Int) -> CGRect
- func drawText(in: CGRect)
  
## Getting the layout constraints
- var preferredMaxLayoutWidth: CGFloat

## Accessing additional attributes
- var isUserInteractionEnabled: Bool

## Supporting types
- enum NSTextAlignment


### 🌐 참고사이트
[UIScreen | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uilabel)   
[[iOS] UIButton, UISlider, UILabel](https://kingso.netlify.app/posts/boostcourse-project1-UIButton/)

