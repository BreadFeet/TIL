# Undoing

## 1. 수정하다 이전 버전(commit) 상태로 되돌리고 싶을 때 

> *주의: 해당 명령어를 실행한 이후 절대로 다시 되돌아 갈 수 없음!!!

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   a.txt

no changes added to commit (use "git add" and/or "git commit -a")
$ git restore a.txt       # 수정사항 다 사라짐
```

-> 이런 경우에는, 그냥 파일 안에서 ctrl+z로 돌아가는 것이 나음

<br>

<br>

## 2. add 취소

### commit이 된적 없는 파일

- 파일을 취소하려는 경우

```bash
$ git add .
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md
        new file:   a.txt
```



```bash
$ git rm --cached a.txt       # add 취소하려는 파일
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        a.txt                 # unstaged
```

- 폴더를 취소하려는 경우

```bash
$ git rm --cached -r newtest   # add 취소하려는 폴더
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        newtest/               # unstaged
        test.txt
```

<br>

### commit이 된 적이 있어 git이 기억하는 파일

```bash
$ git add .
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md
        modified:   a.txt
```



```bash
$ git restore --staged a.txt
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   a.txt
```



### commit된 적 없는 파일, 있는 파일이 섞였을 때는?

```bash
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   c_file.txt
        new file:   n_file.txt
```

==> Instruction을 따르면 되기 때문에 기억해야 할 필요는 없음!! :D

<br>

<br>

## 3. Commit message 수정

> 공개된 저장소에 push된 커밋은 절대 메시지 수정하지 않기! 
>
> => 파일 내용은 같은데 hash value가 변경되기 때문

```bash
$ git commit -m 'commit c_file.txt'
[master (root-commit) 594d8e2] commit c_file.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 c_file.txt

$ git commit --amend
[master e550f09] commit message changed        # 새로운 hash와 commit message
 Date: Sun Jun 6 01:02:33 2021 +0900
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 c_file.txt
```

```bash
$ git log --oneline
e550f09 (HEAD -> master) commit message changed   # 처음 commit 기록은 사라짐
```

* VS code나 vim 등 커밋 메시지 작성 화면이 나오면 수정, 저장하면 된다

<br>

<br>

## 4. 빠진 파일을 추가 커밋하고 싶을 때

#### 해결방법

```bash
$ git add n_file.txt                        # 마저 파일을 추가함
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   n_file.txt
        
$ git commit --amend             # amend만으로 n_file이 포함된 새로운 commit이 발생
[master 33d9346] include n_text.txt         # hash 바뀜
 Date: Sun Jun 6 01:02:33 2021 +0900
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 c_file.txt              # 모든 파일을 commit함
 create mode 100644 n_file.txt
```

```bash
$ git status                        # commit이 모두 완료된 것을 확인가능
On branch master
nothing to commit, working tree clean

$ git log --oneline                 # amend 전 commit 이력 사라짐
33d9346 (HEAD -> master) include n_text.txt
```

- 하나의 commit, hash로 관리하려면, `git commit --amend`
- 별도의 commit, hash로 관리하려면, 원래대로 `git command -m`



