# Higher-order Funtion
> 다른 함수를 전달인자로 받거나 함수 실행의 결과를 함수로 반환하는 함수를 말한다.   
> 스위프트의 함수(Closure)는 First-Class Citizen이기 때문에 함수의 전달인자로 전달할 수 있으며,   
> 함수의 결과값으로 반환할 수 있습니다.   

< 특징 >
1) 변수에 저장할 수 있다.
2) 매개변수로 전달할 수 있다.
3) 리턴값으로 사용할 수 있다.

## map
 - 컨테이너가 담고 있던 **각각의 값을 매개변수를 통해 받은 함수에 적용한 후** 새로운 컨테이너를 생성하여 반환   
 (= 컨테이너 내부의 **기존 데이터를 변형(Transform)하여 새로운 컨테이너를 생성**한다.)
 - 기존 컨테이너의 값은 변경되지 않음
 - **시퀀스(Sequence), 콜렉션(Collection), protocal**을 준수하는 타입과 옵셔널은 
 map 사용할 수 있음
 - Array, Dictionary, Set, Optional
 - for - in 구문 사용하는 것과 비슷하나 코드가 더 간결
 
 ```swift
 let arr = [0, 1, 2, 3]
 let num = arr.map( { (x: Int) -> Int in
 	return x + 1
 })
 print(arr)
 print(num) // [1, 2, 3, 4]
 
 var arr1 = arr.map { $0 + 1 }
 print(arr1)
 // .indices 메소드 한 번 찾아보기 유용하게 쓰일 것 같다!
 ```

## filter
  - 컨테이너가 담고 있던 각각의 값을 조건에 맞는 새로운 값만 추출하여 반환   
  (컨테이너 내부의 **값을 걸러서 새로운 컨테이너로 추출**한다.)
  - 콜렉션 내부의 기존 데이터를 돌면서 특정 조건에 맞는 것만 선택하는 것
  
  ```swift
  let arr = [1, 2, 3, 4, 5]
  var f = [Int]()
  for x in arr {
  	if x % 2 == 0 {
  		f.append(x)
  	}
  }
  print(f) // [2, 4]
  var filteredArr = arr.filter { $0 % 2 == 0 }
  print(filteredArr) // [2, 4]
  
  filteredArr = arr.filter { $0 % 2 != 0 }
  print(filteredArr) // [1, 3, 5]
  ```

## reduce
- 컨테이너 내부의 값을 **하나로 통합(연산)** 하여 리턴
- .reduce(**초기값**) { (**누적값 + 배열에 존재하는 값**) }

```swift
var x = ["a", "1", "c", "AB", "한"]
var x1 = x.joined()
print(x1) // a1cAB한

var x2 = x.reduce( "result", {$0 + $1} )
print(x2) // resulta1cAB한

let y2 = ["a", "b", "c", "d"]
let y3 = y2.reduce("결과 = ") { $0 + $1 } // 후행 클로저
print(y3) // 결과 = abcd
```

## forEach    
 - for-in 구문은 우리가 직접 구현하는 반복문
 - forEach는 내가 반복하고 싶은 구문을 forEach라는 함수의 파라미터로 ‘클로저'로 작성해서 넘겨준다.
 - 그러므로 continue, break는 사용불가능 But! return을 통해 빠져나갈 수 있다.
 ```Swift
 let testArray = [1, 2, 3, 4, 5]

 for index in testArray { print(index) } // 결과: 1 2 3 4 5
 testArray.forEach { print($0) }         // 결과: 1 2 3 4 5
 ```

## compactMap
  - map과 사용법이 같음
  - Returns an array containing the non-nil results of calling the given transformation with each element of this sequence.
  
  ```swift
  let x: [Int?] = [0, 1, 2, nil, 4]
  let map = x.map { $0 }
  let cMap = x.compactMap { $0 }
  print(map) // [Optional(0), Optional(1), Optional(2), nil, Optional(4)]
  print(cMap) // [0, 1, 2, 4], nil값을 제거하고 나머지는 언래핑한 베열
  ```

### 🌐 참고사이트   
[야곰 스위프트 기본 문법 강좌](https://yagom.github.io/swift_basic/contents/22_higher_order_function/)