Velog : <a href="https://velog.io/@dkseodnd1201/Thymeleaf-%EA%B8%B0%EB%8A%A5">Thymeleaf <기본 기능></a>




# 🍃 Thymeleaf란?

> - 뷰 템플릿 엔진으로 서버에서 클라이언트에게 응답할 화면을 만들어 주는 역할을 한다. 


### Thymeleaf의 특징

>### 서버 사이드 HTML 렌더링(SSR)
> * 서버에서 HTML을 동적으로 렌더링한다.

>### 네추럴 템플릿
> * 순수 HTML구조를 유지한다.

>### 스프링 통합지원
> * 스프링에서 공식적으로 Thymeleaf를 권장

### Thymeleaf 사용선언
~~~HTML
<html xmlns:th="http://www.thymeleaf.org">
~~~

### 기본표현식

참고 : [Thymeleaf 기본표현식] (https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#standard-expression-syntax, "Thymeleaf basic")
![](https://images.velog.io/images/dkseodnd1201/post/aa07d663-b844-46ed-b950-09315de84b48/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-23%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2010.52.21.png)

---

## 📃 텍스트
> HTML 콘텐츠에 데이터를 출력해보자.

### text/utext

>* 기본적으로 HTML에 데이터를 출력 : **th:text**
<br>
* 속성이 아닌 콘텐츠 안에 직업 데이터를 출력 :  **[[내용]]**

~~~html
<h1>컨텐츠에 데이터 출력하기</h1>
<ul>
    <li>th:text 사용 <span th:text = "${data}"></span></li>
    <li>컨텐츠 안에서 직접 출력하기 = [[${data}]]</li>
</ul>
~~~

### Escape

~~~html
<ul>
    <li>th:text = <span th:text="${data}"></span></li>
    <li>th:utext = <span th:utext="${data}"></span></li>
</ul>

<h1><span th:inline="none">[[...]] vs [(...)]</span></h1>
<ul>
    <li><span th:inline="none">[[...]] = </span>[[${data}]]</li>
    <li><span th:inline="none">[(...)] = </span>[(${data})]</li>
</ul>
~~~

>* HTML에서 특수문자를 **HTML Entitiy**로 변경하는 것을 **Escape라** 말함.
+ 뷰 템플릿으로 HTML화면을 생성할 때 특수문자에 유의!
* **'<'** 태그가 **lt;** 으로 바뀌는 이유는, HTML에서 특수문자를 **HTML Entity** 로 변경 
**utext*** 에서 u는 **unescaped**를 의미

HTML Entity : 특수문자를 문자로 표현할 수 있는 방법

### Unescape

> * **Escape** 를 사용하지 않을 경우
**th:text 👉🏻 th:utext
[[내용]] 👉 [(내용)]**

---

## 👾 변수 - SpringEL
> * **Thymeleaf** 에서 변수를 사용할때 사용하는 변수 표현식

### SpringEL 다양한 표현식 사용

~~~html
<h1>SpringEL 표현식</h1>
<ul>Object
    <li>${user.username} =    <span th:text="${user.username}"></span></li>
    <li>${user['username']} = <span th:text="${user['username']}"></span></li>
    <li>${user.getUsername()} = <span th:text="${user.getUsername()}"></span></li>
</ul>
<ul>List
    <li>${users[0].username}    = <span th:text="${users[0].username}"></span></li>
    <li>${users[0]['username']} = <span th:text="${users[0]['username']}"></span></li>
    <li>${users[0].getUsername()} = <span th:text="${users[0].getUsername()}"></span></li>
</ul>
<ul>Map
    <li>${userMap['userA'].username} =  <span th:text="${userMap['userA'].username}"></span></li>
    <li>${userMap['userA']['username']} = <span th:text="${userMap['userA']['username']}"></span></li>
    <li>${userMap['userA'].getUsername()} = <span th:text="${userMap['userA'].getUsername()}"></span></li>
</ul>
~~~

![](https://images.velog.io/images/dkseodnd1201/post/35600e0d-eb8e-4d30-854e-489f518725fe/image.png)

### 지역 변수 선언

~~~html
<h1>지역 변수 - (th:with)</h1>
<div th:with="first=${users[0]}">
    <p>처음 사람의 이름은 <span th:text="${first.username}"></span></p>
</div>
~~~
> * **th:with** 를 선언해서 선언한 태그안에 지역 변수를 사용할 수 있다.

---

## 😕 기본 객체

> * HTTP 요청 파라미터  : param
* HTTP 세션 접근 : session
* 스프링 빈 접근 : @

![]  (https://images.velog.io/images/dkseodnd1201/post/bf83599a-f91e-4462-9d88-57384ee2db5c/image.png) 

---
## ⛽️ 유틸리티 객체, 날짜

> * 궁금할 때마다 찾아보자!

참고 : [Thymeleaf 유틸리티 객체] (https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#appendix-b-expression-utility-objects,"ThymeleafUtil")
![](https://images.velog.io/images/dkseodnd1201/post/b4e5f55b-6bdb-42f7-ba94-0b04f7063a92/image.png)

### 날짜
![](https://images.velog.io/images/dkseodnd1201/post/d6924651-f366-45c3-88e4-725624d6f428/image.png)

---

## 📇 URL

![](https://images.velog.io/images/dkseodnd1201/post/c3d6accd-b217-4ed6-ad97-6512064ebf32/image.png)

>* @{hello} : 기본 URL
* @{/hello(param1=${param1}, param2=${param2})} : 메서드처럼 ()부분 파라미터로 처리
* @{/hello/{param1}/{param2}(param1=${param1}, param2=${param2})} : URL 경로에 입력된 변수가 있으면 경로가 변수로 처리됨

---

## 📍Literal
> * 코드 안에서 고정되어 있는 값
ex) 'hello', 10, true, null ( 문자 리터럴은 'string' 이런식으로 감싸야한다.

![](https://images.velog.io/images/dkseodnd1201/post/a83f8446-ecd6-4adc-9e20-5fd39f1ff568/image.png)

---

## 🧮 연산

> * 비교 연산자 : > (gt), < (lt), >= (ge), <= (le), ! (not), == (eq), != (neq, ne)
* Elvis : ${data}?: 'null일경우' 
* No-Operation : _ 가 붙으면 템플릿을 거치징 않은 것처럼 동작


![](https://images.velog.io/images/dkseodnd1201/post/e6c32284-8e79-429e-9d16-358a5e15899c/image.png)

---

## 🤔 속성 값 설정

![](https://images.velog.io/images/dkseodnd1201/post/981069ef-64a0-442f-a64f-29bc1c9c843e/image.png)
> * th:* 지정한 속성으로 대체한다.
<br>
* th:attrappend : 속성 뒤에 값 추가
* th:attrprepend : 속성 앞에 값 추가
* th:classappend : class 속성에 자연스레 추가
<br>
* checked 속성만 있어도 체크가 됨
타임리프는 th:checked 값이 false인 경우 속성자체를 제거

---

## 🔁 반복

> * {users} 값을 순차적으로 꺼내서 {user}에 담아 태그를 반복
* 변수명 + Stat : 반복 상태 유지
>
index : 0부터 시작 값
count : 1부터 시작 값
size : 전체 사이즈
even, odd : 홀수, 짝수(boolean)
first, last : 첫, 끝(boolean)
current : 현 객체


![](https://images.velog.io/images/dkseodnd1201/post/84aecf96-d798-40ee-b619-77a3c7c1391e/image.png)

---
## 🤝 조건식

### if
![](https://images.velog.io/images/dkseodnd1201/post/8dfee9de-72c7-409f-bfdd-57163de0e596/image.png)

~~~html
<span th:text="'미성년자'" th:if="${user.age lt 20}"></span>
~~~
* 조건이 true일 때만 렌더링된다.


### switch
![](https://images.velog.io/images/dkseodnd1201/post/11b4b3ef-7a24-4375-8478-a845ba14ba07/image.png)

---

## 🧩 주석
~~~html
<h1>1. 표준 HTML 주석</h1>
<!--
<span th:text="${data}">html data</span>
-->
~~~
**표준 HTML 주석**
* 타임리프가 렌더링하지 않고 보여진다.
~~~html
<h1>2. 타임리프 파서 주석</h1>
<!--/* [[${data}]] */-->
~~~
**타임리프 파서 주석**
* 렌더링할 때 주석 부분을 제거한다.
~~~html
<h1>3. 타임리프 프로토타입 주석</h1>
<!--/*/
<span th:text="${data}">html data</span>
/*/-->
~~~
**타임리프 프로토타입 주석**
* 타임리프를 렌더링 한 경우만 보여진다.
---
## 🪁 블록
![](https://images.velog.io/images/dkseodnd1201/post/2a4774d9-11ef-4c36-bbb1-0009394fdf16/image.png)
* 위 코드에서 한 태그에 each 반복문을 한번밖에 사용할 수 없는 경우처럼 부득이한 경우 타임리프 자체 태그 **th:block** 를 사용


---

## ♎️ 자바스크립트 인라인

![](https://images.velog.io/images/dkseodnd1201/post/8ac931a2-aa90-4255-a4a0-cc5838b5f494/image.png)

> * 인라인 사용 전/후 렌더링
  userA 👉🏻 "userA"
  주석 부분이 제거되고, "userA"가 적용
  [[${user}]] 가 Json으로 변환 
 
 ---
 
 ## 🧀 템플릿 조각
 
> 웹 페이지 개발에서 공통영역으로 쓰이는 부분들(헤더,푸터 등..)이 있다. 
코드를 재사용성을 높이기 위해

![](https://images.velog.io/images/dkseodnd1201/post/a7a4ef6d-8d48-43a1-a846-8577bd0983c2/image.png)

![](https://images.velog.io/images/dkseodnd1201/post/67681a97-ee31-4b64-aaa2-6b6f40072260/image.png)

~~~html
<div th:insert="~{template/fragment/footer :: copy}"></div>
~~~
* 경로에 입력한 fragment명을 찾아서 div태그의 내용을 불러온다.

~~~html
<div th:replace="~{template/fragment/footer :: copy}"></div>
~~~
* 경로에 입력한 fragment명을 찾아서 태그까지 덮어씌워진다.

~~~html
<div th:replace="~{template/fragment/footer :: copyParam ('데이터1', '데이터2')}"></div>
~~~
* 파라미터값을 전달해서 사용 할 수도 있다.

---

## 😡 템플릿 레이아웃
> 템플릿 조각을 더 확장해서 레이아웃으로 전달해서 사용하는 방법을 알아보자.

![](https://images.velog.io/images/dkseodnd1201/post/7a71a63f-f437-436f-be7c-cfe56ddf284c/image.png)

![](https://images.velog.io/images/dkseodnd1201/post/48258e28-fb64-45e6-912e-5fe06c313800/image.png)

~~~html
<head th:replace="template/layout/base :: common_header(~{::title},~{::link})">
~~~
* ::title 은 기준페이지에 title 태그들을 전달
* ::link 는 기준페이지에 link 태그들을 전달

> 헤더가 정도가 아니라 HTML전체에 적용할 수도 있다.

![](https://images.velog.io/images/dkseodnd1201/post/521cfe2c-93e4-4f8c-84ea-c37b57b5662f/image.png)

![](https://images.velog.io/images/dkseodnd1201/post/26026317-5e5e-4876-b210-714f8753e2d5/image.png)
~~~html
<html th:replace="~{template/layoutExtend/layoutFile :: layout(~{::title}, ~{::section})}"
~~~
* 공통으로 쓰이는 HTML의 fragment를 찾아서 값을 전달해서 부분 변경 후 html 자체를 replace 하게된다.

![](https://images.velog.io/images/dkseodnd1201/post/615437a4-bb02-4abc-ac50-104a24e1863c/image.png)


<br>

본 게시글은 Inflearn 김영한님의 강의내용 정리입니다.

