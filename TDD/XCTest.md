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