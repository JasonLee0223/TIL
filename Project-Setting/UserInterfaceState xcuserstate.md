# UserInterfaceState.xcuserstate 제거하기

.gitignore를 생성하면 항상 무언가 수정 또는 작성사항이 없음에도 불구하고 계속해서 파일의 상태를 저장하는   
UserInterfaceState.xcuserstate 파일을 확인할 수 있었다.   
이 파일 때문에 불필요한 커밋을 계속해서 남기게 되어 해당 파일을 제거하는 방법을 찾아보게되었다.

```zsh
git rm --cached [Project Name].xcworkspace/xcuserdata/[User Name].xcuserdatad/UserInterfaceState.xcuserstate
```
- Project Name: 해당 프로젝트 명
- User Name: 본인 이름

```zsh
git commit -m 'Removed file that shouldnt be tracked'
```
이렇게 commit 이후로는 더 이상 해당 파일이 추적되지 않는다.

만약 계속 gist에서 추적한다면 그냥 gitignore에 추가하도록하자
```
* .xcuserstate
```