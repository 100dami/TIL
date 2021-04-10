## GIT 

### 명령어
#### git add 취소
> git reset HEAD <file>

#### git commit 취소
> git reset --soft HEAD

#### git commit message 변경
> git commit --amend

#### git push 취소?
> git reset HEAD
// 가장 최근의 commit을 취소

### COMMIT 규칙
* 부정문 Don't를 사용합니다.
* 어떻게 보다는 무엇과 왜를 설명한다.      


### 좋은 커밋 메시지를 위한 영어 단어
``` FIX ``` : 보통 올바르지 않은 동작을 고친 경우에 사용 <br>
``` ADD ```  : 코드나 테스트, 예제, 문서 등의 추가가 있을 때 사용 <br>
``` REMOVE ```, ``` Clean ```, ``` Eliminate ``` : 코드의 삭제가 있을 때 사용 <br> 
보통 앞에 ‘unnecessary’, ‘useless’, ‘unneeded’, ‘unused’, ‘duplicated’가 붙는 경우가 많음\
``` USE ``` : 특별히 무언가를 사용해 구현을 할 때 사용 <br>
``` REFACTOR ```, ``` SIMPLYFY ``` : 복잡한 코드를 단순화 할 때 사용 <br> 
``` UPDATE ``` : 개정이나 버전 업데이트가 있을 때 사용 <br> 
Fix와는 달리 Update는 잘못된 것을 바로잡는 것이 아니라는 점에 주의해야 함
