# git config

> git 환경 설정

* global, local 등으로 옵션을 줄 수 있다. 

  

### 초기 설정

```bash
$ git config --global user.name "유저이름"
$ git config --global user.email "이메일"
```

* 사용자 등록 과정으로 github 정보와 동일할 필요는 없음



### 지정된 설정 확인하기

```bash
$ git config --global -l      # 간단한 리스트
user.email=이메일 주소
user.name=유저이름
core.editor=code --wait

$ git config --list           # 설정 내용 full list
```





### 커밋 편집기 변경

```bash
$ git config --global core.editor "code --wait"    # vs code로 설정 
```

* 해당 명령어는 반드시 vs code가 설치되어 있어야 함
* vs code 설치 시, 아래 사항을 반드시 설정해야 사용할 수 있음. 설정하지 않았던 경우에는 재설치 하는 방법밖에 없음

<img src="../../../../OneDrive/%EC%82%AC%EC%A7%84/image-20210604231921556.png" alt="image-20210604231921556" style="zoom:67%;" />

<img src="../../../../AppData/Roaming/Typora/typora-user-images/image-20210606075622156.png" alt="image-20210606075622156" style="zoom:67%;" />

- 설정이 잘 되어서 위 내용이 뜨는 경우, 확인하고 종료하면 됨

