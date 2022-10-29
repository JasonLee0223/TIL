# GCD(Grand Central Dispatch)

## 🟢 GCD란?
Multi Thread 환경에서 어떠한 일련의 작업들이 Concurrency하게 처리될 수 있도록 해주는 하나의 기술.

## 🟢 Dispatch: 보내다, 발송

- Queues and Tasks (대기열 및 작업)
  - DispatchQueue
  - DispatchWorkItem
  - DispatchGroup

- Thread Scheduling (쓰레드 스케쥴링)
  - DispatchQos

- System Event Monitoring (시스템 이벤트 모니터링)
  - DispatchSource
  - DispatchIO
  - DispatchData
  - DispatchDataIterator
  - DispatchSourceProtocol

- Task Synchronization (작업 동기화)
  - DispatchSemaphore

- Time Constructs (시간 구성)
  - DispatchTime
  - DispatchWallTime
  - DispatchTimeInterval
  - DispatchTimeoutResult

- Dispatch Objects (디스패치 객체)
  - DispatchObject
  - DispatchPredicate

## 🟢 DispatchQueue(GCD)의 종류
1. main Queue: Serial
2. global Queue: Concurrent / Qos 설정
3. private Queue: Default Serial(Concurrent로 변경 가능) / Qos 추론

## 🟢 Main Queue
`DispatchQueue.main`   
- `Serial (직렬)`
- 오직 한 개만 존재하며 `Main Thread`에서 동작한다.
- UI 처리를 담당

## 🟢 Global Queue
`DispatchQueue.global(qos:)`
- `Concurrent(동시)`: 여러 개의 Thread로 분산 처리
- `QoS(Quality of Service)`에 따라 6종류로 나뉜다.   
  Reference -> [DispatchQoS.QoSClass | Apple Developer Documentation](https://developer.apple.com/documentation/dispatch/dispatchqos/qosclass)
    ```Swift
    // 유저와 직접 인터렉티브: UI 관련 (즉시)   
    DispatchQueue.global(qos .userInteractive)

    // 반드시 필요, 비동기 처리: 앱 내에서 첨부파일을 열기, 내부 데이터베이스 조회 등
    DispatchQueue.global(qos: .userInitiated)

    // 일반적인 작업(default)
    DispatchQueue.global()

    // ProgressIndicator와 함께 길게 사용되는 작업: 지속적인 데이터 feed, Networking 
    DispatchQueue.global(qos: .utility)

    // 사용자가 직접적으로 인지하지 못하는 부분: 데이터베이스 유지 등
    DispatchQueue.global(qos: .background)

    // 사용하지 않음 legacy API
    DispatchQueue.global(qos: .unspecified)
    ```
- 작업을 Thread에 배치하는 일은 OS에서 알아서 처리한다.
- 우선순위가 더 높은 Queue의 작업을 `우선적으로 더 많은 Thread에 배치`하고 `배터리를 집중적으로 소모`하게 된다.

## 🟢 Private Queue
`DispatchQueue(label:)`   
`DispatchQueue(label:, attribute:)`

- 기본값: Serial (Concurrent로 변경 가능)
- QoS설정 가능: 굳이 설정하지 않아도 OS가 알아서 QoS를 추론하게 된다.   
  하여 label을 설정해주면 된다.

### 🌐 Reference Site
[[iOS] 디스패치큐(GCD)의 종류와 특징, 그리고 주의사항](https://tngusmiso.tistory.com/49)      
[[iOS - swift] DispatchQueue, main, global 사용하여 큰 파일 로드 방법 (스레드 처리, sync, async, concurrent, serial)](https://ios-development.tistory.com/938)   
[iOS) GCD (Grand Central Dispatch)](https://babbab2.tistory.com/65?category=831129)   
[Grand Central Dispatch (GCD에 관하여..)](https://burzum17.tistory.com/8)   
[Dispatch | Apple Developer Documentation](https://developer.apple.com/documentation/DISPATCH)   
[DispatchQueue | Apple Developer Documentation](https://developer.apple.com/documentation/dispatch/dispatchqueue)