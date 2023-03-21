# Producer-Consumer
멀티 스레드 디자인 패턴인 생산자(Producer) 소비자(Consumer) 패턴에 대해 알아보자.

<img src = "https://user-images.githubusercontent.com/92699723/226589105-216aa66d-ac28-4130-8ea1-269bbc004768.png" width = 70%>

## 1️⃣ 생산자 - 소비자 패턴이란?
`작업 목록(Blocking Queue)`을 가운데 두고 `작업을 생산해 내는 주체`와 `작업을 처리하는 주체`를 `분리`시키는 설계 방법이다.  
즉, `Producer(생산자)`와 `Consumer(소비자)`가 각각 감당할 수 있는 부하를 조절할 수 있다는 장점이 있다.  
`Producer(생산자)`는 작업을 새로 만들어 Queue에 쌓아두고(enqueue), `Consumer(소비자)`는 작업을 가져가 처리하는 구조이다.  

오직 각자의 책임에 맞게 동작하여 전혀 신경쓰지 않아도 된다는 점이 중요한 포인트다.  
이때 BlockingQueue를 사용하면 코드 구현에 편리하다. 

## 2️⃣ 생산자 - 소비자 작업량 조절
위 디자인 패턴을 사용할 때는 주의할 점이 나타난다.  
생산자가 소비자가 감당할 수 있는 것보다 많은 양의 작업을 만들어 내면 Queue에는 계속해서 작업이 누적되어 결국 `메모리 오류`가 발생한다.  
(실생활에서는 수요와 공급의 불균형으로 공급 과잉을 떠올려 이해해보았다.)    

하지만, Queue의 크기에 제한을 두게 되면 빈 공간이 생길 때까지 작업을 추가하지 않고, **`대기`하도록 구현하여**,  
불필요한 연산을 하지 않도록 하는 부분이 중요하게 작용한다. 이 역할을 BlockingQueue가 담당하게 된다.     
(기업에서 발주서를 확인하여 필요한 양만 생산하도록 하는 것이 이러한 부분과 동일한 개념이지 않을까..??)

`BlockingQueue`는 결국 생산자가 작업을 빨리 처리하거나, Consumer가 작업을 빨리 처리하는 경우의 오류를 피할 수 있도록 돕고,  
작업의 대한 **`스레드 간의 동기화 및 작업량을 조절`** 해 `Thread-Safe`하게 프로그램을 작성할 수 있게된다.

### 💡 구현에 대한 포인트
- enqueue(): Queue의 크기에 제한이 되어 있을 경우, Queue에 **`빈 공간이 생길 때 까지 대기`** 하고, 빈 공간이 생기면 작업을 큐에 넣어 줍니다.
- dequeue(): Queue의 작업이 없을 경우, **`작업이 생길 때까지 대기`** 하고 작업이 생기면, Queue에서 작업을 꺼내갑니다.

### 🌐 Reference Site
[생산자(Producer) 소비자(Consumer) 패턴](https://coding-food-court.tistory.com/81)  