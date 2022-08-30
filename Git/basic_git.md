Git
===

### 1. 용어
- GIT
    - 버전관리 시스템(형상관리)   
    - Configuratin Management System    
    - Version Control Systems   

- Repository
    - 소스코드가 저장되어 있는 여러 개의 Branch들이 모여있는 디스크상의 물리적인 공간   
    - Local Repository와 Remote Repository로 구분   

- Branch
    - 특정 시점(commit 단위)에서 분기하여 새로운 commit을 쌓을수 있는 가지를 만드는 것   
    - 개발의 주축이 되는 branch를 master branch(main branch)라고 함   
    - 모든 branch는 최종적으로 다시 master branch에 merge되는 방식으로 진행됨

___
### 1.1 Git 설치
#### 1.1.1 CLI (Command Line Interface)
- GitBash를 포함하여 Git을 설치한다. ([http://git-scm.com/](http://git-scm.com/))   

    (1) Git의 버전을 확인한다.
    ```
    git --version
    ```

    (2) 협업시 윈도우와 맥에서 엔터 방식 차이로 인한 오류를 방지한다.
    ```
    git config --global core.autocrlf true 
    ```


#### 1.1.2 GUI (Graphical User Interface)
- SourceTree를 설치한다. ([https://www.sourcetreeapp.com/](https://www.sourcetreeapp.com/))


#### 1.1.3 Integrated Development Environmen
- Visual Studion Code를 설치한다. ([https://code.visualstudio.com/](https://code.visualstudio.com/))
- 기본 터미널을 Git Bash로 설정한다.

___

### 1.2 Git 최초 설정
- 터미널 프로그램(Git Bash)에서 아래 명령어를 실행한다
```
git config --global user.name "(본인 이름)"
git config --global user.email "(본인 이메일)"
```

- 확인은 다음의 명령어로 진행한다.
```
# 하나씩 확인하고 싶을 경우
git config --global user.name
git config --global user.email

# 전체를 한번에 확인하는 방법 (종료시 q 사용)
git config --list
```
- 서버에서 가져올때는 LF를 CRLF로 변경하고 보낼때는 CRLF를 LF로 변경한다.(Windows)
```
git config --global core.autocrlf true
```

- 기본 브랜치명을 변경한다.
```
git config --global init.defaultBranch main
```
___

### 1.3 문법
#### 1.3.1 Git의 Workflow
- Working directory(작업공간) : 실제 소스파일, 생성한 파일들이 존재     
- Index(stage) : staging area, 작업할 내용이 올라가는 임시저장 영역, `git add`한 파일들이 존재 
    - (1) untracked   
    - (2) tracked : unmodified, modified   
- Head - git directiory, 최종확정본, git commit한 파일들이 존재
- Remote


#### 1.3.2 Git 문법
- Repository(히스토리를 저장할 .git 폴더) 생성 : `git init`   
- 배제할 요소 지정 : `git ignore`   
- 폴더 내부요소 전체 보기 : 'ls -all'
- Workflow의 현재상황 확인하기 : `git status`   
- working directory → Index : `git add .`
- working directory → head : `git commit -am "(메시지)"`
- Index → head : `git commit -m "(메시지)`
- Index → working directory : `git rm --cached .`
- head 히스토리 확인 : `git log`

#### 1.3.3 Git Editor
- Vim 문법

|Vim 명령어|작업|
|:--:|:--:|
|i|텍스트 입력 시작|   
|ESC|텍스트 입력 종료|   
|:q|저장없이 종료|   
|:q!|저장없이 강제종료|   
|:wq|저장하고 종료|   
|k|위로 스크롤| 
|j|아래로 스크롤|

___

### 1.4 시간
> Checkout : 특정 시간이나 차원으로 이동한다 (Branch, Commit, Tag)  
- 시간 : 프로젝트의 버전을 과거로 되돌리거나 특정내역을 취소할 수 있다

#### 1.4.1 reset
- 원하는 시점으로 돌아간 뒤 이후 내역을 지운다.
  ```
  git log
  ```
  위의 명령어로 커밋된 내역을 확인한다.
  되돌아 갈 시점의 커밋의 해시를 복사한다.
  `:q`로 빠져나간다.   
     
  ```
  git reset --hard (돌아갈 커밋의 해시) 
  ```
  위의 명령어를 입력하면 해당 커밋으로 돌아가며
  이후에 있는 내역이 모두 삭제되게 된다.
     
  ```
  git reset --hard
  ```
  백업해둔 .git 폴더가 있다면 폴더를 복원한 후
  위의 명령어로 마지막 커밋으로 이동을 한다

#### 1.4.2 revert
- 되돌리기 원하는 시점의 커밋을 거꾸로 시작한다.
  ```
  git revert --no-commit (되돌릴 커밋의 해시)
  ```
___

### 1.5 차원
> Checkout : 특정 시간이나 차원으로 이동한다 (Branch, Commit, Tag)  
- 차원 : 프로젝트의 여러 모드를 쉽게 전환하고 관리할 수 있다   

#### 1.5.1 브랜치 생성/이동/삭제
- 브랜치 생성 : `git branch (브랜치명)`   
- 브랜치 목록 조회(Local Branch) : `git branch`   
- 브랜치 목록 조회(Remote Branch) : `git branch -r`   
- 브랜치 목록 조회(All Branch) : `git branch -a`   
- 브랜치 목록 상세조회 : `git log --all --decorate --oneline --graph`   
- 브랜치 이동 : `git switch (브랜치명)` or `git checkout (브랜치명)`   
- 브랜치 생성, 이동 동시에 : `git switch -c (브랜치명)` or `git chekout -b (브랜치명)`   
- 브랜치 삭제 (Local Branch) : `git branch -d (브랜치명)`   
- 브랜치 삭제 (Remote Branch) : `git push origin --delete (브랜치명)`   
- 브랜치 강제삭제 : `git branch -D (브랜치명)`   
- 브랜치 이름 변경 : `git branch -m (기존이름)(새이름)`   
   
#### 1.5.2 브랜치 병합 `merge`
- 두 브랜치를 한 커밋에 이어붙인다   
- 브랜치의 사용내역이 남는다   
  
    - Git Configuration 파일 열기
    ```
    # 설정한 Git Editor로 실행됨
    git config --global -e
    ```

    - Git Merge 설정 추가
    ```
    [merge]
        tool = vscode
    [mergetool "vscode"]
        cmd = "code --wait --MERGED"
    ```
    - Git Merge
    ```
    # 브랜치 B를 브랜치 A로 merge 할 때, 우선 A브랜치로 이동을 한 후 아래의 코드를 입력한다
    git merge B
    ```
    `:wq`로 자동입력된 커밋 메시지를 저장한 뒤 마무리하고, 병합된 브랜치는 삭제한다.
    - Merge Tool 실행
    ```
    # Conflict 발생 시
    git mergetool
    ```
    - Conflict 해제
    ```
    #1
    git add 

    #2
    git commit
    ```


#### 1.5.3 브랜치 병합 `rebase`
- 브랜치를 다른 브랜치에 이어 붙인다
- 한줄로 커밋이 깔끔하게 정리된다   
  `C` 브랜치를 `A` 브랜치로 merge 할 때,   
  우선 C브랜치로 이동을 한 후 아래의 코드를 입력한다.   
  ```
  git rebase A
  ```
  이때 A브랜치가 C브랜치보다 뒤에 위치해 있는데   
  이를 해결하기 위해 A브랜치로 이동을 한 후 아래의 코드를 입력한다.
  ```
  git merge C
  ```
  그리고 브랜치 c는 삭제한다.

___

## 2. GitHub
### 2.1 토큰 생성 및 관리
  1. Personal access token을 만든다
  2. 토큰을 컴퓨터에 저장한다(Windows 자격 증명 관리자 > Windows 자격 증명 > `git:https://github.com` )
  3. 소스트리에도 토큰을 저장한다. (설정 > 계정 > 추가 > basic > HTTPS)
  

### 2.2 `push`
> Local Repository의 내용 중, Remote Repository에 반영되지 않은 commit을 Remote Repository로 보내는 과정      
> Push를 하는 순간 다른 개발자들도 영향을 받음    
- 처음부터 모든 내용을 `push` 해야하는 경우 로컬 저장소에 원격 저장소 연결 추가    
```
# 매번 아이디와 비밀번호 따로 입력해야 함
git remote add origin http://github.com/<repository>.git(원격 저장소 주소)

# 유저네임과 토큰을 활용하여 아이디 비밀번호 입력을 생략할 수 있음
git remote add origin http://<username>:<token>@github.com/<repository>.git
```
- 기본 브랜치 명을 main으로 설정    
```
git branch -M main   
```
- 로컬 저장소의 커밋 내역들을 원격으로 push    
```
git push origin <branchname>
```
- 원격 목록 보기    
```
git remote
```
- 원격 지우기   
```
git remote remove (origin 등 원격 이름)
```
- 변경 내역을 `push` 해야하는 경우   
```
git push
```

### 2.3 `pull`
> Remote Repository에 있는 내용 중, Local Repositry에 반영되지 않은 내용을 가져와서 Local Repository에 저장하는 과정    
> Push과정에서 Conflict가 발생하여 Push가 거절된 경우에는, Pull을 통해 문제를 해결한 뒤 다시 Push를 시도해야 함   
- 파일만 다운로드 `Download ZIP`   
- Git 관리내역 포함 다운로드 `Git clone`   
  ```
  # 터미널 or Git Bash에서 대상 폴더 이동 후 Git Init으로 해당 폴더를 초기화   
  # Remote Repository 등록
  # git clone으로 Remote Repository의 내용을 Pull
  git clone http://github.com/<repository>.git (원격 저장소 주소)
  git clone http://<username>L<token>@github.com/<repository>.git
  ```
- 변경된 내역을 `pull`해야하는 경우   
  ```
  git pull origin <branchname>
  ```

### 2.4 `push`할 것이 있을 때 `pull`하는 방법   
- merge 방식    
```
git pull --no-rebase
```

- rebase 방식 
```
git pull --rebase
```
___

## 3. 기타
### 3.1 Git Diff Tool 설정
- Git Editor 변경
```
# git config --global core.editor <editorname> --wait
# --wait 옵션 : VSCode 실행시 인스턴스를 닫을 때까지 command 대기

git config --global core.editor "vim"
git config --global core.editor "code --wait"
```
- Git Configuration 파일 열기
```
# 설정한 Git Editor로 실행됨
git config --global -e
```
- Git Diff 설정 추가
```
[diff]
    tool = vscode
[difftool "vscode"]
    cmd = "code --wait --diff $LOCAL $REMOTE"
```
- Local Branch간 비교
```
git diff <branch1> <branch2>
```
- Commit간 비교
```
# git log로 해시 확인 가능
git diff <commithash1> <commithash2>
```
- 마지막 Commit과 이전 Commit 비교
```
git diff HEAD HEAD^
```
- 마지막 Commit과 현재 수정사항 확인
```
git diff HEAD
```
- Local과 Remote 비교
```
git diff <branch> origin/<branch2>
```

___
### 3.2 Tag
> 임의의 commit 위치에 쉽게 찾아갈 수 있도록 붙여놓은 이정표   
> Tag가 붙은 commit은 commit id(version) 대신 tag name으로 쉽게 checkout 가능   

#### 3.2.1 Local
- 현재 버전에 Tag 달기
```
git tag <tagname>
```
- 특정 버전에 Tag 달기
```
git tag <tagname> <commithash>
```
- Tag를 Remote Repository에 Push
```
git push origin <tagname>
```
- Tag 확인
```
# 전체 정보
git log

# 태그 목록
git tag

# 태그 상세 정보
git show <tagname>
```
- Git tag 삭제
```
git tag --delete <tagname>
```


## ○ 레퍼런스
* [[얄팍한 코딩사전] 제대로 파는 깃강좌](https://www.youtube.com/watch?v=1I3hMwQU6GU&t=726s)
* [[드림코딩] 깃의 중요한 컨셉 이해하기](https://academy.dream-coding.com/courses/git)
