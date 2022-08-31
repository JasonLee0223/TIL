# Handling Decimal Point (소수점 다루기)

## 순서
1. 반올림(round)
2. 올림(ceil)
3. 내림(floor)
4. 버림(trunc)
5. n번째 소수점 자르기

### 1. round()
소수점 이하를 반올림 한다. 5 이상은 1로 올리고 미만은 버린다.
```Swift
import Foundation

ceil(10.1) // 10
ceil(8.7)  // 9
ceil(6.5)  // 7
```

### 2. ceil()
소수점 이하를 모두 버리고 정수부에 +1을 해준다.
```Swift
import Foundation

ceil(10.1) // 11
ceil(8.7)  // 9
ceil(6.5)  // 7
```

### 3. floor()
소수점 이하를 모두 버린다.
```Swift
import Foundation

ceil(10.1) // 10
ceil(8.7)  // 8
ceil(6.5)  // 6
```

### 4. trunc()
trunc을 사용하면 말 그대로 소수점을 버립니다. 정수부에는 아무런 영향을 주지 않고 소수점만 지워버립니다.
```Swift
import Foundation

trunc(5.7)  // 5.0
trunc(-3.4) // -3.0
trunc(-4.6) // -4.0
```

### 5. n번째 소수점 자르기
소수점이 원하지않는만큼 길거나, 원하는 자릿수만큼 필요한 경우 소수점을 원하는 n번째까지만 자르는 방법.   
`String(format:_:...)`을 사용한다.  
format이 중요한데 `%.nf`를 사용하며, n번째 까지 소수점을 제거한다는 format입니다.   
return값은 String이며 사용할 때 잘 확인하시길 바랍니다. 
```Swift
let decimal = 5.12337092375920485
String(format: "%.3f", decimal) // "5.123"
String(format: "%.6f", decimal) // "5.123370"
```

### 🌐 참고사이트   
[[Swift ] 소수점 다루기(ceil, floor, round, String format...)](https://leeari95.tistory.com/10)   
[[Swift] 소수점 다루기 반올림(round), 올림(ceil), 내림(floor) 등등](https://formestory.tistory.com/21)