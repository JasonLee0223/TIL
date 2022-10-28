# Process vs Thread

## 🟢 Process
운영체제로부터 시스템 자원을 할당받는 작업의 단위

<img src="https://user-images.githubusercontent.com/92699723/198515411-c1e9f9b6-c4d4-4559-8019-01428c4e6475.png" width="250" height="400">

위 그림에서 보이는 것처럼 **`각각의 독립된 메모리 영역 (Code, Data, Stack, Heap)을 각자 할당 받는다!`**   

**`프로세스는 서로의 변수나 자료구조에 대해 절대 접근할 수 없다!`**   
만약 A-Process -> B-Process의 자원을 접근하려고 하면,   
프로세스간 통신(IPC, Inter-Process Communication)을 사용해야 한다. (파일 , 소켓 메세지큐, 세마포어 등)   

### 🟣 Multi-Process

<img src="https://user-images.githubusercontent.com/92699723/198517312-7cd3aefb-18ca-428b-84d7-d9a925f71cda.png" width="600" heught="400">

**`하나의 프로그램을 여러 개의 프로세스로 구성하여, 각 프로세스마다 하나의 작업(Task)씩 처리하도록 하는 것.`**   
예를 들어 Airbnb라는 앱을 실행하고 예약 버튼을 눌러서   
숙소의 이미지와 텍스트를 받아오는 프로세스 Task1   
VAT 및 결제 금액을 계산하는 프로세스 Task2 이런식으로 생각해보았다.   

이런식으로 `하나의 프로그램에서 일어나는 여러 개의 작업`을 `프로세스를 여러 개 생성하여 각자 하나씩 처리하도록`해주는 것임.

- Multi Process의 장점
  프로세스는 독립된 메모리 영역을 각자 할당받기 때문에, **프로세스 간 서로의 자원에 침투할 수 없다.**   
  따라서 `독립된 구조이기 때문에 안정성이 높다!`   
  A-Process에 문제가 생겨도 B-Process 입장에서는 어떠한 영향도 받지 않을 수 있다.
- Multi Process의 단점
  프로세스들이 통신하는 과정에서 A-Process를 실행할 때는 A-Process의 메모리 영역을 올리고,   
  B-Process를 실행할 때는 B-Process의 메모리 영역을 올린다.   
  이러한 작업을 `Context Switching(문맥 전환)`이라고 하는데,   
  프로세스는 메모리가 모두 독립적으로 존재하기 때문에,   
  `Context Switching`시 **`CPU의 부담도 커지고 오버헤드가 발생하게 된다`**는 것이 가장 큰 단점이다.
  또 다른 하나는, `프로세스간의 자원 공유가 어렵다`는 것이다.

### 🟣 IPC

## 🟢 Thread
**하나의 Process 내에서 동작되는 여러 실행의 흐름.**   
Thread는 Process가 아닌, Process 내에서 동작되는 것이기 때문에   
**`메모리 영역을 독립적으로 할당받지 못한다!`**

<img src="https://user-images.githubusercontent.com/92699723/198524136-c3d8b89b-fe3c-49a3-9b55-370f9ed5ead8.png" width="1000" height="400">

위 그림과 같이 `Code, Data, Heap 영역은 공유`하고 `Stack 영역만 독립적으로 할당`받을 수 있다.   
(잠깐! Stack이 독립적으로 할당받을 수 있는 이유는 Stack영역이 LIFO방식으로 Stack이 쌓이면 프로세스가 섞인 채로 순서대로 나와 흐름에 방해를 주기 때문)   
따라서 쓰레드들 끼리는 **`Heap 영역을 공유하여 같은 자원을 접근`** 할 수 있지만,   
각자의 **`Stack 영역은 서로 접근할 수 없다.`**

### 🟣 Multi Thread
<img src="https://user-images.githubusercontent.com/92699723/198525532-388b60e6-f6b0-4837-835a-b928d63d2f99.png" width="1000" height="400">

**`하나의 프로그램을 여러 개의 Thread로 구성하여, 각 Thread마다 하나의 작업(Task)씩 처리하도록 하는 것.`**   

- Multi Thread 장점
  Thread간 **Code, Data, Heap 영역을 공유**하고 있기 때문에,   
  **`Context Switching이 빠르다!`**   
  또한, Process를 생성하여 자원을 할당하는 것이 아니니 때문에,
  **`생성/종료 시간도 Process보다 빠르다!`**
- Multi Thread 단점
  **`설계가 까다롭다...!`**   
  왜냐하면 Stack 영역을 빼고 공유하기 때문에, A-Thread가 접근하려는 Heap 영역의 자원을 B-Thread가 갑자기 접근해서 바꿔버리는 등 **`자원 공유의 문제가 생기기 때문이다(동기화 문제)`**
  또한 독립적이지 않아, **`하나의 Thread에 문제가 발생 시 전체 Thread가 영향을 받는다.`**   
  마지막으로, 단일 Process 시스템의 경우 효과를 기대하기 어렵다.

||Multi Process|Multi-Thread|
|-----|:---:|:---:|
|정의|하나의 프로그램을 여러 개의 `Process`로 구성<br /> 각 프로세스마다 하나의 작업(Task)씩 처리|하나의 프로그램을 여러 개의 `Thread`로 구성<br /> 각 Thread마다 하나의 작업(Task)씩 처리|
|생성/종료<br />소요 시간| 많음| 적음|
|Context Switching| 많음| 적음|
|자원 접근|IPC 사용|공유 자원(Code,Data,Heap)사용|
|메모리 할당|Code,Data,`Stack`,Heap<br />모두 독립적으로 할당|Code,Data,Heap만 공유<br /> `Stack`만 독립적으로 할당|
|장점|독립된 구조로 안정성이 높음|Context Switching이 빠름<br /> 생성 및 종료 시간도 빠름<br /> Process간 자원 공유가 간단하다|
|단점|Context Switching 소요 시간이 많이 들어가 오버헤드 발생<br /> 생성 및 종료 시간 오래 걸림<br /> Process간 자원 공유가 어려움| 설계가 까다로움 <br /> 동기화시 문제가 생길 수 있음 <br /> 하나의 Thread에서 문제 발생 시 전체 Thread에 영향이 생김|


### 🌐 Reference Site
[iOS) 프로세스(Process) vs 쓰레드(Thread)](https://babbab2.tistory.com/63)