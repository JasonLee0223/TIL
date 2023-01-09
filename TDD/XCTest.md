# XCTest

## 1️⃣ XCTest란?
Unit Test, Performance Test(성능 테스트), UI Test를 만들고 실행하는 프레임워크

## 2️⃣ XCTestCase란?
`추상 클래스인 XCTest의 하위 클래스로, 테스트를 작성하기 위해 상속해야하는 가장 기본적인 클래스.`   
XCTest는 테스트를 위한 프레임워크의 이름이기도 하고, 테스트에서 가장 기본이 되는 추상 클래스의 이름이기도하다.   
해당 클래스를 상속받은 클래스에서는 test에서 사용되는 다양한 프로퍼티와 메서드를 사용할 수 있다.   

## 3️⃣ 초기 UnitTest 항목
<img src="https://user-images.githubusercontent.com/92699723/211242321-c27c6677-778c-41e6-bdcc-c481348cde69.png">

- setUpWithError() → 초기화코드(객체를 만드는 부분)   
각각의 test case가 실행되기 전마다 호출되어 각 테스트가 모두 같은 상태와 조건에서 실행될 수 있도록 만들어줄 수 있는 메서드.

- testDownWithError() → 해제코드   
각각의 test 실행이 끝난 후마다 호출되는 메서드.   
보통 setUpWithError()에서 설정한 값들을 해제할 때 사용된다.   

- testExample()   
test로 시작하는 메서드들은 작성해야 할 test case가 되는 메서드다.   
테스트할 내용을 메서드로 작성해 볼 수 있다.   
메서드 네이밍은 무조건 test로 시작되어야한다.   

- testPerformanceExample()   
성능을 테스트해보기 위한 메서드다. → 성능 테스트가 필요한 것이 아니라면 삭제해도 된다.   
XCTestCase의 measure(block:)라는 메서드를 통해 성능을 측정   

## Practice
```Swift
// 여기서는 Fast 원칙에 맞춰 옵셔널 처리로 하게되면 계속 바인딩을 해줘야해서 예외적으로 강제 언래핑을 사용한다.
var sut: LottoMachine!

// 1, 4
override func setUpWithError() throws {
	try super.setUpWithError()

}

// 3, 6
override func tearDownWithError() throws {
	try super.tearDownWithError()
	sut = nil
}

// 2
func testExample() throws {

}

// 5
func testExmaple2() throws {

}

// 한글로 테스트 메서드명을 작성하는게 Fast 원칙에 맞아서 한글로 작성한다.
func test_6개보다_적은_숫자를_입력했을때_False이다() {
	let input = [1,2,3]

	let result = sut.isValidLottoNumbers(of: input)
	XCTAssertEqual(result, false) // XCT -> XcodeTest 줄인말
}

// 테스트 코드는 메서드명 제일 앞에 test 키워드를 꼭 적어줘야한다!
func test_배열안의_숫자가_1에서_45사이의_숫자이다() {
	// given
	let input = [1,2,3,4,5]

	// when
	let result = sut.isValidLottoNumbers(of: input)
	
	// then
	XCTAssertEqual(result, false)
}

// 내가 만든 테스트 코드
func test_배열안의_랜덤숫자가_1에서_45사이의_숫자가아니면_false를_반환한다() {
	// given
	// 기존에 메서드로 Random을 지원해줘서 필요없을 것 같다!
	let input = sut.makeRandomLottoNumbersArray()
	
	// when
	let expectation = [1,2,3,4,46]
	let result = Set(input)
	
	// then
	XCTAssertEqual(result, false)    // ??
}
```