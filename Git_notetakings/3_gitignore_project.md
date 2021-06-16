# 프로젝트 기본

예시는 아래의 django 프로젝트를 기준으로 함

<img src="../../../../AppData/Roaming/Typora/typora-user-images/image-20210606075748749.png" alt="image-20210606075748749" style="zoom:67%;" />



## Git 저장소 설정

```bash
$ git init
```



## .gitignore

> git으로 관리하지 않을 파일/폴더 등을 관리해줌

* `.gitignore` 파일을 만들어서 관리 

  * 텍스트 문서이지만 별다른 확장자 없이 `.gitignore`로 생성하면 됨
  
  ```bash
  user.csv                 # 특정 파일
  venv/                    # 특정 폴더
  *.csv                    # 특정 확장자를 git에서 제외할 수 있음
  ```
  
* 개발 프로젝트시 어떤 것들을 gitignore로 관리를 하는가?

  1. OS(운영체제)에서 활용되는 파일들 

  2. IDE(통합개발환경 - pycharm), text editor(vs code) 등에서 활용되는 파일 

  * 예) pycharm -> .idea/

  3. 개발 언어(python) 혹은 프레임워크(django)에서 사용되는 파일

  * 예) python -> `__pycache__/` 

  * 예) django -> 가상환경 `venv/`

<img src="../../../../AppData/Roaming/Typora/typora-user-images/image-20210606075855044.png" alt="image-20210606075855044" style="zoom:67%;" />





### * gitignore.io

* [링크](https://gitignore.io)

* 본인 개발 환경에 대한 내용을 넣고 검색하면, 일반적으로 개발자들이 많이 쓰는 .gitignore 문서를 ㅅ생성한다.

* 혹은, github에서 제공하는 문서들을 받아서 활용해도 좋다. 

  [링크](https://github.com/github/gitignore) [파이썬 링크](https://github.com/github/gitignore/blob/master/Python.gitignore)

<img src="../../../../AppData/Roaming/Typora/typora-user-images/image-20210606075923842.png" alt="image-20210606075923842" style="zoom:67%;" />