# branch

## 기본 명령어

* 브랜치 생성

  ```bash
  $ git branch 브랜치이름
  ```

* 브랜치 이동

  ```bash
  $ git checkout 브랜치이름
  $ git switch 브랜치이름   # 최근 명령어
  ```

* 브랜치를 생성 및 이동

  ```bash
  $ git checkout -b 브랜치이름
  ```

* 브랜치 목록

  ```bash
  $ git branch
  ```

* 브랜치 병합

  ```bash
  (master) $ git merge 브랜치이름
  ```

  * **주의!!!!** master로 브랜치이름을 merge 하는 것!

* 브랜치 삭제

  ```bash
  $ git branch -d 브랜치이름
  ```

  