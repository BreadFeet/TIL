#  Markdown 문법 

## 제목(heading)

html h tag와 비슷하게 제목의 레벨을 #으로 표현한다. `#` 6개까지

### 제목

#### 제목

##### 제목

###### 제목



## 목록

- 순서가 없는 목록 (-하이픈이나 * 치고 시작)
  - tab하면 소목록 생성
    - 계속 진행
- shift + tab해서 돌아옴
- enter 2번으로 탈출



1. 순서가 있는 목록
   1. tab으로 소목록 생성
      1. 계속 진행
2. 이후는 순서 없는 목록과 같음



## 코드 블록

Inline 코드 블록 생성

- 아래서 쓰이는 '''는 실제로는 ```(backtick)임



1. '''python + enter로 파이썬 블럭 생성 

```python
# 파이썬 주석
print('hello')
```



2. '''html + enter로 html 블럭 생성

```html
<!--html 주석-->
<h1>
    hello
</h1>
```

- 블락에서 탈출해서 enter 치고 싶을 때: **ctrl + enter**



3. '''bash + enter로 git bash 블럭 생성



## 표

typora가 가장 유용한 이유!

| 순번 |  이름  | 비고 |
| ---- | :----: | ---- |
| 1    | 김철수 |      |
| 2    | 김영희 |      |
| 3    | 홍길동 |      |

ctrl + / 를 이용하여 소스코드 확인 가능



## 이미지

- 드래그 드랍으로 이미지 가져오기 가능

- 환경설정 변경한 뒤, 이미지를 상대 경로로 복사하여 관리할 수 있음

  --> 공유한 경우, 절대 경로는 오류나지만 상대 경로는 접근 가능

![pika](../../../../OneDrive/%EC%82%AC%EC%A7%84/pika.png)



##### 이미지의 크기 조정하기

- 우클릭 --> zoom image로 비율 조정
- 세밀한 조정은 소스코드에서 style 조정하면 됨

<img src="../../../../OneDrive/%EC%82%AC%EC%A7%84/pika.png" width="25%" style="zoom:25%;" />



## 링크

아래 클릭하면 syntax 확인 가능! 

- 링크로 이동하려면, ctrl과 함께 클릭

[구글](http://google.com)

[폴더](./md_image)에 활용된 그림이 저장되어 있음



## 기타

*이탤릭체*            * 이탤릭체 *

**볼드체**             ** 볼드체 **

~~취소선~~             ~~ 취소선 ~~

수직선: 하이픈 3개---

---

