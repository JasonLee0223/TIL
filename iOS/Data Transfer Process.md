# Data Transfer Process
ViewController간에 데이터를 어떻게 전송할 것인지 이전부터 무의식적으로 사용하던 것들이 많았는데 `하나의 ViewController에 2개의 View를 넣고 서로 통신할 수 있지않을까...??` 라는 생각에 찾아보다가 한 번 정리하며 익히면 좋을 것 같다고 생각되어 작성하게되었다.

## VC간의 데이터를 전달하는 방식은 크게 2가지로 나뉜다.
A. 직접 전달 방식(동기 방식) : 데이터를 직접 넘겨주는 방법   
- present,push시 프로퍼티에 접근해 넘겨주는 방식   
- Segue prepare 메소드를 활용해서 데이터를 넘겨주는 방식   
- Protocol / Delegation을 활용해서 데이터를 넘겨받는 방식   
- Closure를 활용해서 데이터를 넘겨받는 방식   
- NotificationCenter를 활용해 데이터를 넘기는 방식   

B. 간접 전달 방식(비동기 방식) : 데이터를 다른곳에 저장해두고, 필요할 때 꺼내가는 방식
- AppDelegate.swift 활용   
- UserDefaults 사용하기   
- CoreData or Realm 활용하기   

### 여기서 제일 자주 사용하는 방법 4가지
- `객체의 프로퍼티 접근`해서 데이터 넘기기   
- delegate 패턴 사용하기   
- Closure 사용하기   
- Notification 사용하기

## 1.객체의 프로퍼티 접근해서 데이터 넘기기   

## 2. Delegate로 데이터 전달

## 3. Closure로 데이터 전달

## 4. NotificationCenter로 데이터 전달


### 🌐 참고사이트   
[iOS 화면 전환 간 데이터 전달 방법](https://jinsangjin.tistory.com/95)   
[[iOS] 데이터 전달 방식 4가지 - property, delegate, closure, NotificationCenter](https://hellozo0.tistory.com/365)   
[Swift에서 데이터 전달하는 6가지 방법 정리!!](https://i-colours-u.tistory.com/6)   
[[iOS] View Controller들 사이에서 Data 주고받는 6가지 방법](https://sweetdev.tistory.com/110)   
[[iOS] 화면간 데이터 전달하기](https://velog.io/@heyksw/iOS-%ED%99%94%EB%A9%B4%EA%B0%84-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%84%EB%8B%AC%ED%95%98%EA%B8%B0)   
[[iOS] VC 간 데이터 전달 방법](https://velog.io/@nnnyeong/iOS-VC-%EA%B0%84-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%84%EB%8B%AC-%EB%B0%A9%EB%B2%95)   
