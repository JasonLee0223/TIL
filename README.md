# TIL
매일매일 학습하여 커밋을 남겨보자!

## Git
|Subject|Link|Explain|
|:--|:--|:--|
|Git Commit|[Commit message style](Git/Commit%20message%20style.md)|

## Operating System
|Section|Title|Subject|
|:---|:---|:---|
|01|Introduction to Operating Systems|운영체제란 무엇인가, 운영체제의 목적, 운영체제의 분류, 운영체제의 예, 운영체제의 구조|
|02|System Structure & Program Execution 1|컴퓨터 시스템 구조, Mode bit, Timer, Device Controller, 입출력(I/O)의 수행 <br/>동기식 입출력과 비동기식 입출력, 시스템콜(System Call), 인터럽트(Interrupt)|
||System Structure & Program Execution 2|컴퓨터 시스템 구조, 인터럽트(Interrupt), 동기식 입출력과 비동기식 입출력 <br/>시스템콜(SystemCall), DMA(Direct Memory Access), 서로 다른 입출력 명령어 <br/>저장장치 계층 구조, 프로그램의 실행(메모리 load), 커널 주소 공간의 내용 <br/>사용자 프로그램이 사용하는 함수, 프로그램의 실행|
|03|Process 1|프로세스의 개념, 프로세스의 상태(Process State), 프로세스의 개념, 프로세스 상태도, Process Control Block(PCB), 문맥교환(Context Switch), 프로세스를 스케줄링하기 위한 큐, Ready Queue와 다양한 Device Queue, 스케줄러(Scheduler)|
||Process 2|동기식 입출력과 비동기식 입출력, 프로세스 스케줄링 큐의 모습, Thread|
||Process 3|Thread, Single and Multithreaded Processes, Benefits of Threads, Implemetation of Threads|
|04|Process Management 1|프로세스 생성(Process Creation), 프로세스 종료(Process Termination)|
||Process Manangement 2|프로세스 생성(Process Creation), 프로세스와 관련한 시스템콜, 프로세스 간 협력, Message Passing, <br/>Interprocess communication, CPU and I/O Bursts in Program Execution, <br/>CPU-burst Time의 분포, 프로세스의 특성 분류, CPU Scheduler & Dispatcher|
|05|CPU Scheduling 1|CPU and I/O Bursts in Program Execution, CPU-burst Time의 분포, CPU Scheduler & Dispatcher, <br/>Scheduling Algorithms, Scheduling Criteria, FCFS(First- Come First-Served), <br/>SJF(Shortest-Job-First), 다음 CPU Burst Time의 예측, Exponential Averaging, Priority Scheduling, <br/>Round Robin(RR)|
||CPU Scheduling 2 <br/>Process Synchronization 1|CPU-burst Time의 분포, Schedulling Algorithms, Round Robin(RR), Multilevel Queue, <br/>Multilevel Feedback Queue, Multi-Processor Scheduling, Real-time Scheduling, <br/>Thread Scheduling, Algorithm Evaluation|
|06|Process Synchronization 1|데이터의 접근, Race Condition, OS에서의 race condition(3/3), The Critical-Section Problem, <br/>OS에서 race condition(1/3), If you preempt CPU while in kernel mode…, <br/>Initial Attempts to Solve Problem, 프로그램적 해결법의 충족조건, Algorithm 1, Algorithm2, <br/>Algorithm3(Peterson's Algorithm), Synchronization Hardware, Semaphores|
||Process Synchronization 2|Semaphores, Critical Section of n Processes, Block / Wakeup Implementation, Implementation, <br/>Two Types of Semaphores, Deadlock and Starvation, Dining-Philosophers Problem|
||Process Synchronization 3|Semaphores, Implementation, Classical Problems of Syncronization, Bounded-Buffer Problem, <br/>Readers-Writers Problem, Dining-Philosophers Problem, Monitor
||Process Synchronization 4 (Concurrency Control)|Semaphores, Monitor, Bounded-Buffer Problem, Dining Philosophers Example|
|07|Deadlocks 1|교착상태(deadlock), The Deadlock Problem, Deadlock 발생의 4가지 조건, <br/>Resource-Allocation Graph(자원할당그래프), Deadlock Prevention, Deadlock의 처리 방법, <br/>Deadlock Avoidance, Resource Allocation Graph algorithm, Banker's Algorithm|
||Deadlocks 2|Deadlock의 처리 방법, Deadlock Avoidance, Deadlock Detection and Recovery, <br/>Deadlock Ignorance|
|08|Memory Management 1|Logical vs. Physical Address, 주소바인딩(Address Binding), Memory-Management Unit(MMU), <br/>Dynamic Relocation, Hadware Support for Address Translation, Some Treminologies, <br/>Dynamic Loading, Overlays, Swapping, Dynamic Linking, Allocation of Physical Memory, <br/>Contiguous Allocation, Paging|
||Memory Management 2|Paging, Dynamic Relocation, Paging Example, Address Translation Architecture, <br/>Implementation of Page Table, Paging Hardware with TLB, Associative Register, <br/>Effective Access Time, Two-Level Page Table, Address-Translation Scheme, <br/>Two-Level Paging Example|
||Memory Management 3|Multilevel Paging and Performance, Two-Level Page Table, Valid (v)/ Invalid (i) Bit in a Page Table, <br/>Memory Protection, Inverted Page Table, Inverted Page Table Architecture, Shared Page, <br/>Shared Pages Example, Segmentation, Segmentation Architecture, Segmentataion Hardware|
||Memory Management 4|Segmentation, Segmentation Hardware, Segmentation Architecture, Example of Segmetation, <br/> Segmentation Architecture(Cont.), Sharing of Segments, Segmentation with Paging, <br/>Address Translation Architecture|
|09|Virtual Memory 1|Demand Paging, Memory에 없는 Page의 Page Table, Page Fault, Steps in Handling a Page Fault, <Br/>Performance of Demand Paging, Free Frame이 없는 경우, Page Replacement, Optimal Algorithm, <br/>FIFO(First In First Out) Algorithm, LRU(Least Recently Used) Algorithm, <br/>LFU(Least Frequently Used) Algorithm, LRU와 LFU 알고리즘 예제, LRU와 LFU 알고리즘의 구현, <br/>다양한 캐슁 환경|
||Virtual Memory 2|다양한 캐슁 환경, LRU와 LFU 알고리즘의 구현, Paging System에서 LRU, LFU 가능한가?, Clock Algorithm, <br/>Page Frame의 Allocation, Global vs. Local Replacement, Thrashing, Thrashing Diagram, <br/>Working-Set Model, Working-Set Algorithm, PFF(Page-Fault Frequency) Scheme, <br/>Page Size의 결정|
|10|File Systems|File and File System, Directory and Logical Disk, open( ), File Protection, File System의 Mounting,<br/> Access Methods|
||File Systems Implementation 1|Allocation of File Data in Disk, Contiguous Allocation, Linked Allocation, Indexed Allocation, <br/>UNIX 파일시스템의 구조, FAT File System, Free-Space Management, Directory Implementation, <br/>VFS and NFS, Page Cache and Buffer Cache|
||File Systems Implementation 2|Page Cache and Buffer Cache, 프로그램의 실행|
|11|Disk Management and Scheduling 1|Disk Structure, Disk Scheduling, Disk Management, Disk Scheduling Algorithm, <br/>FCFS(First Come First Service), SSTF(Shortest Seek Time First), SCAN, C-SCAN, <br/>Other Algorithms, Disk-Scheduling Algorithm의 결정|
||Disk Management and Scheduling 2|Swap-Space Management, RAID|

## API Design Guidelines
### 🪧 Agenda
|Section|Subject|Explain|   
|:--|:--|:--|   
|📕 Fundamentals|[Fundamentals](APIDesignGuideline/Fundamentals.md)|(핵심개념)|
|📗 Naming|[Promote Clear Usage](APIDesignGuideline/Promote%20Clear%20Usage.md)|(명확하게 사용하기)|
||[Strive for Fluent Usage](APIDesignGuideline/Strive%20for%20Fluent%20Usage.md)|(자연스러운 사용을 위해 노력하기)|
||[Use Terminology Well](APIDesignGuideline/Use%20Terminology%20Well.md)|(적절한 기술 용어 사용하기)|
|📘 Conventions|General Conventions|(일반 규칙)|
||Parameters |(매개변수)|
||Argument Labels|(전달인자 레이블)|
|📙 Special Instructions|Special Instructions|(특별 지침들)|
|📖 Article|[✏️ Bool 변수 이름 제대로 짓기 위한 최소한의 영문법](Naming/BoolNaming.md)|

# iOS
|Section|Title|Subject Link|Explain|
|:--|:--|:--|:--|   
|UIKit|
|App and environment||[UIKit 설명, App and Environment](iOS/About%20App%20Development%20with%20UIKit.md)|
|App Structure|Managing your app's life cycle|[ViewController Life-Cycle](iOS/ViewController%20Life-Cycle.md)|
|User Interface|UIView|
||Configuring the bounds and frame rectangles|[var frame vs var bounds](iOS/Frame%20vs%20Bounds.md)|
|||var bounds|Same as above|
||Container Views|[UIStackView](iOS/UIStackView.md)|
||Content Views|[UIImageView](https://github.com/JasonLee0223/TIL/blob/main/iOS/UIImageVIew.md)|
||Controls|[UIButton](iOS/UIButton.md)|
|||[UIButton.Configuration](iOS/UIButton.Configuration.md)|
|||[UISlider](iOS/UISlider.md)|
|||[UIStepper](iOS/UIStepper.md)|
||Text Views|[UILabel](iOS/UILabel.md)|
||Search Field|
||Bars|
||Content Viewer|
||Private Click Measurement (PCM)|
||SwiftUI|
|Windows and screens|Windows|
||Scenes|
||Popovers|
||Alerts|
||Screens|[UIScreen](iOS/UIScreen.md)|
|Touches, presses, and gestures||[UITapGestureRecognizer](iOS/UITapGestureRecognizer.md)|
|Menus and shortcuts||[UIAction](iOS/UIAction.md)|
|Core Graphics|
|Geometric Data Types||[CGPoint, CGSize, CGRect](iOS/CGPoint,CGSize,CGRect.md)|
|||CGSize|Same as above|
|||CGRect|Same as above|
|OS|
|Logs|Essentials|
||Log Messages|[Logger & OS_Log](iOS/Logger%20&%20OS_Log.md)|
|Accessibility for UIKit|
|||[File System Basics](iOS/FileSystem.md)|
|||[Sandbox 정책과 Files 앱](iOS/SandBox.md)|
|Etc|
|||[VC간의 데이터 전송방법](iOS/Data%20Transfer%20Process.md)|
|||[Delegate](iOS/Delegate.md)|
|Storyboard|
|||[3 ways to change the screen](iOS/StoryBoard/3%20ways%20to%20change%20the%20screen.md)|


# Swift
|Section|Title|Subject Link|Explain|
|:--|:--|:--|:--|   
|01|데이터 타입 고급|[typealias](Swift/typealias.md)|
|||Tuple|
||Collection Types|Array|
|||[Dictionary](Swift/Dictionary.md)|
|||Set|
|||[Enumerations](Swift/Enum.md)|
|||Operator|
|||Control Flow|
|||Functions|
|||Optional|
|02|Object Oriented Programming with Swift|[Struct & Class](Swift/Struct%20vs%20Class.md)|
|||Property & Method|
|||Initialization|
|||Access Control|
|03|functional programming with Swift|[Closure](Swift/Closure.md)|
|||Optional Chaining|
|||Early-exit|guard-let|
|||[Higher-order function](Swift/Higher-order%20function.md)|고차함수: map, filter, reduce|
|||Monad|
|04|Extension|[Subscript](Swift/Subscript.md)|
|||[Inheritance](Swift/Inheritance.md)|
|||Type Casting|as, is|
|||[Protocol](Swift/Protocol.md)|
|||Extension|
|||[Generic](Swift/Generic.md)|
|||[Protocol Default Implimentations](Swift/ProtocolDafaultImplimentation.md)|프로토콜 초기구현|
|05|Swift High|Nested Type|
|||[Pattern](Swift/Pattern.md)|
|||where|
|||ARC|
|||[Error Handling](Swift/Error%20Handling.md)|
|||Memory Safe|
|etc||[~= Operator](Swift/~%3D%20Operator.md)|
|||[zip](Swift/zip.md)|
|||[readLine()](Swift/readLine().md)|
|||[@escaping Closure](Swift/@escaping%20closure.md)|미완성|
|||[Handling Decimal Point](Swift/Handling%20Decimal%20Point.md)|
|||[First-Class Citizen](Swift/First-Class%20Citizen.md)|1급 객체|

## OOP(Object Oriented Programming)
### 🪧 Table of Contents
- [SOLID](OOP/SOLID.md)
  - [SRP(Single-Responsibility Principle)](OOP/SRP.md)   
  - [OCP(Open-Close-Principle)](OOP/OCP.md)
  - [LSP(Liskov Substitution Principle)](OOP/LSP.md)   
  - [DIP(Dependency Inversion Principle)](OOP/DIP.md)   
  - [ISP(Interface Segregation Principle)](OOP/ISP.md)      
  - [Value type cannot have a stored property that recursively contains it](Swift/Value%20type%20cannot%20have%20a%20stored%20property%20that%20recursively%20contains%20it.md)

## POP (Protocol-Oriented Language)
### 🪧 Table of Contents

## Commonly used protocols in Swift
- [Equatable](iOS/Equatable.md)
- [Comparable](iOS/Comparable.md)
- [Hashable](Swift/Hashable.md)    
- [Sendable](Swift/Sendable.md) -> 추후 정리 예정
- [CaseIterable](Swift/CaseIterable.md)

## Network
- [REST API](Network/REST%20API.md)   
- [Process vs Thread](Network/Process%20vs%20Thread.md)
- [Async vs sync](Network/Async%20vs%20sync.md)
- [Serial vs Concurrent](Network/Serial%20vs%20Concurrent.md)
- [GCD(Grand Central Dispatch)](Network/GCD(Grand%20Central%20Dispatch).md)

## Design-Pattern
- [Singleton](Design-Pattern/Singleton.md)
- [Factory-method](Design-Pattern/Factory-method.md)

## TDD (Test Driven Development)
- [Unit Test](TDD/UnitTest.md)
- [given-when-then](TDD/given-when-then.md)
- [XCTest](TDD/XCTest.md)
- [Adding test files to an already created project](TDD/Adding%20test%20files%20to%20an%20already%20created%20project.md)
- [🌐 Reference Site](TDD/ReferenceSite.md)

## Project - Setting
- [Device Setting](Project-Setting/Device%20Setting.md)
- [Install CocoaPods(M1 Error)](Project-Setting/Install%20Cocoapods.md)
- [Install RxSwift with CocoaPods(M1 Error)](Project-Setting/Install%20RxSwift%20with%20cocoapods.md)
- [UserInterfaceState.xcuserstate 제거하기](Project-Setting/UserInterfaceState%20xcuserstate.md)

## App 배포와 출시
- [CI/CD란?](https://github.com/JasonLee0223/TIL/blob/main/App%20%EB%B0%B0%ED%8F%AC%EC%99%80%20%EC%B6%9C%EC%8B%9C/CI,%20CD%EB%9E%80?.md)   