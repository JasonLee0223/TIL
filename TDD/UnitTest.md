# Unit Test

> UnitTest란?   
> 직역 그대로 `단위 테스트`라고 하며, 하나의 함수, 메서드를 기준으로 독립적으로 진행되는 가장 작은 단위의 테스트이다.
> 즉, 메서드를 하나하나 테스트 하는 것과 같은 맥락이다.

## 그럼 왜 필요할까?
1. 각각의 모듈을 부분적으로 확인할 수 있어 어떤 모듈에서 문제가 발생했는지 빠른 확인 가능하기 때문
2. 전체 프로그램을 빌드하는 대신 유닛 단위로 빌드해 확인하므로 시간 절약이 가능하다.

## 7가지 테스트 원칙(Seven Testing Principles)
1. 테스팅은 결합의 존재를 보여주는 것이다.
2. 완벽한 테스트는 불가능하다!
3. 테스트 구성은 빠른 시기에 시작한다.
4. 결합은 군집되어있다.
5. 살충제 역설(Persticide Paradox) - 비슷한 테스트가 반복되면 새로운 결함을 발견할 수 없다.
6. 테스팅은 정황에 의존적이다.
7. 오류 부재의 오해 - 사용되지 않는 시스템이나 기대에 부응하지 않는 기능은 결함을 찾고 수정하는 것은 의미가 없다.

## F.I.R.S.T UnitTest 원칙
UnitTest는 가장 작은 단위의 테스트이며, 모든 테스트의 시작점이다.   
UnitTest만 구성되어도 굉장히 많은 문제를 해결할 수 있으며, 코드 품질이 훨씬 좋아질 수 있다.   
- Fast - Unit Test는 빨라야한다.   
  즉, 비즈니스 로직에서 지치게 되니까 테스트코드는 빠르고 간략하게 진행한다.

- Isolated(고립된) - 다른 테스트에 종속적인 테스트는 절대 작성하지 않는다.   
  즉, 각각의 테스트 코드가 서로 다른 테스트 케이스에 영향을 주면 안된다.

- Repeatable - 테스트는 실행할 때마다 같은 결과를 만들어야한다.   
  즉, 언제 어떤 상황에서도 동일하게 반복할 수 있는 테스트 코드이면 좋다.
  
- Self-validating(자체 검증) - 테스트는 스스로 결과물이 옳은지 그른지 판단할 수 있어야한다.   
  특정 상태를 수동으로 미리 만들어야 동작하는 테스트 등은 작성하지 않는다.

- Timely(적시에) - UnitTest는 프로덕션 코드가 테스트를 성공하기 직전에 구성되어야 한다.   
  TDD 방법론에 적합한 원칙이지만 실제로 적용되지 않는 경우도 있다.   
  (예시. 옷을 사기전에 피팅을 해보는 것들)

## Practice
```Swift
// 함수명은 이 기능이 명확하게 어떤 일을 하는지 알 수 있도록 짓는다.
// 하여 메서드명을 한글로 작성하여 보다 명확하게 빨리 파악할 수 있도록한다.
func test_1더하기1은2다() {
	let calculator = Calculator()
	let result = calculator.add(1, 1)
	XCTAssetEqual(result, 2)
	XCTAssetEqual(result, 3).           // 에러 발생
}

// 주로 엣지값을 테스트를 많이한다.
// 엣지값 = 범위의 경계값을 보통 말한다.
func test_2더하기1은3이다() {
	let calculator = Calculator()
	let result = calculator.add(2, 1)
	XCTAssetEqual(result, 3)
}
```

```Swift
// system under test
let sut = Calculator()

func test_1더하기1은2다() {
	let result = sut.add(1, 1)
	XCTAssetEqual(result, 2)
	XCTAssetEqual(result, 3).           // 에러 발생
}
```