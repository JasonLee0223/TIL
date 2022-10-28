# Async vs sync

## 🟢 Synchronous(동기)
요청에 대한 응답이 **동시에 발생해야한다.**   
즉, 내 작업이 끝나기 전까진 다른 작업을 수행하지 못한다.   
우리가 평소에 별도의 작업 없이 쭉쭉 써내려가던 코딩이 대부분 Synchronous였다.   


## 🟢 Asynchronous(비동기)
Synchronous와 반대의 개념으로 요청에 대한 응답이 **동시에 발생하지 않는다.**   
즉, 내 작업이 끝나기 전에 다음 작업을 실행한다.


### 🟣 정리 
||Synchronous|Asynchronous|
|---|:---|:---|
|정의|요청에 대한 응답이 동시에 이루어져야한다.<br />모든 작업을 `순차적`으로 진행한다.|요청에 대한 결과가 동시에 일어나지 않는다.<br />모든 작업을 `동시에` 진행한다.|
|장점| 설계가 간단하고 직관적이다.|응답이 주어질 때까지 기다리지 않고<br />다른 작업을 하므로 자원을 효율적으로 사용할 수 있다.|
|단점|응답이 주어질 때까지 다른 일을 진행할 수 없고 대기해야한다.|동기보다 설계가 복잡하다.|

### 코드 예시
```Swift
// Sync
sleep(3)
print("3초 뒤에 결과가 나옵니다.")  // -> 3초 뒤에 결과가 나온다.

// Async
DispatchQueue.main.async() {
    sleep(3)
    print("3초 뒤에 결과가 나올까요?.")
}
print("비동기라 동시에 출력됩니다.")  // -> sleep 작업과 동시에 출력된다.
```

### 🌐 Reference Site
[iOS) Sync vs Async / Serial vs Concurrent](https://babbab2.tistory.com/64?category=831129)