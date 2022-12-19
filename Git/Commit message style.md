# Commit message style guide

## Karma Style
Karma Style(카르마 스타일)은 Git을 작성할 때 제공하는 convention(규칙)이다.   
카르마에서 convention을 제공하는 2가지 이유로는   
- 자동으로 changeLog를 생성하기 위함
- git history를 간단하게 탐색하기 위해

## Commit message Style
```
<type> (<scope>): <subject>

<body>

<footer>
```
```
// 형식에 맞춘 예시
fix(middleware): subject의 내용

Add one new data, ~~~

Closes #123
```

### 🔴 type의 종류
- `Feat`: 주로 사용자에게 새로운 기능이 추가되는 경우
- `Fix`: 사용자가 사용하는 부분에서 bug가 수정되는 경우
- `Docs`: 문서에 변경 사항이 있는 경우
- `Style`: 세미클론을 까먹어서 추가하는 것 같이 형식적인 부분을 다루는 경우   
  (코드의 변화를 주는 경우가 아닌)
- `Refactor`: 기존 코드를 변경하여 생산적인 코드로 수정하는 경우
  (변수의 네이밍을 수정하는 경우)
- `Test`: 테스트 코드를 수정 또는 추가하는 경우
- `Chore`: 크게 중요하지 않은 일을 수정하는 경우

type은 실제 케바케라서 다를 수 있으며, type을 선택하여 commit message를 작성하는 것.

### 🟡 scope의 종류
- init
- runner
- watcher
- config
- web-server
- proxy
- etc

scope의 경우 생략이 가능, 주로 카르마 도구 내에서 자주 사용하므로 일단 생략한다고 보면 된다.

### 🟢 body 작성
body(본문)을 작성할 때 명령형 어조를 사용하며, 현재 시제를 사용하는 것은 권장한다.   


### 🟡 footer 작성
예를 들면 git의 issue의 기능 단위로 구별하였다면 footer에 closes를 사용하여 issue를 닫을 수 있다.
```
Closes #123, 124, 125
```

## Commit message 7가지 약속
아래의 7가지 약속은 commit message를 영어로 작성할 때 최적화되어있다.   
1. subject와 body 사이는 한 줄 띄워 구분한다.   
   -> git log를 보면 body가 subject와 같이 보여 불편함이 있다!
2. subject line의 글자수는 50자 이내로 제한
3. subject line의 첫 글자는 대문자 사용 (type이 아님)   
   -> 영문으로 작성 시 해당되며 한국어 사용 시 적용 ❌
4. subject line의 마지막에 마침표 사용 ❌
5. subject line에 명령형 어조 사용
6. body는 72자마다 줄 바꾸기
7. ⭐️ body는 `어떻게`보다 `무엇을`, `왜` 라는 키워드에 맞춰서 작성하기

## 🤔 Commit의 단위??
commit의 단위 역시도 팀, 회사마다 다르다.   
각자 다르겠지만 최대한 한 가지 기능을 하는 것에 대해서 commit을 하려고 노력해본다.   
즉, **`함수 단위 혹은 기능 단위로 commit을 하려고 한다.`**

### 🌐 Reference Site
[Karma git commit message](http://karma-runner.github.io/latest/dev/git-commit-msg.html)   
[Udacity Git Commit Message Style Guide](https://udacity.github.io/git-styleguide/)   
[Chris Beams - How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)   
[Uno'Blog - 좋은 Git 커밋 메세지를 작성하기 위한 8가지 약속](https://djkeh.github.io/articles/How-to-write-a-git-commit-message-kor/)   