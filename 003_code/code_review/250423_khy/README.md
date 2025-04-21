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
왜 쓰는걸까? -> 작업하다가 코드를 이전 버전으로 되돌리고 싶을 때 모든 작업 내용에 백업본을 모두 저장할 수 없으므로 편리함.

왜 메일 안씀? --> 메일은 다른 업무도 많이 봐서 하나하나 찾기 힘듦. 누군가는 메일 999개씩 쌓아둬서 업데이트도 늦어짐.

코드 안쓰는 사람들은 Notion 같은거 쓰면 되는거 아님? --> Git으로 똑같은 작업 할 수 있음. 돈 2배로 내야함. 연구원에서 언제 막을지 모름.

그냥 알아서 정리하면 안됌? --> 자신 있으면 해도 됌. 근데 박사님이 그렇게 하지 말라고 할 가능성 99%
```

아무튼 써주면 다른 사람이 뭐하는지도 볼 수 있으니 써주면 좋겠다. (어디가서 git 잘쓴다고 하면 좋아할지도)

### How to use Git?

![history](/003_code/code_review/250423_khy/images/git_명령어_원리.png)

git 이라는 프로그램이 local area의 파일과 remote are의 파일을 계속 확인하면서 위와 같은 과정으로 remote에 있는 저장소와 내 local 저장소를 연동할 수 있음. 변경점이 생길 때 사용자가 이를 git에게 commit을 통해 알려주고, git은 이를 저장하는 역할을 함.

왜 staging area가 나눠져있을까? --> commit을 통해  나처럼 commit 자주 안하는 사람이 기능 단위로 commit을 해야할 때 필요.   
```
ex) file_1과 file_2 를 각각 다른 목적으로 수정한 뒤 commit을 할 경우.

git add file_1 -> git commit -m "1번작업" 
git_add file_2 -> git commit -m "2번작업" 
```

단, commit만 많아지는게 불편하면 그냥 한 번에 commit하고 message를 통합하면 됨.


사용자들이 익숙해져야하는 명령어는 다음과 같다.

```
git clone [repository 주소] 
git pull # remote의 내용을 내려받음 / vscode 기능 대체
git add [파일명] # vscode 기능 대체
git commit ["message"] # vscode 기능 대체
git push # vscode 기능 대체
git status # 현재 staging 및 수정된 file 내역 확인

# branch 및 history 참조 + reset
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

원래 git 명령어를 사용하던 걸 vscode가 UI를 통해 일부 기능을 대체해 주고 있음. User guide를 작성하고자 본 문서를 작성함.

project 받기

```
git clone git@github.com:Corgi-welsh/How_to_git.git
```

sbteam file 에 복사본 넣을 예정이라 안받아도 됌.

git과 vscode를 잘 설치한 뒤 vscode를 실행하면 다음과 같은 화면이 나옴.

![vscode_화면](/003_code/code_review/250423_khy/images/vscode_init.PNG)

이 화면에서 왼쪽의 빨간 박스 안의 아이콘을 누르면 프로젝트를 선택할 수 있음. 아무 git 프로젝트나 열어보자.

여기서 다음 그림의 빨간 박스 안의 아이콘을 눌렀을 때 처음 시작한 사람의 경우 다음과 같은 화면이 나옴.

![git_init](/003_code/code_review/250423_khy/images/git_init.jpeg)

git initialize가 되고 다음과 같은 화면으로 전환된다.

![vs_git](/003_code/code_review/250423_khy/images/vs_git.PNG)

여기 이후로는 실습.

간단한 기능

```
1. git pull
2. git add
3. git commit
4. git push
```

### 앗! 내 데이터가..!

어쩌다가 없어지는 경우가 종종 있는데, commit이나 stash를 자주 했다면 너무 걱정안해도 된다.

--> commit을 하면 데이터가 저장되나?

|Git 객체| 설명 | 저장 위치|
|-------|--------|-----------------|
|Blob | 파일 내용 | .git/objects/|
|Tree |폴더/파일 구조 | .git/objects/|
|commit|meta data | .git/objects/|

위와 같은 경로에 내용들이 SHA 해시 기반의 이름을 가지고 객체들이 저장된다. Blob은 Binary Large Object로 파일의 내용만을 압축된 binary 타입으로 저장하는 방법이고, 해시라는 건 파일 이름을 컴퓨터가 찾기 편하게 key값을 만든거라고 이해하면 쉽다.

실제 데이터가 위의 형태로 commit 또는 stash를 하면 저장되니 ```git reflog``` 또는 ```git log```를 사용하면 이전 HEAD로 돌아가서 작업 내용을 일부 복구 가능하다.

```
권장 commit 횟수 : 작은 기능 단위의 변화가 있을 시 commit할 것. 자주하면 좋으나 stash 기능을 사용해서 중간중간 백업하기.
```

### 자주 겪는 error 상황들..

초보들이 자주 겪는 데이터 크기 문제가 있음. 다들 한 번씩은 겪는 문제라고 생각된다.

![101MB_commit](/003_code/code_review/250423_khy/images/git_101MB.PNG)

위 그림으로 설명이 다 되는데, git은 단일 파일에 대해서 100 MB 이상을 업로드 할 수 없어서 다들 파리채 블로킹을 한 번 씩은 당해본 경험이 있을 것 같음.

※ 참고로 github에서 권장하는 repository 사이즈는 1~5 GB 로 관리해서 내려받고 업로드하는데 무리가 없도록 관리를 하라고 한다.

실제로 100 MB 가 넘는 raw data는 어떻게 공유할까?

우선 해당 파일이 계속 commit 되게 할 수는 없으니 프로젝트 파일안에 .gitignore 이라는 파일을 만들고 해당 파일의 경로까지 정확히 입력하여 업로드 되는 것을 막아줘야함.

![gitignore](/003_code/code_review/250423_khy/images/gitignore.PNG)

그럼 위의 그림과 같이 Large_file_example의 경우 git add를 할 수 없는 상태가 되어서 gitignore만 잘 관리해줘도 커다란 파일이 실수로 commit 되는 불상사를 원천차단 가능함.

그런데 만약 이 파일이 꼭 필요해서 올려야만 프로젝트 내의 기능을 사용할 수 있다면 어떻게 공유할까?

실험실에서는 가지 방법이 있음.

1. share folder 활용
     * 가장 원시적인 방법으로 내 