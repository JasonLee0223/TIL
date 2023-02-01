# Tuple
튜플(Tuple)은 타입의 이름이 따로 지정되어 있지 않은, 프로그래머 마음대로 만드는 타입이다.   
**`지정된 데이터의 묶음`** 이라고 표현할 수 있다.   

 ```Swift
 // String, Int, Doulbe 타입을 갖는 튜플
 var person: (String, Int, Double) = ("Jason", 100, 181)

 // Index로 접근하여 값을 사용할 수 있다.
 print("이름: \(person.0), 나이: \(person.1), 신장: \(person.2)")

// Index를 통해 값을 할당할 수 있다.
 person.1 = 50
 person.2 = 160.5

 print("이름: \(person.0), 나이: \(person.1), 신장: \(person.2)")
 ```