# Logging
통합 로깅 시스템을 사용하여 디버깅 및 성능 분석을 위해 앱에서 원격 분석을 기록합니다.   
Log Message는 앱의 런타임 동작에 대한 지속적인 기록을 제공하고 다른 기술을 사용하여 쉽게 포착할 수 없는 문제를 더 쉽게 식별할 수 있도록 합니다.   
통합 로깅 시스템은 로그 데이터 저장을 메모리와 디스크의 데이터 저장소에 모읍니다.   
모든 level의 시스템에서 메시징을 기록할 수 있는 효율적인 단일 고성능 API를 제공합니다.
> Important   
> iOS 10.0 이상, macOS 10.12이상, tvOS 10.0이상, watchOS 3.0이상에서 사용할 수 있다.

## Essentials
- Generating Log Messages from Your Code(코드에서 로그 메세지 생성)
- Viewing Log Messages(로그 메세지 보기)
- Customizing Logging Behavior While Debugging(디버깅 중 로깅 동작 사용자 지정)

## Log Messages
### struct Logger 
- Creating a Logger
  - 🔴 class OSLog
    Createing a Log
    - init(subsystem: String, category: String)
    - init(subsystem: String, category: OSLog.Category)
    - struct OSLog.Category
    
    Getting the Shared Logs
    - static let 'default': OSLog
    - static let disabled: OSLog
    
    Getting Log Configuration
    - func isEnabled(type: OSLogType) -> Bool
    - var signpostsEnabled: Bool
- Logging a Message
  - func log(OSLogMessage...)
  - func log(level: OSLog...)
  
  - struct OSLogType
  
  - struct OSLogMessage 
- 🔴 Logging a Scoped Message
  - func notice(OSLogMessage)
  - func debug(OSLogMessage)
  - func trace(OSLogMessage)
  - func info(OSLogMessage)
  - func error(OSLogMessage)
  - func warning(OSLogMessage)
  - func fault(OSLogMessage)
  - func critical(OSLogMessage)

### Message Argument Formatters(메시지 인수 포맷터)

### Legacy Logging Symbols(레거시 로깅 기호)

## Measure Events

### Recording Performance Data

### struct OSSignposter

### Legacy Signpost Symbols

### 🌐 참고사이트   
[Apple Develop - Logging](https://developer.apple.com/documentation/os/logging)   
[Apple Develop - Logger](https://developer.apple.com/documentation/os/logger)
[Apple Develop - OSLog](https://developer.apple.com/documentation/os/oslog)
[Zedd0202 - os_log](https://zeddios.tistory.com/979)
[[Swift] OSLog 시스템 로그 함수](https://velog.io/@bibi6666667/Swift-OSLog-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EB%A1%9C%EA%B7%B8-%ED%95%A8%EC%88%98)