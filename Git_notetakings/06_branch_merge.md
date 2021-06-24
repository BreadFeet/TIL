# 준비

> 반드시 root commit(최초 커밋)이 있는 상태에서 브랜치를 조작해야 한다

- commit이 없으면 branch가 만들어지지 않음

* 폴더를 만들고, README.md 파일을 만든 후 commit을 하고 시작!

```bash
$ git commit -m 'create README.md'
[master (root-commit) 818a141] create README.md                # root commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
```





### 상황 1. fast-foward

> fast-foward는 feature 브랜치 생성된 이후 master 브랜치에 변경 사항이 없는 상황

1. feature/index branch 생성 및 이동

   ```bash
   $ git branch feature/index
   $ git checkout feature/index
   ```

   

2. 작업 완료 후 commit

   ```bash
   $ touch index.html
   $ git add . 
   $ git commit -m 'create index.html'
   [feature/index 37ca8fc] create index.html
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 index.html
   $ git log --oneline          # branch는 master의 이전 commit 기록 모두 가져옴
   37ca8fc (HEAD -> feature/index) create index.html
   818a141 (master) create README.md   
   ```
   
   - commit하기 전: master branch로 이동하더라도 index.html 파일이 보임
   
     ​			 -> `git status`에도 확인됨
   
   - commit한 뒤: master branch로 이동하면 index.html 파일이 안 보임
   
     ​			 -> `git log`에 branch commit은 나타나지 않음
   
   


3. master 이동

   ```bash
   $ git checkout master
   Switched to branch 'master'
   ```
   
   


4. master에 병합 - `merge`

   ```bash
   $ git log --oneline
   818a141 (HEAD -> master) create README.md     
   # master에서는 README.md 파일만 commit된 상태
   
   $ git merge feature/index
   Updating 818a141..37ca8fc        # feature/inde
   Fast-forward
    index.html | 0
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 index.html
   ```
   
   


5. 결과 -> fast-foward (단순히 HEAD를 이동)

   ```bash
   $ git log --oneline
   37ca8fc (HEAD -> master, feature/index) create index.html    # commit hash도 넘어옴 
   818a141 create README.md  
   ```

   

6. branch 삭제

   ```bash
   $ git branch -d feature/index
   Deleted branch feature/index (was 37ca8fc)
   ```

---



### 상황 2. merge commit

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 서로다른 파일이 수정되어 있는 상황
>
> git이 auto merging을 진행하고 commit이 발생한다.



1. feature/style branch 생성 및 이동

   ```bash
   $ git checkout -b feature/style
   Switched to a new branch 'feature/style'
   ```

   

2. 작업 완료 후 commit

   ```bash
   $ touch style.css
   $ git add .
   $ git commit -m 'create style.css'
   $ git log --oneline
   6644a76 (HEAD -> feature/style) create style.css
   37ca8fc (master) create index.html
   818a141 create README.md
   ```

   

3. master 이동

   ```bash
   $ git checkout master
   Switched to branch 'master'
   ```

   

4. master에 추가 commit 발생시키기!!

   **- 다른 파일을 수정 혹은 생성!**

   ```bash
   $ touch master.html
   $ git add .
   $ git commit -m 'create master.html'
   $ git log --oneline
   d5a1921 (HEAD -> master) create master.html
   37ca8fc create index.html
   818a141 create README.md
   ```

   

5. master에 병합 - merge

   ```bash
   $ git merge feature/style
   ```

   

6. 결과 -> 자동으로 *merge commit 발생*

   * Visual studio code 라면, 

      ![image-20210606080126734](../../../../AppData/Roaming/Typora/typora-user-images/image-20210606080126734.png)

      - 초록색 instruction에 따라 commit message를 삭제한 뒤 저장, 종료하면,

      ```bash
      $ git merge feature/style
      error: Empty commit message.
      Not committing merge; use 'git commit' to complete the merge.
      ```

        --> merge를 중단할 수 있다!

      

      - `git commit`하면 merge를 완료할 수 있다.

      ```bash
      $ git commit
      [master 4ccec5a] Merge branch 'feature/style' to include style.css with keeping the change in master      # 직접 입력한 commit message가 출력됨
      
      $ git log --oneline
      4ccec5a (HEAD -> master) Merge branch 'feature/style' to include style.css with keeping the change in master
      d5a1921 create master.html
      6644a76 (feature/style) create style.css
      37ca8fc create index.html
      818a141 create README.md
      ```

   

   - 또는 vim 편집기 화면이 나타나는 경우,

   <img src="../../../../AppData/Roaming/Typora/typora-user-images/image-20210606080150581.png" alt="image-20210606080150581" style="zoom:67%;" />

   자동으로 작성된 커밋 메시지를 확인하고, `esc`를 누른 후 `:` `w` `q`를 순서대로 입력하고 엔터를 눌러서 저장 및 종료

   (`w` : write, `q` : quit)



7. 그래프 확인하기

    ```bash
    $ git log --graph --oneline
    *   4ccec5a (HEAD -> master) Merge branch 'feature/style'
    |\
    | * 6644a76 (feature/style) create style.css
    * | d5a1921 create master.html
    |/
    * 37ca8fc create index.html
    * 818a141 create README.md
	```
	
	


8. branch 삭제

   ```bash
   $ git branch -d feature/style
   Deleted branch feature/style (was 6644a76).
   ```

---



### 상황 3. merge commit 충돌

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 동일 파일이 수정되어 있는 상황
>
> git이 auto merging을 하지 못하고, 해당 파일의 위치에 라벨링을 해준다.
>
> 원하는 형태의 코드로 직접 수정을 하고 merge commit을 해야한다.
>
> => 이전 chapter pull error와 같은 상황!



1. feature/about branch 생성 및 이동

   ```bash
   $ git checkout -b feature/about
   Switched to a new branch 'feature/about'
   ```



2. feature/about에서 새 파일 만들고, README.md 파일도 수정!

   ```bash
   $ touch about.html
   # README.md 파일 열어서 수정하고 저장!
   
   $ git status                     
   On branch feature/about
   Changes not staged for commit:            # commit된 적 있는 파일
     (use "git add <file>..." to update what will be committed)
     (use "git restore <file>..." to discard changes in working directory)
           modified:   README.md
   
   Untracked files:                          # commit된 적 없는 파일
     (use "git add <file>..." to include in what will be committed)
           about.html
   
   no changes added to commit (use "git add" and/or "git commit -a")
   ```
   
   ```bash
   $ git add .
   $ git commit -m 'Update about and README'
   $ git log --oneline
   db20aa2 (HEAD -> feature/about) create about.html and update README.md
   4ccec5a (HEAD -> master) Merge branch 'feature/style'
   d5a1921 create master.html
   6644a76 create style.css
   552a702 Complete index page
   a7f5099 Add README
   ```
   
   


3. master 이동

   ```bash
   $ git checkout master
   ```
   
   


4. master에 추가 commit 발생시키기!

   * **동일 파일을 수정 혹은 생성! **

     **(동일하게 about.html을 생성하고, README.md에 내용을 위와는 다르게 수정) **

   ```bash
   $ git status
   On branch master
   Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
     (use "git restore <file>..." to discard changes in working directory)
           modified:   README.md
   
   Untracked files:
     (use "git add <file>..." to include in what will be committed)
           about.html
   
   no changes added to commit (use "git add" and/or "git commit -a")
   ```

   ```bash
   $ git add .
   $ git commit -m 'Update README'
   $ git log --oneline
   81454df (HEAD -> master) master_c_about_u_README
   4ccec5a Merge branch 'feature/style' 
   d5a1921 create master.html
   6644a76 create style.css
   37ca8fc create index.html
   818a141 create README.md
   ```

   

5. master에 병합

   ```bash
   $ git merge feature/about
   Auto-merging README.md
   CONFLICT (content): Merge conflict in README.md
   Automatic merge failed; fix conflicts and then commit the result.
   # branch가 (master|MERGING)인 상태
   ```
   
   


6. `git status`를 통해 merge conflict 상태를 확인 가능

   ```bash
   $ git status
   On branch master
   You have unmerged paths.
     (fix conflicts and run "git commit")     
     # 충돌 수정 후 'All conflicts fixed'라고 뜨면 git commit으로 진행 가능
     (use "git merge --abort" to abort the merge)   
   
   Unmerged paths:
     (use "git add <file>..." to mark resolution)
     # 수정 후 자동으로 인식하지 못하면 add, commit의 과정을 거쳐야 함
           both modified:   README.md
   
   no changes added to commit (use "git add" and/or "git commit -a")
   ```
   
   


7. 충돌 확인 및 해결

   ```bash
   <<<<<<< HEAD           
   master에서 README.md 파일을 수정함     # 현재 head: master에서 수정된 부분
   =======
   feature/about에서 README 파일 수정    # feature/about에서 수성된 부분
   >>>>>>> feature/about
   ```

   - 내용을 정리하여 수정한 뒤 `git status` 다시 실행

   ```bash
   $ git status                        # 똑같은 메세지 출력
   On branch master
   You have unmerged paths.
     (fix conflicts and run "git commit")
     (use "git merge --abort" to abort the merge)
   
   Unmerged paths:               # 수정사항 인식하지 못함!
     (use "git add <file>..." to mark resolution)
           both modified:   README.md
   
   no changes added to commit (use "git add" and/or "git commit -a")
   ```

   => 바로 `git commit` 할 수 없고, `git add`부터 진행해야 함!

   


8. add 실행 --> 충돌이 수정되었음을 인식함!

   ```bash
   $ git add .
   $ git status
   On branch master
   All conflicts fixed but you are still merging.
     (use "git commit" to conclude merge)
   
   Changes to be committed:
           modified:   README.md
   ```

   

9. merge commit 실행

   ```bash
   $ git commit
   ```

   * Vs code 화면에서 commit message 작성하고 저장, 종료

      

10. 결과 확인

    ```bash
    $ git log --oneline
    bb413ea (HEAD -> master) Merge branch 'feature/about'
    81454df master_c_about_u_README
    db20aa2 (feature/about) create about.html and update README.md
    4ccec5a Merge branch 'feature/style' to include style.css with keeping the change in master
    d5a1921 create master.html
    6644a76 create style.css
    37ca8fc create index.html
    818a141 create README.md
    ```

    ```bash
    $ git log --oneline --graph
    *   bb413ea (HEAD -> master) Merge branch 'feature/about'
    |\
    | * db20aa2 (feature/about) create about.html and update README.md
    * | 81454df master_c_about_u_README
    |/
    *   4ccec5a Merge branch 'feature/style' to include style.css with keeping the change in master
    |\
    | * 6644a76 create style.css
    * | d5a1921 create master.html
    |/
    * 37ca8fc create index.html
    * 818a141 create README.md
    ```

    

11. `git checkout feature/about` 해서 파일을 확인하면, README.md 파일은 merge 되지 않았음!

    -> 이 상태에서 merge를 진행하면, fast-forward

    ```bash
    $ git merge master
    Updating db20aa2..bb413ea        # merge commit hash가 그대로 넘어옴
    Fast-forward
     README.md | 7 ++++++-
     1 file changed, 6 insertions(+), 1 deletion(-)
    ```

    - README.md 파일이 merge 된 상태로 바뀜
    - 그러나 실제로는 branch에서 master를 merge할 일은 없음!



12. feature/about branch에서 결과 확인

    ```bash
    $ git log --oneline
    bb413ea (HEAD -> feature/about, master) Merge branch 'feature/about'
    ```

    ```bash
    $ git log --oneline --graph   
    *   bb413ea (HEAD -> feature/about, master) Merge branch 'feature/about'
    |\
    | * db20aa2 create about.html and update README.md
    * | 81454df master_c_about_u_README
    |/
    *   4ccec5a Merge branch 'feature/style' to include style.css with keeping the change in master
    |\
    | * 6644a76 create style.css
    * | d5a1921 create master.html
    |/
    * 37ca8fc create index.html
    * 818a141 create README.md
    ```

    --> HEAD가 가리키는 값이 변화한 것 외에 모두 같음!

    

13. branch 삭제

    ```bash
    $ git branch -d feature/about
    ```

---



### 위의 상황들을 그림으로 이해하기

![image-20210606072949827](../../../../AppData/Roaming/Typora/typora-user-images/image-20210606072949827.png)
