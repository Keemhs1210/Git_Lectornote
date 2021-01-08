# 원격 저장소 기초

> 원격 저장소를 제공하는 서비스 중 Github을 기준으로 설명한다.

## 준비사항

* git 저장소(로컬)
* 원격 저장소(remote repository)

## 명령어

### 원격 저장소 설정

```bash
$ git remote add origin __원격저장소url__
$ git remote add origin https://github.com/edutak/first.git
```

* 깃아, 원격 저장소(remote) 추가해줘(add) origin(이름)으로 url을

* 설정된 원격 저장소 확인하기

  ```bash
  $ git remote -v
  origin  https://github.com/edutak/first.git (fetch)
  origin  https://github.com/edutak/first.git (push)
  ```

* 설정된 원격 저장소 삭제하기

  ```bash
  $ git remote rm origin
  ```

### push

```bash
$ git push origin master
```

* origin  원격저장소의 master 브랜치로 push

