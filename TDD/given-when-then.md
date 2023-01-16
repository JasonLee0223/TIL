# given-when-then

## 🤔 왜 given / when / then 으로 나누어 작성할까??
이러한 흐름 방식을 BDD(Behavior Driven Development)라는 테스트 방식에서 가져온 것이다.   
시나리오를 설정하여 예상대로 결과가 흘러가는지 확인하는 방법론으로,   
어떤 상황이 주어지고(given)   
어떤 코드를 실행하고(when)   
결과를 확인하는(then) 단계로 구분하여 테스트 흐름을 보다 쉽게 파악함에 있다.   

## Test Format
- given: 필요한 모든 Value들을 셋팅하는 영역
- when: 테스트 중인 코드를 실행하기 위한 작성 영역
- then: 예상 결과 확인, 실패하는 경우의 메세지를 출력한다.

## 테스트가 이루어지는 방식
예제를 보고 기본적인 테스트가 이루어지는 방식을 확인해보자!

```Swift
func testArraySorting() {
    // given
	let input = [1, 7, 6, 3, 10]

    // when
    // 예상값과 결과값을 비교하는 식으로 진행된다.
	let expectation = [1, 3, 6, 7, 10]
	let result = input.sorted()

    // then
	XCTAssertEqual(result, expectation)
}
```

## Test Function
- XCTAssertGreaterThan: 대소 비교
- XCTAssertNil: nil인지를 판별
- XCTAssertThrowsError: 무엇을 throw하는 지
- XCTAssertTrue: 어떤 Bool값을 반환하는 지
- etc...

### 🌐 Reference Site
[GivenWhenThen](https://martinfowler.com/bliki/GivenWhenThen.html)