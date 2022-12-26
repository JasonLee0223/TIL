# File System Basics
파일 시스템은 데이터 파일, App 및 OS와 관련된 영구 저장소를 처리합니다.   
따라서 파일 시스템은 모든 프로세스에서 사용되는 기본 리소스 중 하나입니다.   
APFS는 macOS, iOS, watchOS 및 tvOS의 기본 파일 시스템입니다.   
기본 디렉터리 구조는 iOS와 macOS에서 비슷하지만 각 시스템이 앱과 사용자 데이터를 구성하는 방식에는 치이가 있습니다.   

파일 시스템과 상호 작용하는 코드를 작성하기 전에, 먼저 파일 시스템의 구성과 코드에 적용되는 규칙에 대해 약간 이해를 해야합니다.   
적절한 보안 권한이 없는 디렉토리에 파일을 쓸 수 없다는 기본 교의(tenet)외에,   
App도 좋은 시민이 되고 적절한 장소에 파일을 넣어야합니다.   
파일을 저장하는 위치는 플랫폼에 따라 다르지만   
**`중요한 목표는 사용자의 파일을 쉽게 검색할 수 있도록 하고,`**   
**`코드에서 내부적으로 사용하는 파일이 사용자의 방해를 받지 않도록 하는 것입니다.`**   

## About the iOS File System
iOS 파일 시스템은 `독자적으로 실행되는 앱을 대상`으로 합니다.   

### ⚙️ iOS Standard Directories: Where Files Reside (iOS 표준 디렉토리: 파일이 있는 곳)
보안을 위해 iOS앱과 파일 시스템의 사용작용은 Sandbox 디렉토리에 있는 디렉토리로 제한이 됩니다.   
새 App을 설치하는 동안, 설치 프로그램은 Sandbox 디렉토리 내에 App용 컨테이너 디렉토리를 만듭니다. 각 컨테이너 디렉토리에는 특정 역할이 있습니다.   
`Bundle` 컨테이너 디렉토리는 앱의 Bundle을 보유하고   
`Data` 컨테이너 디렉토리는 앱과 사용자 모두에 대한 데이터를 보유합니다.   
**`이 디렉토리는 앱이 데이터를 정렬하고 구성하는 데 사용할 수 있는 여러 하위 디렉토리로 더 나뉩니다.`**   
앱은 런타임에 추가 컨테이너 디렉토리(예시: iColud 컨테이너)에 대한 접근을 요청할 수 있습니다.   

<img src="https://user-images.githubusercontent.com/92699723/209491096-1634c2c4-e08e-490e-bc5c-1b145a045e27.png" width="400" height="400">   

위 그림은 App의 Sandbox 디렉토리를 보여주는 그림입니다.   
<img src="https://user-images.githubusercontent.com/92699723/209491409-83e11569-8161-4ff5-a22a-901c26e8967a.png" width="600" height="300">
위 그림은 App 디렉토리를 다운 받아서 위 데이터 컨테이너와 비교하여 확인되는 그림입니다.   

**`App은 일반적으로 컨테이너 디렉토리 외부에서 파일에 접근하거나 만들 수 없습니다.`**   
**`(= 외부에서 앱 내의 디렉토리에 접근하거나 파일을 만ㄷ르 수 없다.)`**   
이 규칙의 한가지 예외는 앱이 Public 시스템 인터페이스를 사용하여 사용자의 연락처나 음악과 같은 항목에 접근하는 경우입니다.

위 Sandbox 디렉토리 안의 있는 하위 디렉토리를 확인해보겠습니다.   
<img src = "https://user-images.githubusercontent.com/92699723/209493261-54b485db-c72d-4076-ae4c-d1560d1163d4.png" width="400" height="400">   

#### 🟢 Bundle Directory
- 파일 시스템 내 하나의 디렉터리
  - 실행 가능한 파일
  - info.plist
  - 각 종 Resources(이미지, 사운드, strings 등) 등을 그룹화

#### 🔴 Data Container -> Home Directory
- Data Container Home Directory = NSHomeDirectory()
- 기본 디렉토리
  - Documents
  - Library
  - tmp

#### 🔴 Data Container -> Document Folder
- 유저가 앱을 통해 생성한 문서나 데이터, 또는 외부 앱을 통해서 전송한 음악, pdf 등의
컨텐츠를 저장하는 곳
- 설정에 따라 유저가 직접 파일 추가 및 삭제 가능
  - ex) info.plist 에서 UIFileSharingEnabled = YES로 설정
- 따라서 유저에 의해 삭제되거나 내용이 변경되어도 무방하고 유저가 다루는 컨텐츠와 관련이 있는 파일들만 저장

#### 🔴 Data Container -> Document Folder -> Inbox
- 타 앱을 통해 전송받은 파일이 저장되는 디렉토리
  - ex) 메일 앱 첨부파일 등
- 파일을 읽거나 삭제할 수 있지만, 새 파일을 추가하거나 기존 파일 수정 불가
- 타 앱에서 받은 파일들은 덮어쓰기 대신 `[file-1, file-2]`처럼 번호가 자동으로 부여되면서 새 파일이 생성된다.

#### 🟣 Data Container -> Library Folder
- 유저 데이터 파일 및 임시 파일을 제외한 모든 파일들을 관리
- 유저에게 노출되는 것을 피하고 앱의 기능이나 관리에 필요한 파일 저장
- 주로 SubDirectory인 `Application Support`와 `Caches`를 이용하지만 커스텀 디렉터리 사용이 가능
- Preference, Cookies, Saved Application State, WebKit 등 필요할 때 시스템에서 자동 생성

#### 🟣 Data Container -> Library Folder -> Application Support
- 앱의 기능 또는 관리를 위해 지속적으로 관리해야되는 파일 저장
- Documents와 거의 동일한 속성을 가지지만, 유저에 대한 노출 여부에 따라 위치가 결정됩니다.
- 주로 BundleID 또는 회사명 등의 SubDirectory로 만들어 관리
- CoreData 기본 저장 경로
- Realm은 Documents 경로를 사용하는데 Documents는 노출이 되기 때문에 중요한 정보들이 저장되어있으면   
Application Support 폴더로 변경해서 사용하는 것이 좋다.

#### 🟣 Data Container -> Library Folder -> Caches
- 앱의 동작 속도/데이터 절약 등을 위해 사용되는 공간
  - ex) Background에서 Foreground로 넘어올 때 스냅샷 이미지로 사용됨.

#### 🔵 Data Container -> Temporary Directory
- 현재 앱 실행중에는 사용하지만 유지할 필요 없는 임시 파일 저장
- 사용 후 필요없어진 파일은 직접 삭제해주는 것을 권장

### 📲 Where You Should Put Your App's Files
iOS 디바이스의 동기화 및 백업 프로세스가 오래 걸리지 않도록 하려면, 파일을 저장할 위치를 선택하세요.   
대용량 파일을 저장하는 App은 iTunes또는 iCloud로 백업하는 과정을 지연시킬 수 있습니다.   
또한 이러한 App은 저장공간을 많이 차지하므로, 사용자가 앱을 삭제하거나 해당 앱의 데이터를 iCloud에 백업하지 못하도록 유도할 수 있습니다.   
이를 염두에 두고, 다음 가이드라인에 따라 앱 데이터를 저장해야합니다.

- **`Documents/ 에 사용자 데이터를 입력하세요.`**
  - 사용자 데이터에는 일반적으로 사용자에게 공개하려는 파일(사용자가 생성, 가져오기, 삭제 또는 편집할 수 있는 모든 파일)이 포함됩니다.
  - 그리기 App의 경우, 사용자 데이터에는 사용자가 만들 수 있는 모든 그래픽 파일이 포함됩니다.   
  - 비디오 및 오디오 App에는 사용자가 나중에 시청하거나 듣기위해 다운로드한 파일도 포함 될 수 있습니다. -> **`사용자 데이터는 다 여기 넣으라는 말`**

- **`Library/Application support/ 디렉토리에 App에서 만든 support 파일을 넣으세요.`**
  - 일반적으로 이 디렉토리는 앱이 실행하는데 사용하지만, `사용자에게 숨겨져 있어야 하는 파일을 포함`합니다.
  - 이 디렉토리에는 데이터파일, 구성파일, 템플릿 및 앱 번들에서 로드된 수정 된 버전의 리소스도 포함 될 수 있습니다.   

- **`Documents/ 와 Application Support / 디렉토리의 파일은 기본적으로 백업된다는 점을 기억하세요.`**
  - NSURLIsExcludedFromBackupKey를 사용하여 백업에서 파일을 제외할 수 있습니다.   
  ```Swift
  var resourceValues: URLResourceValues = URLResourceValues()
  resourceValues.isExcludedFromBackup = true
    do {
        try fileUrl.setResourceValues(resourceValues)
    }
  ```
  - 여기서 `fileUrl`은 백업에서 제외시키고 싶은 파일의 URL입니다.   
  다시 만들거나 다운로드 할 수 있는 파일은 백업에서 제외해야합니다.   
  이는 대용량 미디어 파일에 특히 중요합니다.
  App에서 비디오 또는 오디오 파일을 다운로드 하는 경우, 해당 파일이 백업에 포함되어 있지 않은지 확인하세요.

- **`임시 데이터를 tmp/ 디렉터리에 저장하세요.`**
  - 임시 데이터는 오랜 기간동안 유지 할 필요가 없는 모든 데이터로 구성됩니다.   
  - 사용자의 디바이스에서 공간을 계속 소비하지 않도록 파일을 삭제해야합니다.
  - 앱이 실행되고 있지 않을 때, 시스템에서 주기적으로 파일을 삭제합니다.

- **`Library / Caches / 데렉터리에 데이터 캐시 파일을 저장합니다.`**
  - 캐시 데이터는 임시 데이터보다 오래 지속되어야 하지만, Support 파일이 아닌 모든 데이터에 사용될 수 있습니다.
  - 일반적으로 App은 캐시 데이터가 제대로 작동하는 것을 요구하지 않지만, 캐시 데이터를 사용하여 성능을 향상시킬 수 있습니다.
  - 캐시 데이터의 예로는 DB 캐시 파일과 일시적으로 다운로드 할 수 있는 Contents가 있습니다.
  - 시스템에서 Caches/디렉터리를 삭제하여 디스크 공간을 비울 수 있으므로, 앱이 필요에 따라 이러한 파일을 다시 만들거나, 다운로드 할 수 있어야 한다.

< @Blue의 FileSystem 정리>
<img src= "https://user-images.githubusercontent.com/92699723/209509098-fe49d5e4-e732-4cb4-9445-2d9c4515b016.png">

## 🌐 Reference Site
[[Apple] File System Basics](https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/FileSystemOverview/FileSystemOverview.html#//apple_ref/doc/uid/TP40010672-CH2-SW12)   
[[iOS] File System 구조](https://velog.io/@leeyoungwoozz/iOS-File-System-%EA%B5%AC%EC%A1%B0)   
[[iOS] 파일시스템(File System)](https://jinshine.github.io/2019/01/19/iOS/UserDefaults.1/)   
[[Zedd0202]File System Programming Guide](https://zeddios.tistory.com/435)   
[[Zedd0202]iOS ) 내 App의 데이터 보기](https://zeddios.tistory.com/437)   
