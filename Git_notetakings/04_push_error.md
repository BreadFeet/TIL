# Push error

변경 후 push를 하면 아래와 같은 문구를 만날때가 있음 :/

![image-20210606080019500](../../../../AppData/Roaming/Typora/typora-user-images/image-20210606080019500.png)



## 확인 해보기

> 원격저장소 커밋과 로컬 저장소 커밋 히스토리를 서로 비교

![img](https://lh6.googleusercontent.com/ewlxzYgVxnKQfPY4QMcPWsAodW6MJByi-OJIf8JzaGYkp8WO88U5v2nYtZlIjuA3su4A7XtL9AcqAgKJp0j4GI6rHcuWj4g7b9Y40obd28r95Ahmo4Q0xV3pIvRayLcz65SDV6Gm)

![image-20210605182338009](../../../../AppData/Roaming/Typora/typora-user-images/image-20210605182338009.png)

- 서로 불일치 하는 경우 push에 오류가 생긴다!

  -> 앞선 push를 통해 동일한 `hash value`를 갖고 있던 commit이, 

     로컬 또는 원격저장소에서 변경, commit을 하면서 다른 `hash value`를 갖게 된 것





## 해결 방법 - pull

```bash
$ git pull origin master                           # merge되면 commit이 발생함
$ git log --oneline
b7b72e1 (HEAD -> master) Merge branch 'master' of https://github.com/edutak/edutak  
		 # 지금 파일 보고 있는 위치는 로컬의 master branch
3946b62 Update 경력
e884994 (origin/master) Update README.md       # 원격저장소 master branch에서 commit 이력   
dcf3558 Add README
```

![image-20210605182110046](../../../../AppData/Roaming/Typora/typora-user-images/image-20210605182110046.png)

- merge하는 순간 bash에 (master|MERGING)으로 바뀜



#### 예시 1

한 파일을 로컬에서 수정하고 commit하지 않고, 원격에서는 파일을 수정하여 commit한 상태

```bash
$ git pull origin master
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 731 bytes | 26.00 KiB/s, done.
From https://github.com/BreadFeet/TIL
 * branch            master     -> FETCH_HEAD
   f535de7..0aedab3  master     -> origin/master
error: Your local changes to the following files would be overwritten by merge:
        README.md
Please commit your changes or stash them before you merge.
Aborting              # 로컬 수정사항이 commit되지 않았기 때문에 진행시키지 않겠다는 것
```

-> commit 하고 다시 진행하면 됨!



#### 예시 2

한 파일을 로컬, 원격 양쪽에서 수정, commit한 뒤 merge하는 경우, 결과물이 다소 지저분할 수 있음

```bash
$ git pull origin master
From https://github.com/BreadFeet/TIL
 * branch            master     -> FETCH_HEAD
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md         # 지저분하게 합쳐질 것이 예상됨
Automatic merge failed; fix conflicts and then commit the result.
# 이렇게 merge에 실패한 경우에는 commit이 발생하지 않음
```

<img src="../../../../AppData/Roaming/Typora/typora-user-images/image-20210605180525339.png" alt="image-20210605180525339"  />

==> merge후 코드를 정리하는 것도 개발자의 일..

​	정리 한 뒤 commit하고 push해서 원격저장소로 보내면 된다!

```bash
$ git push origin master
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 12 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 725 bytes | 725.00 KiB/s, done.
Total 6 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/edutak/edutak.git
   e884994..b7b72e1  master -> master
```

![image-20210606080056848](../../../../AppData/Roaming/Typora/typora-user-images/image-20210606080056848.png)

- push해야 비로소 Github의 history에서도 merge를 확인할 수 있음!!





## Trouble-Shooting

git을 여러번 pull-push 하다보면 문제가 생겨 막힐 수가 있다. 초보일 경우에는 이런 경우 고민하지 말고,



1. 로컬에서 `push` 하려던 수정된 파일을 다른 위치로 옮겨 놓고, 해당 `.git`이 있던 폴더는 삭제한다.
2. 원격저장소에서 `clone`하여 이전 git 기록을 모두 다시 로컬로 받아온다.
3. 옮겨놓았던 수정된 파일을 clone된 로컬저장소로 옮긴다.
4. 원격저장소로 다시 `push`를 진행한다.

