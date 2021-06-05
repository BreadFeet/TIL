# Reset vs Revert



## reset - 취소하면서 기록 삭제

> commit 취소하고 이전으로 돌아가기

* `--hard`: 특정 commit으로 돌아가면서,***현재 작업하던 staging area, working directory 모든 내용 사라짐***

```bash
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   c_file.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   n_file.txt

$ git log --oneline
bb5e499 (HEAD -> master) update 1
33d9346 include n_text.txt

$ git reset --hard 33d9346            # 돌아가려는 hash를 지정해야 함!
HEAD is now at d547a8a !!!

$ git status                         
On branch master                      # 모든 기록 사라짐
nothing to commit, working tree clean

$ git log --oneline
33d9346 (HEAD -> master) include n_text.txt
```

- Hash 대신 HEAD 번호로 지정하여 reset 가능 

```bash
$ git reflog                         # HEAD 번호 확인 
cf77124 (HEAD -> master) HEAD@{0}: revert: Revert "create first.txt" by deleting the content of first.txt
876c1c1 HEAD@{1}: commit: delete first.txt
9a0c265 HEAD@{2}: commit: commit to revert
6ad8626 HEAD@{3}: commit: create second.txt
390d453 HEAD@{4}: commit (initial): create first.txt

$ git reset --hard HEAD~2            # 3번째=HEAD@{2}로 가고 싶음
HEAD is now at 9a0c265 commit to revert

$ git log --oneline
9a0c265 (HEAD -> master) commit to revert
6ad8626 create second.txt
390d453 create first.txt
```



- `--mixed` : 특정 commit으로 돌아가면서, ***현재 작업 내용은 모두 그대로 유지됨***

  ​		  ***다만, staging area에서 add 취소됨, working directory은 그대로 유지***

  ​		  (옵션을 따로 지정하지 않으면 `--mixed` 작동함)

  1. 특정 commit hash를 지정하지 않은 경우 = 가장 최신 commit hash를 지정한 것과 같음

```bash
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   c_file.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   n_file.txt

$ git log --oneline
1fcafd0 (HEAD -> master) update c_file
33d9346 include n_text.txt

$ git reset --mixed                     # 특정 commit hash 지정 안하면
Unstaged changes after reset:           # hash: 1fcafd0를 지정한 것과 같음
M       c_file.txt
M       n_file.txt

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   c_file.txt            # 모두 working directory로 내려옴
        modified:   n_file.txt

$ git log --oneline
1fcafd0 (HEAD -> master) update c_file    # commit 이력은 그대로
33d9346 include n_text.txt
```

​	

​    2. 특정 commit hash를 지정한 경우

```bash
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   c_file.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   n_file.txt

$ git log --oneline
572babc (HEAD -> master) c_file changed
33d9346 include n_text.txt

$ git reset --mixed 33d9346
Unstaged changes after reset:
M       c_file.txt           # 실제 파일 내용은 1의 경우와 같음!
M       n_file.txt

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   c_file.txt
        modified:   n_file.txt

$ git log --oneline
33d9346 (HEAD -> master) include n_text.txt
```



- `--soft` : 특정 commit으로 돌아가면서, ***현재 작업 내용 모두 그대로 유지됨***

  ​		 ***staging area, working directory도 그대로 유지***

```bash
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   c_file.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   n_file.txt

$ git log --oneline
a2ea0a6 (HEAD -> master) c_file commit
33d9346 include n_text.txt

$ git reset --soft 33d9346                   # 함께 출력되는 값 없음

$ git status                                 # 상태 똑같음
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   c_file.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   n_file.txt

$ git log --oneline
33d9346 (HEAD -> master) include n_text.txt
```





## revert - 취소면서 취소 기록 commit

> 현재 상태를 유지하되, 특정 commit만 취소하기
>
> **`$ git revert` + 취소할 commit hash**

- 지정한 commit에서 실행한 내용만 취소하고, 이후 기록은 가지고 있음!

  => ***<u>실행내용 취소 후, 남은 commit끼리 merge하여 새로운 commit을 발생!!</u>*** 

- reset과는 다르게, commit이 되지 않은 수정사항들이 있으면 오류남!

```bash
$ git log --oneline
9a0c265 (HEAD -> master) commit to revert     # 두 파일에 내용 추가하고 commit
6ad8626 create second.txt                     # 빈 파일 생성
390d453 create first.txt                      # 빈 파일 생성

$ git revert 390d453
error: Reverting is not possible because you have unmerged files.
hint: Fix them up in the work tree, and then use 'git add/rm <file>'
hint: as appropriate to mark resolution and make a commit.
fatal: revert failed
```

-> 위 `revert` 명령은, 390d453으로 돌아가고 싶다는 뜻이 아님!! 

   **390d453이 실행한 commit을 취소하고 싶다는 뜻임!!! **

--> 이게 지시하는 내용은 first.txt 만든 것을 취소하지만, 이후 파일에 내용 추가한 commit은 유지하라는 뜻         	**"불가능"**



#### 해결방법

- first.txt의 내용을 지운 빈 문서로 commit하면 merge 가능

```bash
$ git commit -m 'delete first.txt'     # 내용만 지우고 파일은 있는 상태로 commit
[master 876c1c1] delete first.txt
 1 file changed, 1 deletion(-)

$ git revert 390d453
Removing first.txt
[master cf77124] Revert "create first.txt" by deleting the content of first.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 first.txt

$ git log --oneline
cf77124 (HEAD -> master) Revert "create first.txt" by deleting the content of first.txt   
                                             # revert commit 발생    
876c1c1 delete first.txt
9a0c265 commit to revert
6ad8626 create second.txt
390d453 create first.txt
```



## 위 내용을 그림을 표현

![image-20210606073111717](../../../../AppData/Roaming/Typora/typora-user-images/image-20210606073111717.png)
