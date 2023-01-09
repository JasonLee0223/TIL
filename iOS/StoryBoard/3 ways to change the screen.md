# 3 ways to change the screen (화면 전환 3가지 방법)
XCode에서 스토리보드를 이용하여 개발할 경우 다양한 방법으로 View와 View 사이를 이동 할 수 있습니다.   
이때 서로 다른 View간 이동은 `Segue`라는 것을 이용하여 이동을 하게 되는데 제일 많이 사용되는 것 같은   
총 3가지 이동 방법을 정리해 보겠습니다.   
들어가기에 앞서 Action Segue의 4가지 종류에 대해 먼저 알아보고 가보도록 하겠습니다.   

<img src="https://user-images.githubusercontent.com/92699723/211282499-93ef3032-3454-4f5c-b4d3-023f562ac2b4.png" width=200>   

[StoryBoard Segue] Segue를 연결했을때 기호를 Story Segue라고 한다.

## 🟢 Segue의 4가지 종류
<img src="https://user-images.githubusercontent.com/92699723/211282506-e6b9d190-9926-4f48-9c1c-7725e521d0f2.png" width = 200>

- Show(`Push`): 이 segue는 `target viewController`의 `showViewController: sender:` 가 실행된다.   
  일반적으로는 `source ViewController` 위에 새로운 컨텐츠가 Modal로 보여진다.   
  몇몇 ViewController들은 해당 메서드가 재정의 되어있어서 다른 동작을 한다.   
  UIKit은 `target ViewContollerForAction: sender:`메서드로 `source ViewController`를 찾는다.

- Show Detail(`Replace`): 이 segue는 `target ViewController`의 `showDetailViewController: sender:`메서드가 실행된다.   
  이 segue는 UISplitViewController 객체 내에 내장된 ViewController에 대해서만 관련된 Segue이다.   
  splitViewController는 Child ViewController를 새로운 컨텐츠로 `replace`합니다.
  나머지 대부분의 ViewController에서는 Modal로 보여줍니다.

- Present Modally: 이 segue는 ViewController를 `Modal`로 보여준다.

- Present As Popover: 기존 View에 앵커를 둔 컨텐츠를 보여줍니다.

- Custom: 개발자가 지정한 행동을 하는 segue입니다.
---

## 🔴 화면 전환 기법 3가지
위 segue의 5가지 Type에 대해 알아보았으니 본격적으로 화면 전환을 해보자!
1. 인터페이스 빌더에서 직접 연결하기
2. Segue의 Identifier를 설정 후, 코드에서 performSegue 적용하기
3. Storyboard ID 설정 후, 코드에서 present 적용하기
각 항목에 대해 자세히 살펴보자!

### 1️⃣ 인터페이스 빌더에서 직접 연결하기
① 2개의 ViewController에서 A ViewController에서 NavigationBar의 BarButtonItem을   
`ctrl키를 누른채` B ViewController에 `Drag and Drop`을 하면, 연결할 수 있는 Segue의 종류(위 참고)가 뜬다.

② Segue로 Show를 선택하면, `A ViewController에서 B ViewController의 방향으로` 화살표가 하나 생긴다.   
이게 `Segue가 연결되었다는 의미`이고, Segue 화살표를 선택 후 `Inspector`에서 설정을 변경할 수 있다.

### 2️⃣ Segue의 Identifier를 설정 후, 코드에서 performSegue 적용하기
여기서는 Inspector에서 Segue의 Identifier를 설정한 후, 코드에서 화면 전환이 필요할 때   
`performSegue` 메서드를 사용하여 Segue 객체를 생성해본다.   

① 인터페이스 빌더에서 연결한 것 처럼 Segue를 연결해준다.   
여기서 주의할 점으로 `Button에서 ctrl을 통해 Drag and Drog 형태가 아니라` A ViewController의 위에 있는 버튼에서 끌고 간다.

② 위와 동일하게 Action Segue에서 Show를 선택하고 Inspector에서 보면,   
`Segue의 Identifier를 설정`할 수 있다. (Custom하게 작성한다.)

③ 이제 A ViewController의 클래스에 있는 `화면 전환에 사용될 Button의 Action` 메서드 안에    
`performSegue(withIdentifier: sender:)`를 구현해준다.
```Swift
@IBAction func GoToBViewController(_ sender: UIButton) {
    performSegue(withIdentifier: "Custom String", sender: sender)
}
```
📍 performSegue 메서드가 실행되기 전에 `prepare(for segue: sender:)`메서드가 항상 먼저 실행되는데,   
`ViewController간에 데이터를 전달해야 할 때`, `prepare(for segue: sender:)`를 이용한다.

### 3️⃣ Storyboard ID 설정 후, 코드에서 present 적용하기
이번에는 ctrl로 `Drag And Drop`히여 segue를 연결해줄 필요 없이, 각 ViewController의   
`Storyboard ID를 지정`해주고, 코드에서 `present(_: animated: completion:)`라는 메서드를 이용해보자.   

① B ViewController를 선택 후, Inspector에 Identify -> Storyboard ID를 `B ViewController`로 설정해준다.

② A ViewController 클래스에서 `GoToBViewController`버튼의 Action 메서드 내에서 먼저   
Optional Chaning으로 `instantiatedViewController(with Identifier:)`하여   
UIViewController 객체를 가져온다.   
`가져온 객체의 타입을 B ViewController로 바꿔주기 위해` as?를 써서 다운캐스팅하고,   
이를 B ViewController라는 변수에 넣는다.   
그럼 다음, `present(_: animated: completion)` 메서드를 사용하여 B ViewController를 보여달라고 말하면 된다!

```Swift
@IBAction func GoTOB(_ sender: UIButton) {
    if let BViewController = self.storyboard?.instantiateViewController(identifier: "B ViewController") as? BViewController {
        present(BViewController, animated: true, completion: nil)
    }
}
```

### 🌐 Reference Site
[iOS) Segue](https://o-o-wl.tistory.com/44)   
[[iOS] Segue 연결 방법](https://jiyeonlab.tistory.com/8)   
[XCode 스토리보드 사용시에 Segue 이용방법 3가지](http://theeye.pe.kr/archives/2292)