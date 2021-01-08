# Undoing

## unstaging (add 취소)

```bash
$ git status
On branch master
Changes to be committed:
# unstage를 하기 위하여 사용해..
  (use "git restore --staged <file>..." to unstage)
        modified:   a.txt
        new file:   b.txt

```

```bash
$ git restore --staged a.txt
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   b.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   a.txt

```

![3125646324](md-images/3125646324.jpg)

## Working directory 작업 내용 취소

> 커밋되지 않은 변경사항을 되돌릴 수는 없다.

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  # (WD에 있는) 변경사항을 버리기위해서 아래의 명령어
  (use "git restore <file>..." to discard changes in working directory)
        modified:   a.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

![63546435](md-images/63546435.jpg)

## Commit 메시지 변경

> 공개된 저장소에 push한 경우 절대 변경 금지.

```bash
$ git log --oneline
b29a55e (HEAD -> master) Add d.txt
4bacb2d Complete
9b54031 Add a.txt
```

```bash
$ git commit --amend
hint: Waiting for your editor to close the file..[master 8645fc8] Add c.txt
 Date: Fri Jan 8 17:16:25 2021 +0900
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 c.txt
 
$ git log --oneline
# 커밋 해시값 변화, 즉 다른 커밋이 됨.
8645fc8 (HEAD -> master) Add c.txt
4bacb2d Complete
9b54031 Add a.txt
```

* 이 명령어를 활용하면 빠뜨린 파일도 같이 커밋 시킬 수 있다.

  ```bash
  $ git log --oneline
  # 두개의 파일을 커밋하려고함.
  65840b9 (HEAD -> master) Add omit.txt and d.txt
  8645fc8 Add c.txt
  4bacb2d Complete
  9b54031 Add a.txt
  
  $ git status
  On branch master
  Untracked files:
    (use "git add <file>..." to include in what will be committed)
    # add를 깜빡!
          omit.txt
  
  nothing added to commit but untracked files present (use "git add" to track)
  ```

  ```bash
  $ git add .
  $ git commit --amend
  hint: Waiting for your editor to close the file..[master 1f7fb86] Add omit.txt and d.txt
   Date: Fri Jan 8 17:23:56 2021 +0900
   2 files changed, 0 insertions(+), 0 deletions(-)
   create mode 100644 d.txt
   create mode 100644 omit.txt
  ```

![8678678678678](md-images/8678678678678.jpg)

















