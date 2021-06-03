# Git - 기초 문법

> 분산 버전 관리시스템 (DVCS)



# 준비 사항

* [git bash](gitforwindow.com) : 맥 외에 윈도우 사용하는 경우 필요
* 폴더 - 우클릭 - git bash here: command 창 띄우기
* 뜨는 경로에 (master)가 떠야 git 저장소로 지정된 것



# 기본 문법

### 0. git 저장소 생성

'''bash 블럭 생성

```bash
# 현재 디렉토리에 비어있는 git 저장소를 생성(./.git)
$ git init
```

* 폴더에 git 저장소를 초기화하면, 

  * .git 폴더 생성,
  * bash에는 해당 폴더가 (master)라고 표시됨

* 주의사항

  * git 저장소 내에 다른 git 저장소를 만들지 않기

    * `git init` 명령어 입력할 때, 이미 (master)가 보이면 절대 입력하지 말 것

      

### 1. `add`

```bash
$ git add .              # 현재 디렉토리(하위 디렉토리 포함)
$ git add {directory}    # 해당 디렉토리 
$ git add myfolder       # 특정 폴더
$ git add a.txt          # 해당 파일
```

- `working directory` 상태의 파일을 `staging area` 상태로 변경
- commit을 위해 파일들을 추가하는 명령어



#### 예시

```bash
$ touch a.txt           # 파일을 만들고 코드 작업을 한 경우
$ git status          # untracked file, added file, committed file을 보여줌  
```

- untracted files: git으로 한번도 관리되지 않은 파일
- add 전후로 status 결과에 차이



### 2. `commit`

```bash
$ git commit -m 'commit message'    # 커밋 메세지와 함께 버전 기록
$ git log                           # commit된 목록을 보여줌
```

- commit을 통해 하나의 버전으로 기록됨
- commit message는 현재 변경사항들을 잘 나타낼 수 있어야 한다!
- commit은 고유한 id인 `hash value`를 가진다
  - commit 명렁어 실행 후, 또는 $ git log를 통해서 확인할 수 있는 긴 코드명
  - SHA-1 알고리즘에 의해 생성



### 3. `log`

```bash
$ git log
$ git log --oneline               # log 목록을 한줄로 보여줌
$ git log -2                      # 2개를 보여줌
$ git log --oneline -1            # 1개를 한줄로 보여줌
```





###  4. `status`

```bash
$ git status
```

* working directory (add 전), staging area (add 후) 공간의 파일 상태를 확인할 수 있다.

![img](md_images/z7QsjQG-af7iZICqxOuTEPpZfMuwJv6uAwrOFfYGSDe8f8etRL7mvB8P665qPWnIfR7cIhD73lJjzvYyegMRhF6imYIF3Qv8eL9sluAKgE0ALCkzidVmouvJloDNMfw9TEN53Mt3)























