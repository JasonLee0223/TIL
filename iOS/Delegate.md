# Delegate

## 1. Delegate 패턴이란?
Delegate는 '위임하다'라는 사전적 의미로 해당 delegate 프로토콜을 준수하는 `위임자를 갖고 있는 객체가 자신의 일을 위임하는 형태의 디자인 패턴이다.`   
Delegate는 iOS에서 MVC기준으로 설명하게되면 ViewController에서 Model과 View의 변화를 감지하여
이로인해 해당되는 역할을 수행할 객체에게 명령을 내린다고보면 조금 이해가 쉬웠다.   
<img src="https://user-images.githubusercontent.com/92699723/194560447-14fb91b1-9be3-4e66-903e-66ef70866ccb.png" width="800" height="400">

순서를 살펴보면
1. View에서 어떠한 이벤트를 받는다.
2. `ViewController에서 Model에게` 해당 Action에 맞는 객체를 생성 또는 변형하게한다.
3. `Model에서 ViewController에게` 해당 객체를 만들었음을 알린다.
4. `ViewController에서 View에게` 해당 객체가 만들어졌으니 UI를 구성 또는 변경해달라고 요청한다.

## 3. Delegate를 이용한 예시 및 실습

### 참고사이트 🌐
[[iOS] Delegate 패턴이란 무엇일까?](https://velog.io/@zooneon/Delegate-%ED%8C%A8%ED%84%B4%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C)
[swiftbysundell-Delegation in Swift](https://www.swiftbysundell.com/articles/delegation-in-swift/)
[iOS Delegate 패턴에 대해서 알아보기](https://magi82.github.io/ios-delegate/)
[[swift] Delegate Pattern ( + delegate로 데이터 전달 )](https://ggasoon2.tistory.com/6)