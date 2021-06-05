# git diff

> 파일의 변경 내용을 확인할 수 있는 명령어



#### 현재 master의 git 상태

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
```



#### git diff

- 최신 commit과 현재 수정중인(working directory) 파일을 비교

```bash
$ git diff
diff --git a/n_file.txt b/n_file.txt
index e69de29..33a8826 100644
--- a/n_file.txt                      # n_file.txt와 비교
+++ b/n_file.txt
@@ -0,0 +1 @@
+33d9346 이후 수정만 한 파일(add 안함)
\ No newline at end of file
```



#### git diff --staged

- 최신 commit과 staging area 파일을 비교

```bash
$ git diff --staged
diff --git a/c_file.txt b/c_file.txt
index 6f52238..5d1a5d9 100644
--- a/c_file.txt                      # c_file.txt와 비교
+++ b/c_file.txt
@@ -1 +1,3 @@
 33d9346이후 commit 만들기 위해 추가
+
+a2ea0a6이후 add로 만들려고 추가
\ No newline at end of file
```



#### git diff hash1 hash2

- 지정한 두 commit을 비교 --> 하나의 hash만 넣는 경우, 최신 commit과 비교

```bash
$ git diff a2ea0a6
diff --git a/c_file.txt b/c_file.txt
index 6f52238..5d1a5d9 100644
--- a/c_file.txt
+++ b/c_file.txt
@@ -1 +1,3 @@
 33d9346이후 commit 만들기 위해 추가
+
+a2ea0a6이후 add로 만들려고 추가
\ No newline at end of file

diff --git a/n_file.txt b/n_file.txt
index e69de29..33a8826 100644
--- a/n_file.txt
+++ b/n_file.txt
@@ -0,0 +1 @@
+33d9346 이후 수정만 한 파일(add 안함)
\ No newline at end of file
```



#### git diff branch1 branch2

- Branch 간의 상태 비교
  - commit하기 전에는 master와 branch의 상태가 같아서 비교해도 결과값이 없음

```bash
# (feature) branch 상태
$ git log --oneline
0d0fb1f (HEAD -> feature) create a.txt
a2ea0a6 (master) c_file commit
33d9346 include n_text.txt

$ git diff master feature            # (feature - master)의 차이
diff --git a/a.txt b/a.txt           # 어느 branch에서 실행해도 같은 결과
new file mode 100644
index 0000000..08050de
--- /dev/null
+++ b/a.txt
@@ -0,0 +1,2 @@
+feature branch에서 수정함
+master에서도 보일까? 예
\ No newline at end of file
```





