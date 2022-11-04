#  REST API

## 🟢 1. REST란?
REST(Representational State Transfer)라는 용어의 약자로   
- Representational: 구상주의적인?, 구체적인 <-> abstract(추상적인)   
- State: 상태   
- Transfer: 이동하다.   

모두 이어서 말해보면 "구체적인 상태를 이동한다."라고 이해할 수 있겠다!   
2000년도에 로이 필딩(Roy Fielding)의 박사 학위 논문에서 최초로 소개되었다.   
로이 필딩은 HTTP의 주요 저자 중 한 사람으로 그 당시 웹(HTTP) 설계의 우수성에 비해 제대로 사용되어지지 못하는   
모습에 안타까워하며 웹의 장점을 최대한 활용할 수 있는 아키텍처로서 REST를 발표했다고 한다.   

즉, **`자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미한다.`**   
구체적인 개념으로, `HTTP URI를 통해 자원을 명시`하고,    
`HTTP Method를 통해 해당 자원에 대한 CRUD Operation을 적용`하는 것을 의미한다.

### CRUD Operation
- Create: 생성 (POST)
- Read: 조회 (GET)
- Update: 수정 (PUT)
- Delete: 삭제 (DELETE)
- HEAD: header 정보 조회 (HEAD)

## 🟢 2. REST 구성
쉽게 표현하면 아래의 3가지 구성으로 이루어져있다.   
- 자원(Resource) - URI
  - 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
- 행위(Verb) - HTTP METHOD
  - HTTP 프로토콜의 Method를 사용한다.
  - HTTP 프로토콜은 `GET, POST, PUT, DELETE` 와 같은 메서드를 제공한다.
- 표현(Representations)
  - Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
  - REST에서 하나의 자원은 `JSON, XML, TEXT, RSS`등 여러 형태의 Representation으로 나타내어질 수 있다.
  - 보통 JSON 혹은 XML을 통해 데이터를 주고 받는 것이 일반적이다. 

## 🟢 3. REST의 특징
1. Uniform (유니폼 인터페이스)   
    Uniform Interface는 URI로 지정한 리소스에 대한 `조작을 통일`되고 `한정적인 인터페이스로 수행`하는   
    아키텍쳐 스타일을 말한다.
2. Stateless (무상태성)   
   REST는 무상태성 성격을 갖는다.   
   `다시 말해 작업을 위한 상태 정보를 따로 저장하고 관리하지 않는다.`   
   세션 정보나 쿠키 정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만을 단순히 처리하면 된다.   
   때문에 **서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로서 구현이 단순해진다.**
3. Cacheable (캐시 가능)   
   REST의 가장 큰 특징 중 하나는 **`HTTP라는 기존 웹 표준을 그대로 사용하기 때문에`**,   
   웹에서 사용하는 기존 인프라를 그대로 활용이 가능합니다.   
   따라서 HTTP가 가진 캐싱 기능이 적용 가능하다.   
   HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.   
4. Self-descriptiveness (자체 표현 구조)   
   REST의 또 다른 큰 특징 중 하나는 **`REST API 메세지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조`**
   로 되어있다.
5. Client - Server 구조   
   REST 서버는 API제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조로   
   각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고   
   서로 간의 의존성이 줄어들게된다.
6. 계층형 구조
   REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해   
   구조상의 유연성을 둘 수 있고, PROXY, GateWay 같은 네트워크 기반의 중간 매체를 사용할 수 있게 한다.   

---

## 🔴 4. REST API란?
- API(Application Programming Interface)   
  데이터와 기능의 집합을 제공하여 프로그램간 상호작용을 촉진하며, 서로 정보를 교환가능 하도록 하는 것.
- REST API
  - REST 기반으로 서비스 API를 구현하는 것
  - 최근 Open API, 마이크로 서비스등을 제공하는 업체 대부분은 REST API를 제공한다.  

## 🔴 5. REST API 디자인 가이드
REST API 설계 시 가장 중요한 항목은 다음의 2가지로 요약할 수 있다.   

**첫 번째,** URI는 정보의 자원을 표현해야한다.   

**두 번째,** 자원에 대한 행위는 HTTP Method (GET, POST, PUT, DELETE)로 표현한다.   

## 🔴 6. REST API 설계 기본 규칙
### **1. URI는 정보의 자원을 표현해야 한다.**
```HTTP
GET /members/delete/1
```
위와 같은 방식은 REST를 제대로 적용하지 않은 URI이다.   
URI는 자원을 표현하는데 중점을 두어야 한다.   
**`delete`와 같은 행위에 대한 표현이 들어가서는 안된다!**

### **2. 자원에 대한 행위는 HTTP Method로 표현한다.**
위의 잘못된 예시를 수정해보면
```HTTP
DELETE /members/1
```
다음과 같이 수정할 수 있다.
- 회원 정보를 가져오는 URI
  ```HTTP
  GET /members/show/1 (X)
  GET /members/1      (O)
  ```
- 회원을 추가할 때
  ```HTTP
  GET /members/insert/2 (X)
  POST /members/2       (O)
  ```

## 🔴 7. URI 설계 시 주의할 점
1. 슬래시 구분자(/)는 계층 관계를 나타내는데 사용
   ```HTTP
   http://restapi.example.com/houses/apartments
   http://restapi.example.com/animals/mammals/whales
   ```

2. URI 마지막 문자로 슬래시(/)를 포한하지 않는다.   
   URI에 포함되는 모든 글자는 `리소스의 유일한 식별자로 사용`되어야 하며   
   `URI가 다르다는 것은 리소스가 다르다는 것`이고, 역으로 리소스가 다르면 URI도 달라져야 한다.
   REST API는 분명한 URI를 만들어 통신을 해야하기 때문에 혼동을 주지 한도록 경로 마지막에는 슬래시(/)를 사용하지 않는다.   
   ```HTTP
   http://restapi.example.com/houses/apartments/ (X)
   http://restapi.example.com/houses/apartments  (O)
   ```

3. 하이픈(-)은 URI 가독성을 높이는데 사용  
   URI를 쉽게 읽고 해석하기 위해, 불가피하게 긴 URI경로를 사용하게 된다면 하이픈(-)을 사용해 가독성을 높인다.   

4. 밑줄(_)은 URI에 사용하지 않는다.   
   밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도하여 지양한다. (가독성을 위해)

5. URI 경로에는 소문자가 적합하다.   
   대소문자에 따라 다른 리소스로 인식하게 되기 때문에 URI 경로에 대문자 사용은 피하도록 한다.   
   `RFC 3986(URI 문법 형식)`은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문
   ```
   RFC 3986 is the URI (Unified Resource Identifier) Syntax document
   ```

6. 파일 확장자는 URI에 포함시키지 않는다.   
   ```
   http://restapi.example.com/members/soccer/345/photo.jpg (X)
   ```
   REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않습니다.   
   Accept header를 사용하도록 합시다.
   ```
   GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg
   ```

7. 리소스 간에는 연관 관계가 있는 경우
   - / 리소스명 / 리소스 ID / 관계가 있는 다른 리소스명
   - ex)
   ```HTTP
   GET /users/{userid}/devices          (일반적으로 소유 'has'의 관계를 표현할 때)
   GET : /users/{userid}/likes/devices  (관계명이 애매하거나 구체적 표현이 필요할 때)
   ```
## 🔴 8. 자원을 표시하는 Collection과 Document
Collection과 Document에 대해 알면 URI 설계가 한 층 더 쉬워진다.   
- Document: 단순히 문서로 이해해도되고, 한 `객체`라고 이해하여도 괜찮다.   
  객체 인스턴스나 데이터베이스 레코드와 유사한 개념

- Collection: 문서들의 집합, `객체들의 집합`이라고 생각하면 이해하기 쉽다.   
  서버에서 관리하는 Directory(디렉터리)라는 리소스

- Store: 클라이언트에서 관리하는 리소스 저장소   
Document & Collection 모두 리소스를 표현할 수 있으며 URI에 표현된다.

```HTTP
http:// restapi.example.com/sports/soccer
```
위 URI는 `sports라는 컬렉션`과 `soccer라는 도큐먼트`로 표현되고 있다고 생각하면 된다.
```HTTP
http:// restapi.example.com/sports/soccer/players/13
```
`sports, players 컬렉션`과 `soccer, 13(13번인 선수)를 의미하는 도큐먼트`로 URI가 이루어져있다.
여기서 중요한 점은 **`컬렉션은 복수`**로 사용되고 있다는 점이다.   
좀 더 직관적인 REST API를 위해서는 컬렉션과 도큐먼트를 사용할 때 단수 복수도 지켜준다면 좀 더 이해하기 쉬운 URI를 설계할 수 있다.

## 🔴 9. REST API 설계 예시
|CRUD|HTTP verbs|Route| 
|:-----|:---|:---|
|resource들의 목록을 표시|GET|/resource|
|resource 하나의 내용을 표시|GET|/resource/:id|
|resource를 생성|POST|/resource|
|resource를 수정|PUT|/resource/:id|
|resource를 삭제|DELETE|/resource/:id|

### [참고] HTTP 응답 상태 코드

- 1xx: 전송 프로토콜 수준의 정보 교환
- 2xx: 클라이언트 요청이 성공적으로 수행됨
- 3xx: 클라이언트는 요청을 완료하기 위해 추가적인 행동을 취해야 함
- 4xx: 클라이언트의 잘못된 요청
- 5xx: 서버쪽 오류로 인한 상태코드
---
## ⭐️ RESTful이란?
- RESTful은 일반적으로 REST라는 아키텍쳐를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다.   
  - `REST API`를 제공하는 웹 서비스를 `REST ful하다고 할 수 있다.
- RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다.
  - 즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.

### 👉🏻 RESTful의 목적
- 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
- RESTful한 API를 구현하는 근본적인 목적이 성능 향상에 있는 것이 아니라   
  일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주 동기이니,   
  성능이 중요한 상황에서는 굳이 RESTful한 API를 구현할 필요는 없다.

### RESTful 하지 못한 경우
- Ex1) CRUD 기능을 모두 POST로만 처리하는 API
- Ex2) route에 resource, id 외의 정보가 들어가는 경우(/students/updateName)

---
### 🌐 Reference Site
[REST API 제대로 알고 사용하기](https://meetup.toast.com/posts/92)   
[[Network] REST란? REST API란? RESTful이란?](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)   
[iOS) HTTP / HTTPS / RESTful 이 도대체 뭘까](https://babbab2.tistory.com/70?category=831129)   
[RESTful API란 무엇입니까? - AWS](https://aws.amazon.com/ko/what-is/restful-api/)   