# 원격 저장소(remote repository) 기초

## 기본 설정



- local git 저장소 생성
- Github remote repository 생성 [github](https://github.com/BreadFeet/github_practice)



## 명령어

#### 원격 저장소 설정

```bash
$ git remote add origin 저장소URL
```

- 이제 origin은 원격저장소 이름



#### 원격 저장소 목록 보기

```bash
$ git remote -v      # verbose
```



#### 원격 저장소 설정 삭제하기

```bash
$ git remote rm origin      # remove
```



#### push

```bash
$ git push origin master
```

- 원격저장소(origin)에 master branch를 push함
- push는 commit한 파일만 전송함

