# Git 기초 문법

> 분산 버전 관리시스템 (DVCS)



## 준비 사항

* [git bash](gitforwindow.com) : 맥 외에 윈도우 사용하는 경우 필요
* 폴더 - 우클릭 - git bash here: command 창 띄우기
* 뜨는 경로에 (master)가 떠야 git 저장소로 지정된 것





## 기본 문법

#### 0. git 저장소 생성

```bash
# 현재 디렉토리에 비어있는 git 저장소를 생성(./.git)
$ git init
```

* 폴더에 git 저장소를 초기화하면, 

  * `.git` 폴더 생성,
  * bash에는 해당 폴더가 `(master)`라고 표시됨

* 주의사항

  * git 저장소 내에 다른 git 저장소를 만들지 않기!!

    * `git init` 명령어 입력할 때, 이미 (master)가 보이면 절대 입력하지 말 것

      

#### 1. `add`

```bash
$ git add .               # 현재 디렉토리(하위 디렉토리 포함)
$ git add a.txt           # 해당 파일
$ git add myfolder/       # 특정 폴더(/는 안붙여도 되긴 함)
$ git add 디렉토리         
```

```bash
# 디렉토리 추가하는 방법에서 경로를 복사해올 때, \를 /로 바꾸는 작업 필요
# 그대로 붙여쓰면 오류남
$ git add C:/Users/-----/Desktop/git_practice/scenario/newtest
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   newtest/abc.txt
        new file:   test.txt
```



- `working directory` 상태의 파일을 `staging area` 상태로 변경
- commit을 위해 파일들을 추가하는 명령어



#### 예시

```bash
$ touch a.txt         # 파일을 만들고 코드 작업을 한 경우
$ git status          # untracked files로 분류
```

- untracted files: git으로 한번도 관리되지 않은 파일
- add 전후로 status 결과에 차이



#### 2. `commit`

```bash
$ git commit -m 'commit message'    # 커밋 메세지와 함께 버전 기록
$ git log                           # commit된 목록을 보여줌
```

- commit을 통해 하나의 버전으로 기록됨
- commit message는 현재 변경사항들을 잘 나타낼 수 있어야 한다!
- commit은 고유한 id인 `hash value`를 가진다
  - commit 명렁어 실행 후, 또는 `$ git log`를 통해서 확인할 수 있는 긴 코드명
  - SHA-1 알고리즘에 의해 생성



#### 3. `log`

```bash
$ git log                         # Detailed list
$ git log --oneline               # log 목록을 한줄로 보여줌
$ git log -2                      # 2개를 보여줌
$ git log --oneline -1            # 1개를 한줄로 보여줌
```

```bash
$ git reflog           
cf77124 (HEAD -> master) HEAD@{0}: revert: Revert "create first.txt" by deleting the content of first.txt
876c1c1 HEAD@{1}: commit: delete first.txt
9a0c265 HEAD@{2}: commit: commit to revert
6ad8626 HEAD@{3}: commit: create second.txt
390d453 HEAD@{4}: commit (initial): create first.txt
```

- `HEAD@{n}` 의미: HEAD 이동 n번 전 위치





####  4. `status`

```bash
$ git status
$ git status -s          # short version
```

* working directory (add 전), staging area (add 후) 공간의 파일 상태를 확인할 수 있음

![image-20210606074955476](../../../../AppData/Roaming/Typora/typora-user-images/image-20210606074955476.png)





# 원격 저장소(remote repository) 기초

## 기본 설정

- local git 저장소 생성
- Github remote repository 생성 [github](https://github.com/BreadFeet/github_practice)



## 명령어 - Git remote

#### 원격 저장소 설정

```bash
$ git remote add origin 저장소URL
```

- 이제 origin은 원격저장소를 일컫는 말!



#### 원격 저장소 목록 보기

```bash
$ git remote -v            # verbose
origin  https://github.com/BreadFeet/TIL-1.git (fetch)
origin  https://github.com/BreadFeet/TIL-1.git (push)
```



#### 원격 저장소 설정 삭제하기

```bash
$ git remote rm origin      # remove
```



#### push

```bash
$ git push origin master    # 뒷부분은 branch 이름 지정에 따라 다름
$ git push origin main
```

- 원격저장소(`origin`)의 `master` branch에 push함
- push는 commit한 파일만 전송함

![image-20210606075026880](../../../../AppData/Roaming/Typora/typora-user-images/image-20210606075026880.png)















