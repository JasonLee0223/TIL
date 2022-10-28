# Serial vs Concurrent

main & global의 차이를 알기 위해서는 우선적으로 Serial과 Concurrent의 차이를 이해해야한다.

엄연히 Sync & Async  ≠ Serial & Concurrent 다릅니다!   

## 🟢 Serial
Sync는 앞 작업과 뒷 작업의 연관성에는 상관이 없다.   
즉, 나는 내 요청에 대한 답을 받을 때까지 기다린다. -> `단일 작업`에 대한 특성을 지칭.   
따라서 앞 작업은 Sync여도 뒷 작업이 Async일 수 있다는 말이다!   

**`Serial`은 내 Queue에 들어온 작업들을 순차적으로 실행시키겠다.**   
대표적으로 애플에서 GCD를 사용할 때, Main Queue가 Serial Queue이다.

`'Sync'는 단일 작업의 특성 중 하나`이고   
`'Serial'은 단일 작업들'을' 순차적으로 '하나씩' 실행하는 것이다.`   
⭐️ `'Serial Queue'는 한 번에 하나의 Task`만 실행시킬 수 있기 때문이다!

<img src="https://user-images.githubusercontent.com/92699723/198546982-0cae2523-2f03-4015-afe1-56d9c10b3e27.png" width="650" height="250">

위 그림처럼 **`Async`작업이 있다 해도 Serial Queue에는 `1개의 Task만 실행`할 수 있다!**
그래서 주로 Serial Queue는 `동기화` 작업을 진행할 때 많이 사용한다.

## 🟢 Concurrent
Async와는 다른 개념으로, Async는 `단일 작업`에 대한 특성을 지칭하는 것이라면,   
**`Concurrent Queue`는 내 Queue에 들어온 작업들을 동시다발적으로 실행 시키겠다!**   
⭐️ `한 번에 여러 개의 Task`를 실행시킬 수 있다!   

 <img src="https://user-images.githubusercontent.com/92699723/198548519-d771713e-118a-42a8-a139-ee2f50243db3.png" width="700" height="500">


