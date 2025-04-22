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


* 왜 쓰는걸까?
```
작업하다가 코드를 이전 버전으로 되돌리고 싶을 때 모든 작업 내용에 백업본을 모두 저장할 수 없으므로 편리함.
```

* 왜 메일 안씀?
```
메일은 다른 업무도 많이 봐서 하나하나 찾기 힘듦. 누군가는 메일 999개씩 쌓아둬서 업데이트도 늦어짐.
```

* 코드 안쓰는 사람들은 Notion 같은거 쓰면 되는거 아님?
```
Git으로 똑같은 작업 할 수 있음. 돈 2배로 내야함. 연구원에서 언제 막을지 모름.
```

* 그냥 알아서 정리하면 안됌?
```
자신 있으면 해도 됌. 근데 박사님이 그렇게 하지 말라고 할 가능성 99%
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

* git add

![git_add](/003_code/code_review/250423_khy/images/git_add.png)

위 그림에서 + 버튼 누르면 staging area로 이동된다.

* git commit -m

staging area의 파일들을 git commit 을 통해 메세지를 남기면서 local repository에 저장한다.

![git_commit](/003_code/code_review/250423_khy/images/)


### Branch는 왜 써야하는가?

우선 git에서 branch가 어떤 것인지 정확히 알 필요가 있다.

![branch](/003_code/code_review/250423_khy/images/what_is_branch.png)

branch라고 하는 것은 현재 프로젝트의 복사본을 만드는 것이고, 정확히 말하자면 **HEAD상태에서 commit의 복사본** 을 만드는 것이다.

일반적으로 main이라는 큰 줄기가 생성된 상태가 초기 상태가 되고, 여기서 작업을 진행할 수도 있지만 여러 사람과 함께 일하거나, 특정 기능을 추가하는 작업을 하고 싶을 경우 branch를 갈라서 사용하는게 일반적이다.

왜?

```
1) 여러 사람 할 때 최종본으로 사용될 main(배포용)에 뭔 짓했다가 버그 나면 안되니까

2) 혼자 하더라도 내가 어떤 작업을 했는지 commit message에 구구절절 적는 사람은 없다. (오히려 한 번에 전부 커밋하고 update라고 적어두는데 뭐가 뭔지 알 방법이 더더욱 없음.)

3) 이후에 여러 코드가 한 번에 작동하는 연구 또는 웹페이지를 제작할 때 겁쟁이 같아도 퇴로를 만들어 놓는게 좋다..
```

위의 이유로 특정 작업을 할 경우 branch를 갈라서 하는 것을 추천함. 

아래는 참고용 자료. 그럼 어떻게 branch를 관리 할 수 있나? 라는 내용임.

* gitflow (전문가 / 큰 프로젝트 수준)

  흔히 개발자들이 사용하는 방법. 굉장히 복잡하고 체계적이지만 사고날 위험이 적다.

  ![gitflow](/003_code/code_review/250423_khy/images/gitflow.png)

  branch type을 5가지로 나눠서 관리함.

  예를 들어 자판기를 만든다고 가정해서 어떤 역할인지 설명하면

  1. main
    * 상용화 된 자판기
  2. develop
    * 새로운 메뉴를 추가하고 싶음. 
  3. feature
    * 새로운 메뉴를 뽑을 수 있는 버튼 feature, 새로운 메뉴를 자판기 아래로 내려주는 feature 등등...
  4. release
    * 회사 내부에서 자판기 테스트할 수 있는 단계. 상남자식 코드는 필요없음.
  5. hotfix
    * 자판기가 음료를 안뱉고 동전을 마구 뱉음. -> 당장 고쳐야함.

* Trunk-based development(개별 연구 수준)
  
  연구실에서 실제 사용되는 방법. 우리 팀은 실제로 협업이 적기 때문에 develop branch 같은거 사실 필요없음. branch하나만 잘 관리해도 되면 다음과 같은 형태로 사용할 수 있음.

  ![trunk_based](/003_code/code_review/250423_khy/images/trunk_based.jpg)

  이렇게 하면 본인 연구에서 기능 단위로 branch를 관리하면 나중에 어떤 기능을 추가했을 때 어떤 코드 및 데이터가 사용되었는지 관리하기 편해짐.

* 그렇다면 우리팀은..?

![sbteam_git](/003_code/code_review/250423_khy/images/sbteam_git.PNG)

sbteam 레포지토리가 가장 활발하게 사용되고 있어 예시로 가져옴. trunk_based development로 사용되고 있고, 박사님이 merge하면서 적절히 관리되고 있음. 그러나 최근 main에 바로 작업하는게 눈에 띄고 있음. 


### 앗! 내 데이터가..!

어쩌다가 없어지는 경우가 종종 있는데, commit이나 stash를 자주 했다면 너무 걱정안해도 된다.

--> commit을 하면 데이터가 저장되나?

|Git 객체| 설명 | 저장 위치|
|-------|--------|-----------------|
|Blob | 파일 내용 | .git/objects/|
|Tree |폴더/파일 구조 | .git/objects/|
|commit|meta data | .git/objects/|

위와 같은 경로에 내용들이 SHA 해시 기반의 이름을 가지고 객체들이 저장된다. 

```
Blob은 Binary Large Object로 파일의 내용만을 압축된 binary 타입으로 저장하는 방법이고, 해시라는 건 파일 이름을 컴퓨터가 찾기 편하게 key값을 만든거라고 이해하면 쉽다.
```

실제 데이터가 위의 형태로 commit 또는 stash를 하면 저장되니 ```git reflog``` 또는 ```git log```를 사용하면 이전 HEAD로 돌아가서 작업 내용을 일부 복구 가능하다.

```
권장 commit 횟수 : 작은 기능 단위의 변화가 있을 시 commit할 것. 자주하면 좋으나 stash 기능을 사용해서 중간중간 백업하기.
```

### 자주 겪는 error 상황들..

* 100 MB 이상 업로드

초보들이 자주 겪는 데이터 크기 문제가 있음. 다들 한 번씩은 겪는 문제라고 생각된다.

![101MB_commit](/003_code/code_review/250423_khy/images/git_101MB.PNG)

위 그림으로 설명이 다 되는데, git은 단일 파일에 대해서 100 MB 이상을 업로드 할 수 없어서 다들 파리채 블로킹을 한 번 씩은 당해본 경험이 있을 것 같음.

※ 참고로 github에서 권장하는 repository 사이즈는 1~5 GB 로 관리해서 내려받고 업로드하는데 무리가 없도록 관리를 하라고 한다.

실제로 100 MB 가 넘는 raw data는 어떻게 공유할까?

우선 해당 파일이 계속 commit 되게 할 수는 없으니 프로젝트 파일안에 .gitignore 이라는 파일을 만들고 해당 파일의 경로까지 정확히 입력하여 업로드 되는 것을 막아줘야함.

![gitignore](/003_code/code_review/250423_khy/images/gitignore.PNG)

그럼 위의 그림과 같이 Large_file_example의 경우 git add를 할 수 없는 상태가 되어서 gitignore만 잘 관리해줘도 커다란 파일이 실수로 commit 되는 불상사를 원천차단 가능함.

그런데 만약 이 파일이 꼭 필요해서 올려야만 프로젝트 내의 기능을 사용할 수 있다면 어떻게 공유할까?

실험실에서는 4가지 방법이 있음.

1. share folder 활용
     * 가장 직관적인 방법. 153 서버 share folder를 사용해서 파일을 연구원 내에서 공유. 1GB 미만 정도에서 적합할 듯함.

2. 서버 내의 script 파일과 DB 파일을 사용하기
    * linux 사용에 익숙하지 않으면 불편할 수 있음.
    * 서버 사용량 많아짐.

3. vessl AI 를 통해 공유
    *  RUN script를 복제하는 것으로 같은 환경을 구축 가능.

4. 외부 링크를 통해 다운로드(wget, curl)
    * 기존 DB를 받기에 편함.

* Merge를 하라고?

git branch를 main에 merge 시키려다가 특정 파일을 merge 시키는 도중 conflict 에러를 종종 겪게 된다.

