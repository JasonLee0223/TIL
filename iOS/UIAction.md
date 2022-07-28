# UIAction
클로저에서 작업을 수행하는 메뉴 요소입니다.
## OverView
클로저에서 작업을 수행하는 메뉴 요소를 원할 때 UIAction 개체를 만듭니다.   

## addTarget -> UIAction으로
코드로 UIButton에서 sender를 통하여 User의 행동에 따라 값을 사용할 수 있었던 addTarget 메서드를 기존에 사용해왔었는데   
iOS14+부터 UIAction을 지원해주며 새로운 기술을 사용해보면 좋겠다고 생각이 들었다.

## Basically Form
```Swift
// Create a closure-based action to use as a menu element.
let refreshAction = UIAction(title: "Refresh") { (action) in
    print("Refresh the data.")
}
```
위와 같이 클로저전에 UIAction의 프로퍼티로 `title`을 사용할 수 있는데 아래에 다른 항목들도 찾아보았다.

### Parameters
title : 해당 액션이 적용될 것의 title을 설정   
image : title 옆에 보여질 image   
identifier : action의 고유한 식별자, 기본값은 nil, nil로 지정하면 알아서 고유한 식별자를 생성   
discoverabilityTitle : action의 목적을 설명하는 정교한 제목 (= elaborated title)   
attributes : action의 style을 나타내는 속성   
  - disabled
  - destructive
  - hidden   

state : action의 initial state   
  - off
  - on
  - mixed

handler : 사용자가 action을 선택한 후에 호출되는 핸들러


🌐 참고사이트   
[Apple Develop - UIAction](https://developer.apple.com/documentation/uikit/uiaction)   
[iOS 14 + ) UIAction closure based UIControl](https://zeddios.tistory.com/1093)   
[UIButton + UIAction](https://velog.io/@pcsoyeon/UI-Button-Action)