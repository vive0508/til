Git
===


# 1. Git
## 1.1 Git 설치
### 1.1.1 CLI (Command Line Interface)
- GitBash를 포함하여 Git을 설치한다. ([http://git-scm.com/](http://git-scm.com/))   

    (1) Git의 버전을 확인한다.
    ```
    git --version
    ```

    (2) 협업시 윈도우와 맥에서 엔터 방식 차이로 인한 오류를 방지한다.
    ```
    git config --global core.autocrlf true 
    ```

### 1.1.2 GUI (Graphical User Interface)
- SourceTree를 설치한다. ([https://www.sourcetreeapp.com/](https://www.sourcetreeapp.com/))


### 1.1.3 Integrated Development Environmen
- Visual Studion Code를 설치한다. ([https://code.visualstudio.com/](https://code.visualstudio.com/))
- 기본 터미널을 Git Bash로 설정한다.

___

## 1.2 Git 최초 설정
터미널 프로그램(Git Bash)에서 아래 명령어를 실행한다
```
git config --global user.name "(본인 이름)"
git config --global user.email "(본인 이메일)"
```

확인은 다음의 명령어로 진행한다.
```
git config --global user.name
git config --global user.email
```

기본 브랜치명을 변경한다.
```
git config --global init.defaultBranch main
```

## 1.2 문법
### 1.2.1 Git의 Workflow
> 1. working directory
> 2. staging area
>>  (1) untracked   
>>  (2) tracked : unmodified, modified
> 3. .git directiory
> 4. remote


### 1.2.1 Git 문법
- 히스토리를 저장할 .git 폴더 생성 `git init`
- 배제할 요소 지정 `git ignore`
- Workflow의 현재상황 확인하기 `git status`
- working directory → staging area `git add .`
- working directory → .git directory `git commit -am "(메시지)"`
- staging aread → .git directiory `git commit -m "(메시지)`
- staging aread → working directory `git rm --cached .`
- .git directiory 히스토리 확인 `git log`


### 1.2.2 Vim 문법
|Vi 명령어|작업|
|:--:|:--:|
|i|텍스트 입력 시작|   
|ESC|텍스트 입력 종료|   
|:q|저장없이 종료|   
|:q!|저장없이 강제종료|   
|:wq|저장하고 종료|   
|k|위로 스크롤| 
|j|아래로 스크롤|


## 1.3 시간
- 시간 : 프로젝트의 버전을 과거로 되돌리거나 특정내역을 취소할 수 있

### 1.3.1 reset
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

### 1.3.2 revert
- 되돌리기 원하는 시점의 커밋을 거꾸로 시작한다.
  ```
  git revert --no-commit (되돌릴 커밋의 해시)
  ```


## 1.4 차원
- 차원 : 프로젝트의 여러 모드를 쉽게 전환하고 관리할 수 있다   

### 1.4.1 브랜치 생성/이동/삭제
  브랜치 생성 `git branch (브랜치명)`   
  브랜치 목록 조회 `git branch`   
  브랜치 목록 상세조회 `git log --all --decorate --oneline --graph`   
  브랜치 이동 `git switch (브랜치명)`   
  브랜치 생성, 이동 동시에 `git switch -c (브랜치명)`   
  브랜치 삭제 `git branch -d (브랜치명)`   
  브랜치 강제삭제 `git branch -D (브랜치명)`   
  브랜치 이름 변경 `git branch -m (기존이름)(새이름)`   
   
### 1.4.2 브랜치 병합 `merge`
- 두 브랜치를 한 커밋에 이어붙인다
- 브랜치의 사용내역이 남는다   
 `B` 브랜치를 `A` 브랜치로 merge 할 때,   
  우선 A브랜치로 이동을 한 후 아래의 코드를 입력한다
  ```
  git merge B
  ```
  `:wq`로 자동입력된 커밋 메시지를 저장한 뒤 마무리한다.   
  병합된 브랜치는 삭제한다.


### 1.4.3 브랜치 병합 `rebase`
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

# 2. GitHub
## 2.1 토큰 생성 및 관리
  1. Personal access token을 만든다
  2. 토큰을 컴퓨터에 저장한다(Windows 자격 증명 관리자 > Windows 자격 증명 > `git:https://github.com` )
  3. 소스트리에도 토큰을 저장한다. (설정 > 계정 ? 추가 > basic > HTTPS)


## 2.2 `push`
- 처음부터 모든 내용을 `push` 해야하는 경우
  로컬 깃 저장소에 원격 저장소 연결 추가
  ```
  git remote add origin (원격 저장소 주소)
  ```
  기본 브랜치 명을 main으로 설정
  ```
  git branch -M main
  ```
  로컬 저장소의 커밋 내역들을 원격으로 push
  ```
  git push -u origin main 
  ```
  원격 목록 보기
  ```
  git remote
  ```
  원격 지우기
  ```
  git remote remove (origin 등 원격 이름)
  ```
- 변경 내역을 `push` 해야하는 경우
  ```
  git push
  ```

## 2.3 `pull`
- 파일만 다운로드 `Download ZIP`
- Git 관리내역 포함 다운로드 `Git clone`

  터미널 or Git Bash에서 대상 폴더 이동 후
  ```
  git clone (원격 저장소 주소)
  ```

- 변경된 내역을 `pull`해야하는 경우
  ```
  git pull
  ```

## 2.4 `push`할 것이 있을 때 `pull`하는 방법
### 2.4.1 merge 방식
  ```
  git pull --no-rebase
  ```
### 2.4.2 rebase 방식
  ```
  git pull --rebase
  ```

## ○ 레퍼런스
* [[얄팍한 코딩사전] 제대로 파는 깃강좌(무료)](https://www.youtube.com/watch?v=1I3hMwQU6GU&t=726s)
* [[드림코딩] 깃의 중요한 컨셉 이해하기(무료)](https://academy.dream-coding.com/courses/git)
