# given-when-then

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

### 🌐 Reference Site
[GivenWhenThen](https://martinfowler.com/bliki/GivenWhenThen.html)