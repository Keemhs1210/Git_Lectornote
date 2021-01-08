* **20.01.07 ~ 20.01.08 멀티 캠퍼스 Git 특강 교육 내용 정리**

# **Git**

> 인용문 정의하거나 주의할 점 핵심 내용으로 주로 쓰임

> Git은 DVCS, 분산 버전 관리 시스템

# 원격 저장소 설정
````bash
    $git init 
    (master) $
````
★ tip 코드는 결과와 같이 넣어야 보기 좋음
* `.git`  숨김 폴더가 생성된다.
* `(master)` 브랜치 표기

# 기본 흐름
* 어떠한 작업 => `$ touch 파일명`
````bash
 On branch master
 No commits yet
 # 트래킹이 X 파일들add
 # 버전에 기록된적없는 파일들 
 # => 파일 생성 등
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        ../1.txt
        ../first/
        ./
#커밋할 파일이 없다
#but, untraked files는 있다. 
nothing added to commit but untracked files present (use "git add" to track)
````
---
## add

````bash
$git add . #현재 디렉토리(하위까지)
$git add a.txt #특정 파일
$git add test/ #특정 폴더

On branch master

No commits yet
#커밋이 될 변경 사항 들
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   1.txt
        new file:   README.md

````
---
## Commit
> 스냅샷, 버전을 새롭게 만듬

````bash
$git commit -m '커밋메세지'
````
* 해쉬값이 고유한 커밋 의미
  
    예) e93991d982a9e09e0a06d0017434498925ab4390 
* 커밋메시지는 반드시 현재 작업 내용을 나타낼 수 있도록 작성하는 것이 중요하다.
---
# 기타 상태 명령어
### status
````bash
$git status
````
### 커밋 히스토리(log)
````bash
 $git log
    commit e93991d982a9e09e0a06d0017434498925ab4390 (HEAD -> master)
    Author: Keemhs1210 <kimhs1210@gmail.com>
    Date:   Thu Jan 7 14:18:36 2021 +0900

    Add 1.txt

$git log --oneline  
    e93991d (HEAD -> master) Add 1.txt
$git log -2 
    Author: Keemhs1210 <kimhs1210@gmail.com>
    Date:   Thu Jan 7 14:18:36 2021 +0900
    Add 1.txt

$git log -1 --oneline
    e93991d (HEAD -> master) Add 1.txt

````

---
## 원격 저장소 기초
> 원격 저장소를 제공하는 서비스 중 Github을 기준으로 설명한다.

### 준비사항
* git 저장소(local)
* 원격 저장소(remote repository)
---
## 명령어
### 원격 저장소 설정
````bash
$git remote add origin ___원격저장소url___
$git remote add origin git remote add origin https://github.com/Keemhs1210/ first.git
````
* 원격 저장소(remote) url을 추가한다(add) origin(이름)으로
* 설정된 원격 저장소 확인하기
    ````bash
    $git remote -v
    origin http:s//github.com/Keemhs1210/first.git(fetch)
    origin http:s//github.com/Keemhs1210/first.git(push)
````
    
* 설정된 원격 저장소 삭제하기
    ````bash
    $git remote rm origin
    ````
---
### **push**
````bash
$git push origin master
````
* origin 원격 저장소의 master 브랜치로 push
* push는 모든 버전을 push하지만 보여지는 것은 최신 버전이다.

````bash 
project/
    .git/
        보고서/
            .git/
````
* project 로컬 git 저장소 아래에 또 다른 git 저장소가 저장됨
* sub module 활용 x
* git 저장소 아래 다른 git 저장소 사용 금지
  * ex.1) 실수로 특정 디렉터리 C:// git init 한번이라도 함.
    * C:// .git 폴더를 삭제
  * ex.2)폴더를 이동하는 경우
    * 리눅스 폴더에서 git을 쓰다가
    * 아두이노 폴더에서 git을 쓰다가
    * 같이 정리하고 싶어서 옮김
* **예방법**
  * git init 명령어 입력하기 전에 (master)있는지 확인
  * 폴더 이동시에 확인
---
# **좋은 git 커밋 메세지를 작성하기 위한 7가지 약속
1. 제목과 본문을 한 줄 띄워 분리하기
2. 제목은 영문 기준으로 50자 이내
3. 제목 첫글자는 대문자로
4. 제목 끝에 `.` 금지
5. 제목은 `명령조`로
6. 본문은 영문 기준 72줄마다 줄 바꾸기
7. 분문은 `어떻게`보다 `무엇을`, `왜`에 맞춰 작성하기
---
# **Day 2**
## **git 문서 편질을 VS code로 변경하기**

* git bash에서 기본 편집기가 vscode 
* 사용자가 활용하기 불편한 환경으로 편집기를 아래와 같이 설정 가능
````bash
code [파일명]
code 1.txt
````
* pycharm에서 idea, _pychache, venv를 관리 안함
* 로컬에서 실행시켜서 생긴 모델, 소스 코드와 상관 없음
* `gitignore.io`를 활용하여 gitinore 파일 생성 
---
## gitignore
> git으로 관리하지 않을 파일을 관리
`.gitignore 라는 파일을 만들어서 디렉토리를 관리한다.

````bash
a.txt #특정파일
venv # 특정 폴더
*.csv #특정 확장자
````
* 일반적으로 로컬 개발환경과 관련된 파일/폴더는 git으로 관리하지 않는다.
  * ex) 운영체제(윈도우/맥), IDE/TEXT Editor, 특정 언어에서 실행시 생성되는 파일
  * 처음에는 아래의 사이트를 참고하여 gitignore를 만들자.
    * https://gitignore.io
    * https://githun.com/github/gitignore
  * 추가적인 파일(ex, 고객데이터, 키 값)도 설정할 수 있다.
---
## **push error**
* Github 사이트에서 파일을 만들면 로컬 저장소와 원격 저장소간의 commit된 상태가 다르다 그래서 이를 동기화 시켜야함
* reject: 왜냐하면
* 원격저장의 커밋들 (remote contains work)
* 로컬 저장소에 가지고 있지 않다.
* 즉, 원격 저장소 커밋과 로컬 저장소의 커밋이 서로 다르게 구성됨
* 원할거다.
* 먼저 원격 저장소의 번경사항들(remote chages)을 통합
* 다시 push 전에 `$git pull orgin master`
### **해결방법**
* Merge commit
* 원격저장소 != 로컬 저장소
* 해당 커밋 이력들을 '합쳤다' 커밋
  1. 푸쉬 거절
  2. 거절(에러)
  3. pull
  4. push (merge한 commit)
---
## **brach**
### **기본 명령어**

* 브랜치 생성
  ````bash
  $git brach 브랜치 이름
  ````
* 브랜치이동
  ````bash
  $git checkout 브랜치이름
  $git switch 브랜치 이름
  ````
* 브랜치를 생성 및 이동
  ````bash
  $git checkout -b 브랜치 이름
  ````
* 브랜치 목록
  ````bash  
  $git branch
  ````
* 브랜치 병합
  ````bash
  (master) $git merge 브랜치 이름
  ````
  * **주의!** master로 merge 하는 것
  * Git의 Flow 흐름에 따라 merge할 것
* 브랜치 삭제 (단, 다른 브랜치 혹은 master에서 삭제)
  ````bash
  $git branch -d 브랜치이름
  ````
---
### **branch 예제** 
### 준비사항
* git 로컬 저장소
  
  * 루트 커밋이 반드시 있어야함. (한번 커밋!)
* 기본 작업의 흐름
  ````bash
  $touch 파일명 #기본 작업
  $git add .
  $git commit -m "커밋 메세지"
  
  ---
  $touch README.md
  $gid add .
  $git commit -m 'Add README.md'
  ````


### 상황 1. fast-foward (혼자 다함)

> fast-foward는 feature 브랜치 생성된 이후 master 브랜치에 변경 사항이 없는 상황

1. feature/test branch 생성 및 이동
  ````bash
  $git branch feature/index
  $git branch feature/index
  *master
  $git checkout feature/index
  Switched to branch 'feature/index' (freaute/index)
  $
  ````
2. 작업 완료 후 commit
   ````bash
   $touch index.html
   $git add .
   $git commit -m "Complete the index page'
   $git log --oneline
   (HEAD -> feature/index) Complete the index page (master) Add README.md
   ````
3. master 이동
   ````bash
    $git checkout master
    $git log --oneline
    (HEAD -> master) Add README.md
   ````
4. master에 병합
  ````bash
  $git master $git merge feature/index 
  ````
5. 결과 -> fast-foward (단순히 HEAD를 이동)
   ````bash
   $git log --oneline
   ````
6. branch 삭제
   ````bash
   $git branch -d feature/index
   ````
---
### 상황 2. merge commit

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 다른 파일이 수정되어 있는 상황
>
> git이 auto merging을 진행하고, commit이 발생된다.

1. feature/signout branch 생성 및 이동
   ````bash
   $git checkout -b feature/sub
   ````
2. 작업 완료 후 commit
    ````bash
    $touch sub.html
    $git add .
    $git commit -m "Complete the sub"
    $git log --oneline
    ````
3. master 이동
   ````bash
   $git checkout master
   ````
4. master에 추가 commit 이 발생시키기!!
    * **다른 파일을 수정 혹은 생성하세요! -> Hotfix 추가**
    ````bash
    $touch hotfix.html
    $git add .
    $git commit -m 'Hotfix'
    $git log --oneline 
    HEAD -> master Hotfix, Complete the sub, Add README.md
    ````
5. master에 병합
   ```bash
   $git merge feature/sub
   ````
6. 결과 -> 자동으로 *merge commit 발생*

   * vim 편집기 화면이 나타납니다.
   * 자동으로 작성된 커밋 메시지를 확인하고, `esc`를 누른 후 `:wq`를 입력하여 저장 및 종료를 합니다.
     * `w` : write
     * `q` : quit
   * 커밋이  확인 해봅시다.

7. 그래프 확인하기
    ````bash
    $git log --oneline --graph
    ````
8.  branch 삭제
    ````bash
      $git branch -d feature/sub
    ````

* **서로다른 commit 합치는 과정**
---
### 상황 3. merge commit 충돌

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 동일 파일이 수정되어 있는 상황
>
> git이 auto merging을 하지 못하고, 해당 파일의 위치에 라벨링을 해준다.
>
> 원하는 형태의 코드로 직접 수정을 하고 merge commit을 발생 시켜야 한다.

1. feature/board branch 생성 및 이동
  ````bash
  $git checkout -b feature/about
  ````
2. 작업 완료 후 commit
  ````bash
    $touch about.html
    #README 수정해야함
    $git status
    $git add .
    $git commit -m 'Update README and about"
  ````
3. master 이동
  ````bash
  $git checkout master
  ````
4. *master에 추가 commit 이 발생시키기!!*
  * **동일 파일을 수정 혹은 생성하세요! -> README 수정**
  ````bash
  $git status
  $git add .
  $git commit -m "Update README"
  ````

5. master에 병합
  ````bash
  $git merge feature/about #충돌 발생
  ````

6. 결과 -> *merge conflict발생*

7. 충돌 확인 및 해결
  * VScode를 통해 git에 있는 현재 상태를 내가 원하는 상태로 변경
  ````bash
  $git status #git staus는 답을 알고 있다. 
  #현재 상황에서는 both modified README.md 
  ````
8. merge commit 진행
   ```bash
   $ git add . #변경사항 다시 업로드
   ```
   * vim 편집기 화면이 나타납니다.

   * 자동으로 작성된 커밋 메시지를 확인하고, `esc`를 누른 후 `:wq`를 입력하여 저장 및 종료를 합니다.
     * `w` : write
     * `q` : quit

   * 커밋이  확인 해봅시다.
9. 그래프 확인하기
    ````bash
    $git log --oneline --graph
    ````
10. branch 삭제
    ````bash
    $git branch -d feature/about
    ````
----
## 중간 프로젝트 참여시
1. 원격 저장소 복제 (원격저장소 이력 복사)
    ````bash
    $git clone 원격 저장소URL
    ````
2. 복제 후 주의 사항!
   1. 명령어를 입련한 곳에 원격 저장소 이름의 폴더가 생김
   2. cd 원격저장소 한번 더 사용

* 다른 사람 원격 저장소 활용 clone
  * 다른 사람의 저장소를 활용하므로 init은 필요 없다. -> 오류를 줄일 수 있음
* branch를 활용하는 것이 git flow
---
#### Fork와 shared Reposity와 다른점
1. 푸쉬 권한이 있는지 없는지에 갈린다.
---
#### Fork가 지속적으로 업데이트 된 경우
````bash
$git remote add upstream https:"//github.com/github-flowtutorials/fork-pull-model.git
$git pull upstream master
$git push origin master
````
## **Undoing**
---
### **Unstaing (add 취소)**
````bash 
$git status  #status를 통해 staging area에 있는 파일 파악
$git restore --stage <file>

````
### **Working Directory 취소**
> 커밋되지 않은 변경사항을 되돌릴 수 없다.
> 
````bash
$git status #status를 통해 wprlomg directory안에 있는 파일을 확인한다.
$git restore <file> 
````
**커밋은 건들지 말자 실수해도 앞으로 가자**
### **Commit 메세지 변경**
> 공개된 저장소에 push한 경우 절대 변경 금지
````bash
$git commit --amend #명령어를 입력하면 에디터가 생성되는데 자신이 원하는 Commit Msg로 변경한다.
$git log --oneline #log를 확인해보면 커밋의 Hash 값이 변경되어 다른 커밋이 된다.
````
* 이 명령어를 활용하면 빠뜨린 파일도 커밋 시킬 수 있다. (Hash 값 변경은 동일)
  ````bash
  $git add .
  $git add commit --amend
  ````
  * Amend 명령어는 메세지 수정 뿐만 아니라 staging area에서 commit area 영역으로 넘어간 파일들이
  * 다시 stage area로 넘어간다. 
---
### **reset vs revert**
* **revert**
  ````bash
  #log에 기록이 남는다
  $git revert <log_hash_value>
  ````

* **reset** 
  > 공개된 저장소에 push가 된 경우 주의할 것
  ````bash
  #log를 안남긴다.
  $git reset --hard <log_hash_value>
  ````
  * 옵션
    * 기본(--mixed): 변경사항을 SA에 보관
    * --soft: 변경사항 및 WD 내용까지 WD에 모두 보관
    * --hard: 모든 변경사항을 삭제 (**주의**)


# Git config
* 전체 글로벌 옵션 확인
````bash
  $git config --global -l
````
## comit author 설정
* 컴퓨터 설정이 반드시 필요
````bash
  $git config --global user.name '_____'
  $git config --global user.email '______'
````
*자격증명관리 -> windwos 자격 증명 github.com 내용 reset하여 사용해야한다.
