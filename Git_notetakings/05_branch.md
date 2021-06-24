# Branch 명령어

* branch 생성

  ```bash
  $ git branch 브랜치명
  ```

* branch 목록

  ```bash
  $ git branch
  ```

* branch 이동

  ```bash
  $ git checkout 브랜치명            # bash 화면에서 (브랜치명)으로 이동한 것을 볼 수 있음
  ```
  
* branch 생성 및 이동

  ```bash
  $ git checkout -b 브랜치명
  ```

* branch 병합

  ```bash
  $ git merge 브랜치명               # (master)에 있는 상태에서 
  ```

  * `master` branch에 `브랜치명` 을 병합

* branch 삭제

  ```bash
  $ git branch -d 브랜치명
  ```

  