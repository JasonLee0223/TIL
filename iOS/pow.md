# pow() & sqrt()
## 제곱구하기
```Swift
pow(_ x: Decimal, _y: Int) -> Decimal
```
pow(제곱할 값, 제곱 수)

```Swift
import Foundation

let value = 3.0
pow(value, 2)       // 9.0
```

## 제곱근 구하기
```Swift
func sqrt(_: Double) -> Double
```

```Swift
import Foundation

let value = 9.0
sqrt(value)         // 3.0
```

### Reference Site
[[Swift] 제곱 함수 pow, 제곱근 함수 sqrt](https://hongssup.tistory.com/297)   
[pow(_:_:) | Apple Developer Documentation](https://developer.apple.com/documentation/foundation/1779833-pow)   