Date : 20250423   
Author : hy3074

### Why Use Git?

![version](/003_code/code_review/250423_khy/images/git_버전관리.png)

* 코드 버전 관리
  * 과거 버전으로 되돌리기 가능.
  * 작업별 태그를 달아둬서 어떤 기능인지 알기 편함.

* Project 별 작업 내용 관리
  * branch라는 기능을 통해 기능 단위의 업데이트가 가능함.
  * 여러 사람이 모여 작업할 때 모든 사람이 각각의 작업 내용이 있는데 이를 branch라는 기능을 쓰면 관리하기 편해짐.

```  
우리는 왜 쓰는걸까? -> 작업하다가 코드를 이전 버전으로 되돌리고 싶을 때 모든 작업 내용에 백업본을 모두 저장할 수 없으므로 편리함.

왜 메일 안씀? --> 메일은 다른 업무도 많이 봐서 하나하나 찾기 힘듦.

코드 안쓰는 사람들은 Notion 같은거 쓰면 되는거 아님? --> Git으로 똑같은 작업 할 수 있음. 돈 2배로 내야함. 연구원에서 언제 막을지 모름.

그냥 알아서 공유하면 안됌? --> 자신 있으면 해도 됌. 근데 박사님이 그렇게 하지 말라고 할 가능성 100%
```

아무튼 써주면 다른 사람이 뭐하는지도 볼 수 있으니 써주면 좋겠다. (어디가서 git 잘쓴다고 하면 좋아할지도?)

### How to use Git?

![history](/003_code/code_review/250423_khy/images/git_명령어_원리.png)

위와 같은 과정으로 remote에 있는 저장소와 내 local 저장소가 연동된다.

왜 staging area

사용자들이 익숙해져야하는 명령어는 다음과 같다.

```
git clone [repository 주소] 
git pull # remote의 내용을 내려받음 / vscode 기능 대체
git add [파일명] # vscode 기능 대체
git commit ["message"] # vscode 기능 대체
git push # vscode 기능 대체
git status # 현재 staging 및 수정된 file 내역 확인

# branch 및 history 참조
git branch [branch name] # vscode 기능 대체
git stash save ["message"]
git stash pop [index]
git checkout [branch name]
git reflog
git log
git reset --hard / git reset --soft
git merge # 권장 x
```

### how to use git with vscode


### 자주 겪는 error 상황들..


 ```
 권장 commit 횟수 : 작은 기능 단위의 변화가 있을 시 commit할 것. 자주하면 좋으나 stash 기능을 사용해서 중간중간 백업하기.
 ```
