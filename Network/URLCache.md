# URLCache

> 💡 URL 요청을 캐시된 응답 개체에 매핑하는 개체입니다.


URLCache 클래스는 NSURLRequest 개체를 CachedURLResponse 개체에 매핑하여 URL 로드 요청에 대한 응답 캐싱을 구현합니다.    
복합 인-메모리 및 온-디스크 캐시를 제공하고 부분의 크기를 조작할 수 있습니다.   
캐시 데이터가 지속적으로 저장되는 경로를 제어할 수도 있습니다.  

> iOS에서는 시스템의 디스크 공간이 부족할 떄 온-디스크 캐시가 제거될 수 있지만 앱이 실행되고 있지 
않을 때만 가능합니다.

## Thread Safety

iOS 8 이상 및 macOS 10.10 이상에서 URLCache는 스레드로부터 안전합니다.

URLCache 인스턴스 메서드는 동시에 여러 실행 컨텍스트에서 안전하게 호출할 수 있지만 `cachedResponse(for:)` 및 `storeCachedResponse(_: for:)`와 같은    
메서드는 동일한 요청에 대한 응답을 읽거나 쓰려고 시도할 때 피할 수 없는 경합 상태(Race Condition)가 있음을 유의하십시오.   
URLCache의 하위 클래스는 스레드로부터 안전한 방식으로 재정의된 메서드를 구현해야 합니다.    

## Subclassing Notes

URLCache 클래스는 있는 그대로 사용하기 위한 것이지만 특정 요구 사항이 있을 때 하위 클래스로 만들 수 있습니다.

예를 들어 어떤 응답이 캐시되는지 확인하거나 보안 또는 기타 이유로 저장 메커니즘을 다시 구현해야 할 수 있습니다.

이 클래스의 메서드를 재정의할 때 작업 매개 변수를 사용하는 메서드가 그렇지 않은 메서드보다 시스템에서 선호된다는 점에 유의하십시오.     
따라서 다음과 같이 서브클래싱할 때 작업 기반 메서드를 재정의해야 합니다.       

- 캐시에 응답 저장    
    요청 기반  `storeCachedResponse(_: for:)` 대신 또는 추가로 작업 기반 `storeCachedResponse(_: for:)` 를 재정의합니다.

- 캐시에 응답 받기    
    `cachedResponse(for: )` 대신 또는 이에 추가하여 `getCachedResponse(for: completionHandler:)` 를 재정의합니다.

- 캐시된 응답 제거    
    요청 기반 `removeCachedResponse(for: )` 대신 또는 추가로 작업 기반 `removeCachedResponse(for: )` 를 재정의합니다.