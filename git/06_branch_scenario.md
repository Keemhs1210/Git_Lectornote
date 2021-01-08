## 준비사항

* git 로컬 저장소

  * 루트 커밋이 반드시 있어야함. (한번 커밋!)

* 기본 작업의 흐름

  ```bash
  $ touch 파일명 # 기본 작업
  $ git add .
  $ git commit -m '커밋메시지'
  ```

### 상황 1. fast-foward (혼자 다함)

> fast-foward는 feature 브랜치 생성된 이후 master 브랜치에 변경 사항이 없는 상황

1. feature/index branch 생성 및 이동

   ```bash
   $ git branch feature/index
   $ git branch
     feature/index
   * master
   $ git checkout feature/index
   Switched to branch 'feature/index'
   (feature/index) $
   ```

2. 작업 완료 후 commit

   ```bash
   $ touch index.html
   $ git add .
   $ git commit -m 'Complete index page'
   $ git log --oneline
   5c7e460 (HEAD -> feature/index) Complete index page
   5af4ebd (master) Add README.md
   ```


3. master 이동

   ```bash
   $ git checkout master
   $ git log --oneline
   5af4ebd (HEAD -> master) Add README.md
   ```


4. master에 병합

   ```bash
   (master) $ git merge feature/index
   Updating 5af4ebd..5c7e460
   Fast-forward
    index.html | 0
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 index.html
   ```


5. 결과 -> fast-foward (단순히 HEAD를 이동)

   ```bash
   $ git log --oneline
   5c7e460 (HEAD -> master, feature/index) Complete index page
   5af4ebd Add README.md
   ```

6. branch 삭제

   ```bash
   $ git branch -d feature/index
   ```

![Inkedblank_LI](md-images/Inkedblank_LI.jpg)

---

### 상황 2. merge commit(보고서+발표자료)

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 다른 파일이 수정되어 있는 상황
>
> git이 auto merging을 진행하고, commit이 발생된다.

1. feature/sub branch 생성 및 이동

   ```bash
   $ git checkout -b feature/sub
   ```

2. 작업 완료 후 commit

   ```bash
   $ touch sub.html
   $ git add .
   $ git commit -m 'Complete sub'
   $ git log --oneline
   97fbbf6 (HEAD -> feature/sub) Complete sub
   5c7e460 (master) Complete index page
   5af4ebd Add README.md
   ```

3. master 이동

   ```bash
   $ git checkout master
   ```

4. *master에 추가 commit 이 발생시키기!!*

   * **다른 파일을 수정 혹은 생성하세요!**

   ```bash
   $ touch hotfix.html
   $ git add .
   $ git commit -m 'Hotfix'
   $ git log --oneline
   1cb1426 (HEAD -> master) Hotfix
   5c7e460 Complete index page
   5af4ebd Add README.md
   ```

5. master에 병합

   ```bash
   $ git merge feature/sub
   Merge made by the 'recursive' strategy.
    sub.html | 0
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 sub.html
   ```

6. 결과 -> 자동으로 *merge commit 발생*

   * ![Screen Shot 2021-01-08 at 오후 2.22](md-images/Screen%20Shot%202021-01-08%20at%20%EC%98%A4%ED%9B%84%202.22.png)
   
7. 그래프 확인하기

   ```bash
   $ git log --oneline --graph
   *   2db60ba (HEAD -> master) Merge branch 'feature/sub'
   |\
   | * 97fbbf6 (feature/sub) Complete sub
   * | 1cb1426 Hotfix
   |/
   * 5c7e460 Complete index page
   * 5af4ebd Add README.md
   ```

8. branch 삭제

   ![12312312](md-images/12312312.jpg)

---

### 상황 3. merge commit 충돌

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 동일 파일이 수정되어 있는 상황
>
> git이 auto merging을 하지 못하고, 해당 파일의 위치에 라벨링을 해준다.
>
> 원하는 형태의 코드로 직접 수정을 하고 merge commit을 발생 시켜야 한다.

1. feature/about branch 생성 및 이동

   ```bash
   $ git checkout -b feature/about
   ```

2. 작업 완료 후 commit

   ```bash
   $ touch about.html
   # README 수정
   $ git status
   On branch feature/about
   Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
     (use "git restore <file>..." to discard changes in working directory)
           modified:   README.md
   
   Untracked files:
     (use "git add <file>..." to include in what will be committed)
           about.html
   
   no changes added to commit (use "git add" and/or "git commit -a")
   $ git add .
   $ git commit -m 'Update README & Complete about'
   ```


3. master 이동

   ```bash
   $ git checkout master
   ```


4. *master에 추가 commit 이 발생시키기!!*

   * **동일 파일을 수정 혹은 생성하세요!**

   ```bash
   $ git status
   On branch master
   Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
     (use "git restore <file>..." to discard changes in working directory)
           modified:   README.md
   
   no changes added to commit (use "git add" and/or "git commit -a")
   $ git add .
   $ git commit -m 'Update README'
   ```

5. master에 병합

   ```bash
   $ git merge feature/about
   Auto-merging README.md
   CONFLICT (content): Merge conflict in README.md
   Automatic merge failed; fix conflicts and then commit the result.
   (master|MERGING) $
   ```


6. 결과 -> *merge conflict발생*

   ```bash
   $ git status
   On branch master
   You have unmerged paths.
     (fix conflicts and run "git commit")
     (use "git merge --abort" to abort the merge)
   
   Changes to be committed:
           new file:   about.html
   
   Unmerged paths:
     (use "git add <file>..." to mark resolution)
     # 두 브랜치에서 충돌남.
           both modified:   README.md
   ```


7. 충돌 확인 및 해결

   ```
   # git이 알려준거
   <<<<<<< HEAD          <---- 지금 있는 위치
   # 프로젝트
   
   * 메인
   * 서브
   =======
   # 프로젝트!
   
   * about
   >>>>>>> feature/about <--- merge 
   ```
   
   ```
   # 내가 원한는 거로 바꿈
   # 프로젝트
   
   * 메인
   * 서브
   * about
   ```
   
   ```bash
   $ git add .
   ```


8. merge commit 진행

   ```bash
   $ git commit
   [master d829627] Merge branch 'feature/about'
   ```

9. 그래프 확인하기

    ```bash
   $ git log --oneline --graph
   *   d829627 (HEAD -> master) Merge branch 'feature/about'
   |\
   | * c852005 (feature/about) Update README & Complete about
   * | d57de33 Update README
   |/
   *   2db60ba Merge branch 'feature/sub'
   |\
   | * 97fbbf6 Complete sub
   * | 1cb1426 Hotfix
   |/
   * 5c7e460 Complete index page
   * 5af4ebd Add README.md
   ```


10. branch 삭제

    ```bash
    $ git branch -d feature/about
    ```

    ![merge](md-images/merge.jpg)

    
