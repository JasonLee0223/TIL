# typealias
Swift에서 기본으로 제공하는 데이터 타입이거나, 사용자가 임의로 만든 데이터 타입이거나   
임의로 별칭(별명, 다른 이름)을 부여할 수 있습니다.   

```Swift
typealias MyInt = Int
typealias YourInt = Int
typealias MyDouble = Double

let age: MyInt = 100        // MyInt == Int 같은 의미의 또 다른 이름으로 정의합니다.
var year:YourInt = 2080     // YourInt == Int 같은 의미의 또 다른 이름으로 정의합니다.

year = age
let month: Int = 7
let percentage: MyDouble = 99.9
```