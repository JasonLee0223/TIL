# ViewController LifeCycle
ViewController의 생명 주기는 Scene(장면)의 전환과 복귀에 밀접하게 연관되어 있다.   
일반적으로 `새로운 장면으로 전환`하거나 `이전 화면으로 복귀하는 과정`에서 ViewController의 `객체의 생성과 소명이 발생`하기 때문이다.

아래와 순서로 ViewController의 생명주기는 이와 같은 과정을 순홚나다.
1. 앱을 처음 실행하거나 새로운 장면으로 전환할 때에는 그 장면을 담당하는 ViewController 객체가 새로 생성된다.
2. 생성된 객체는 메모리에 로드되어 자신의 역할을 하고 주어진 역할을 모두 마치면 앱은 이전 장면으로 복귀한다.
3. 생성되었던 ViewController 객체는 메모리에서 해제되면서 소멸한다.
4. 필요에 의해 이전 장면으로 다시 전환할 경우, ViewController 객체는 이미 소멸된 후이기 때문에 다시 새롭게 생성되고, 역할을 끝내고나면 다시 소멸된다.

## ViewController 상태 변화에 따른 API
- Appearing: ViewController가 스크린에 등장하기 시작한 순간부터 등장을 완료하기 직전까지의 상태
- Appeared: ViewController가 스크린 전체에 완전히 등장한 상태를 나타낸다.
- Disappearing: ViewController가 스크린에서 가려지기 시작해서 완전히 가려지기 직전까지의 상태. 또는 퇴장하기 시작해서 완전히 퇴장하기 직전까지의 상태.
- Disappeared: ViewController가 스크린에서 완전히 가려졌거나 혹은 퇴장한 상태   

## ViewController Life Cycle 
<img src = "https://user-images.githubusercontent.com/92699723/182879205-2561325b-9640-4c69-bc4f-aac998f3bec3.jpeg" width=300 height=400>   

[이미지 출처](https://subscription.packtpub.com/book/application-development/9781783550814/6/ch06lvl1sec60/uiviewcontroller-lifecycle-methods)

<img src = "https://user-images.githubusercontent.com/92699723/182880648-626cf83a-81e2-4095-8b27-c80539127869.png" width=500 height=500>   

[[이미지 출처] [iOS]View의 Life-Cycle](https://do-misol.tistory.com/48)   

### 각 메서드별로 설명
```Swift
func viewDidLoad()
``` 
뷰 게층이 **메모리에 Load된 직후 호출되는 메서드**
`메모리에 처음 로딩될 때 1회 호출`되는 메서드
```Swift
func viewWillAppear(_ animated: Bool)
```
**화면에 표시되기 직전**에 호출되는 메서드
`다른 뷰로 이동했다가 되돌아오면 다시 호출`되는 메서드
```Swift
func viewDidAppear(_ animated: Bool)
```
**화면에 표시되고 나면**호출되는 메서드
뷰를 나타내는 것과 관련된 추가적인 작업을 하기 좋은 시점
```Swift
func viewWillDisappear(_ animated: Bool)
```
뷰가 뷰 계층에서 **사라지기 직전**에 호출되는 메서드
뷰가 생성된 뒤 발생한 변화를 이전 상태로 되돌리기 좋은 시점
```Swift
func viewDidDisappear(_ animated: Bool)
```
뷰가 뷰 계층에서 **사라진 후**호출되는 메서드

### 🌐 참고사이트   
꼼꼼한 재은씨의 Swift기본편(p108~114)   
[iOS ) View Controller의 생명주기(Life-Cycle)](https://zeddios.tistory.com/43)   
[Swift - ViewController Life Cycle(생명주기)](https://tono18.tistory.com/11)   
[Swift - ViewController Life Cycle(생명주기)02](https://tono18.tistory.com/20)   



