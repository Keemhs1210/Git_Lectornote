# push error

> 원격 저장소와 로컬 저장소의 이력이 다른 경우 발생

```bash
$ git push origin master
To https://github.com/edutak/python-day2.git
 ! [rejected]        master -> master (fetch first)
 
# error!!!!!
error: failed to push some refs to 'https://github.com/edutak/python-day2.git'
# rejected; 왜냐하면...
# 원격저장소의 커밋들(remote containas work)
# 로컬저장소에 가지고 있지 않다.
# 즉, 원격 저장소 커밋과 로컬 저장소의 커밋이 서로 다르게 구성됨.
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
# 원할거다...
# 먼저 원격 저장소의 변경사항들(remote changes)을 통합
# 다시 push하기 전에..
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

![push](md-images/push.jpg)

## 해결 방법

```bash
$ git pull origin master
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 652 bytes | 72.00 KiB/s, done.
From https://github.com/edutak/python-day2
 * branch            master     -> FETCH_HEAD
   815bf3e..c7581a0  master     -> origin/master
Merge made by the 'recursive' strategy.
 README.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
(base)
```

```bash
$ git log --oneline
# Merge commit!
# 원격저장소 != 로컬 저장소
# 해당 커밋 이력들을 '합쳤다' 커밋
48695b6 (HEAD -> master) Merge branch 'master' of https://github.com/edutak/python-day2
1dab216 hi
c7581a0 (origin/master) Create README.md
815bf3e 파이썬 02
73961ba Day02
```

```bash
$ git push origin master
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 16 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 485 bytes | 485.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 1 local object.
To https://github.com/edutak/python-day2.git
   c7581a0..48695b6  master -> master
```

![push2](md-images/push2.jpg)