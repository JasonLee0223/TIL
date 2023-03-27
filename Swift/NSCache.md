# NSCahe
> 💡 Resource(자원)가 부족할 떄 제거될 수 있는 임시 Key-Value 쌍을 임시로 저장하는 데 사용하는 변경 가능한 컬렉션이다.

## Declaration (선언)

```swift
class NSCache<KeyType, ObjectType> : NSObject where KeyType : AnyObject, ObjectType : AnyObject
```

## Overview

> 캐시 객체는 몇 가지 면에서 다른 가변 컬렉션(Array, Dictionary, Set 등)과 다릅니다.

- NSCache 클래스는 캐시가 시스템 메모리를 너무 많이 사용하지 않도록 다양한 자동 제거 정책을
통합합니다.   
다른 애플리케이션에 메모리가 필요한 경우 이러한 정책은 캐시에서 일부 항목을 제거하여
메모리 사용 공간을 최소화합니다.    
- 캐시를 직접 잠그지 않고도 다른 스레드에서 캐시의 항목을 추가, 제거 및 쿼리할 수 있습니다.     
- `NSMutableDictionary` 객체와 달리 캐시는 캐시에 넣은 키 객체를 복사하지 않습니다.     

> 일반적으로 NSCache 객체를 사용하여 생성 비용이 많이 드는 임시 데이터가 있는 객체를 임시로 
저장합니다.

> 이러한 객체를 재사용하면 해당 값을 다시 계산할 필요가 없기 때문에 성능상의 이점을 얻을 수 있습니다.

그러나 객체는 응용 프로그램에 중요하지 않으며 메모리가 부족한 경우 삭제할 수 있습니다.  
만약 폐기된 경우 해당 값은 필요할 때 다시 계산해야 합니다.  
사용하지 않을 때 버릴 수 있는 하위 구성 요소가 있는 객체는 캐시 제거 동작을 개선하기 위해 `NSDiscardableContent` 프로토콜을 채택할 수 있습니다.     
기본적으로 캐시의 `NSDiscardableContent` 객체는 콘텐츠가 삭제되면 자동으로 제거되지만 이 자동 제거 정책은 변경할 수 있습니다.

`NSDiscardableContent` 객체가 캐시에 저장되면 캐시는 제거 시 그에 대한 `discardContentIfPossible()` 메서드를 호출합니다.

### 🌐 Reference Site
[NSCache | Apple Developer Document](https://developer.apple.com/documentation/foundation/nscache)