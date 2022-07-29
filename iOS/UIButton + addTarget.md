# UIButton + addTarget
PockerGame 프로젝트를 진행하면서 UIButton의 sender를 통해 사용자의 Touch Event에 대해
처리하는 addTarget을 사용해보게되었다.
## addTarget Method
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
[[Swift]UIButton 버튼 눌러서 함수 호출 addTarget(처음부터 차근차근)](https://youbidan-project.tistory.com/152)   
[ERROR) UIButton.addTarget이 작동 안 될 때 In Code](https://hururuek-chapchap.tistory.com/165)   
[[iOS]addTarget, @objc, #selector](https://hyunndyblog.tistory.com/161)
[Apple Developer Site](https://developer.apple.com/documentation/uikit/uicontrol/1618259-addtarget)