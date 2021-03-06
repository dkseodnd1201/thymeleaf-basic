Velog : <a href="https://velog.io/@dkseodnd1201/Thymeleaf-%EA%B8%B0%EB%8A%A5">Thymeleaf <๊ธฐ๋ณธ ๊ธฐ๋ฅ></a>




# ๐ Thymeleaf๋?

> - ๋ทฐ ํํ๋ฆฟ ์์ง์ผ๋ก ์๋ฒ์์ ํด๋ผ์ด์ธํธ์๊ฒ ์๋ตํ  ํ๋ฉด์ ๋ง๋ค์ด ์ฃผ๋ ์ญํ ์ ํ๋ค. 


### Thymeleaf์ ํน์ง

>### ์๋ฒ ์ฌ์ด๋ HTML ๋ ๋๋ง(SSR)
> * ์๋ฒ์์ HTML์ ๋์ ์ผ๋ก ๋ ๋๋งํ๋ค.

>### ๋ค์ถ๋ด ํํ๋ฆฟ
> * ์์ HTML๊ตฌ์กฐ๋ฅผ ์ ์งํ๋ค.

>### ์คํ๋ง ํตํฉ์ง์
> * ์คํ๋ง์์ ๊ณต์์ ์ผ๋ก Thymeleaf๋ฅผ ๊ถ์ฅ

### Thymeleaf ์ฌ์ฉ์ ์ธ
~~~HTML
<html xmlns:th="http://www.thymeleaf.org">
~~~

### ๊ธฐ๋ณธํํ์

์ฐธ๊ณ  : [Thymeleaf ๊ธฐ๋ณธํํ์] (https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#standard-expression-syntax, "Thymeleaf basic")
![](https://images.velog.io/images/dkseodnd1201/post/aa07d663-b844-46ed-b950-09315de84b48/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-23%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2010.52.21.png)

---

## ๐ ํ์คํธ
> HTML ์ฝํ์ธ ์ ๋ฐ์ดํฐ๋ฅผ ์ถ๋ ฅํด๋ณด์.

### text/utext

>* ๊ธฐ๋ณธ์ ์ผ๋ก HTML์ ๋ฐ์ดํฐ๋ฅผ ์ถ๋ ฅ : **th:text**
<br>
* ์์ฑ์ด ์๋ ์ฝํ์ธ  ์์ ์ง์ ๋ฐ์ดํฐ๋ฅผ ์ถ๋ ฅ :  **[[๋ด์ฉ]]**

~~~html
<h1>์ปจํ์ธ ์ ๋ฐ์ดํฐ ์ถ๋ ฅํ๊ธฐ</h1>
<ul>
    <li>th:text ์ฌ์ฉ <span th:text = "${data}"></span></li>
    <li>์ปจํ์ธ  ์์์ ์ง์  ์ถ๋ ฅํ๊ธฐ = [[${data}]]</li>
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

>* HTML์์ ํน์๋ฌธ์๋ฅผ **HTML Entitiy**๋ก ๋ณ๊ฒฝํ๋ ๊ฒ์ **Escape๋ผ** ๋งํจ.
+ ๋ทฐ ํํ๋ฆฟ์ผ๋ก HTMLํ๋ฉด์ ์์ฑํ  ๋ ํน์๋ฌธ์์ ์ ์!
* **'<'** ํ๊ทธ๊ฐ **lt;** ์ผ๋ก ๋ฐ๋๋ ์ด์ ๋, HTML์์ ํน์๋ฌธ์๋ฅผ **HTML Entity** ๋ก ๋ณ๊ฒฝ 
**utext*** ์์ u๋ **unescaped**๋ฅผ ์๋ฏธ

HTML Entity : ํน์๋ฌธ์๋ฅผ ๋ฌธ์๋ก ํํํ  ์ ์๋ ๋ฐฉ๋ฒ

### Unescape

> * **Escape** ๋ฅผ ์ฌ์ฉํ์ง ์์ ๊ฒฝ์ฐ
**th:text ๐๐ป th:utext
[[๋ด์ฉ]] ๐ [(๋ด์ฉ)]**

---

## ๐พ ๋ณ์ - SpringEL
> * **Thymeleaf** ์์ ๋ณ์๋ฅผ ์ฌ์ฉํ ๋ ์ฌ์ฉํ๋ ๋ณ์ ํํ์

### SpringEL ๋ค์ํ ํํ์ ์ฌ์ฉ

~~~html
<h1>SpringEL ํํ์</h1>
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

### ์ง์ญ ๋ณ์ ์ ์ธ

~~~html
<h1>์ง์ญ ๋ณ์ - (th:with)</h1>
<div th:with="first=${users[0]}">
    <p>์ฒ์ ์ฌ๋์ ์ด๋ฆ์ <span th:text="${first.username}"></span></p>
</div>
~~~
> * **th:with** ๋ฅผ ์ ์ธํด์ ์ ์ธํ ํ๊ทธ์์ ์ง์ญ ๋ณ์๋ฅผ ์ฌ์ฉํ  ์ ์๋ค.

---

## ๐ ๊ธฐ๋ณธ ๊ฐ์ฒด

> * HTTP ์์ฒญ ํ๋ผ๋ฏธํฐ  : param
* HTTP ์ธ์ ์ ๊ทผ : session
* ์คํ๋ง ๋น ์ ๊ทผ : @

![]  (https://images.velog.io/images/dkseodnd1201/post/bf83599a-f91e-4462-9d88-57384ee2db5c/image.png) 

---
## โฝ๏ธ ์ ํธ๋ฆฌํฐ ๊ฐ์ฒด, ๋ ์ง

> * ๊ถ๊ธํ  ๋๋ง๋ค ์ฐพ์๋ณด์!

์ฐธ๊ณ  : [Thymeleaf ์ ํธ๋ฆฌํฐ ๊ฐ์ฒด] (https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#appendix-b-expression-utility-objects,"ThymeleafUtil")
![](https://images.velog.io/images/dkseodnd1201/post/b4e5f55b-6bdb-42f7-ba94-0b04f7063a92/image.png)

### ๋ ์ง
![](https://images.velog.io/images/dkseodnd1201/post/d6924651-f366-45c3-88e4-725624d6f428/image.png)

---

## ๐ URL

![](https://images.velog.io/images/dkseodnd1201/post/c3d6accd-b217-4ed6-ad97-6512064ebf32/image.png)

>* @{hello} : ๊ธฐ๋ณธ URL
* @{/hello(param1=${param1}, param2=${param2})} : ๋ฉ์๋์ฒ๋ผ ()๋ถ๋ถ ํ๋ผ๋ฏธํฐ๋ก ์ฒ๋ฆฌ
* @{/hello/{param1}/{param2}(param1=${param1}, param2=${param2})} : URL ๊ฒฝ๋ก์ ์๋ ฅ๋ ๋ณ์๊ฐ ์์ผ๋ฉด ๊ฒฝ๋ก๊ฐ ๋ณ์๋ก ์ฒ๋ฆฌ๋จ

---

## ๐Literal
> * ์ฝ๋ ์์์ ๊ณ ์ ๋์ด ์๋ ๊ฐ
ex) 'hello', 10, true, null ( ๋ฌธ์ ๋ฆฌํฐ๋ด์ 'string' ์ด๋ฐ์์ผ๋ก ๊ฐ์ธ์ผํ๋ค.

![](https://images.velog.io/images/dkseodnd1201/post/a83f8446-ecd6-4adc-9e20-5fd39f1ff568/image.png)

---

## ๐งฎ ์ฐ์ฐ

> * ๋น๊ต ์ฐ์ฐ์ : > (gt), < (lt), >= (ge), <= (le), ! (not), == (eq), != (neq, ne)
* Elvis : ${data}?: 'null์ผ๊ฒฝ์ฐ' 
* No-Operation : _ ๊ฐ ๋ถ์ผ๋ฉด ํํ๋ฆฟ์ ๊ฑฐ์น์ง ์์ ๊ฒ์ฒ๋ผ ๋์


![](https://images.velog.io/images/dkseodnd1201/post/e6c32284-8e79-429e-9d16-358a5e15899c/image.png)

---

## ๐ค ์์ฑ ๊ฐ ์ค์ 

![](https://images.velog.io/images/dkseodnd1201/post/981069ef-64a0-442f-a64f-29bc1c9c843e/image.png)
> * th:* ์ง์ ํ ์์ฑ์ผ๋ก ๋์ฒดํ๋ค.
<br>
* th:attrappend : ์์ฑ ๋ค์ ๊ฐ ์ถ๊ฐ
* th:attrprepend : ์์ฑ ์์ ๊ฐ ์ถ๊ฐ
* th:classappend : class ์์ฑ์ ์์ฐ์ค๋  ์ถ๊ฐ
<br>
* checked ์์ฑ๋ง ์์ด๋ ์ฒดํฌ๊ฐ ๋จ
ํ์๋ฆฌํ๋ th:checked ๊ฐ์ด false์ธ ๊ฒฝ์ฐ ์์ฑ์์ฒด๋ฅผ ์ ๊ฑฐ

---

## ๐ ๋ฐ๋ณต

> * {users} ๊ฐ์ ์์ฐจ์ ์ผ๋ก ๊บผ๋ด์ {user}์ ๋ด์ ํ๊ทธ๋ฅผ ๋ฐ๋ณต
* ๋ณ์๋ช + Stat : ๋ฐ๋ณต ์ํ ์ ์ง
>
index : 0๋ถํฐ ์์ ๊ฐ
count : 1๋ถํฐ ์์ ๊ฐ
size : ์ ์ฒด ์ฌ์ด์ฆ
even, odd : ํ์, ์ง์(boolean)
first, last : ์ฒซ, ๋(boolean)
current : ํ ๊ฐ์ฒด


![](https://images.velog.io/images/dkseodnd1201/post/84aecf96-d798-40ee-b619-77a3c7c1391e/image.png)

---
## ๐ค ์กฐ๊ฑด์

### if
![](https://images.velog.io/images/dkseodnd1201/post/8dfee9de-72c7-409f-bfdd-57163de0e596/image.png)

~~~html
<span th:text="'๋ฏธ์ฑ๋์'" th:if="${user.age lt 20}"></span>
~~~
* ์กฐ๊ฑด์ด true์ผ ๋๋ง ๋ ๋๋ง๋๋ค.


### switch
![](https://images.velog.io/images/dkseodnd1201/post/11b4b3ef-7a24-4375-8478-a845ba14ba07/image.png)

---

## ๐งฉ ์ฃผ์
~~~html
<h1>1. ํ์ค HTML ์ฃผ์</h1>
<!--
<span th:text="${data}">html data</span>
-->
~~~
**ํ์ค HTML ์ฃผ์**
* ํ์๋ฆฌํ๊ฐ ๋ ๋๋งํ์ง ์๊ณ  ๋ณด์ฌ์ง๋ค.
~~~html
<h1>2. ํ์๋ฆฌํ ํ์ ์ฃผ์</h1>
<!--/* [[${data}]] */-->
~~~
**ํ์๋ฆฌํ ํ์ ์ฃผ์**
* ๋ ๋๋งํ  ๋ ์ฃผ์ ๋ถ๋ถ์ ์ ๊ฑฐํ๋ค.
~~~html
<h1>3. ํ์๋ฆฌํ ํ๋กํ ํ์ ์ฃผ์</h1>
<!--/*/
<span th:text="${data}">html data</span>
/*/-->
~~~
**ํ์๋ฆฌํ ํ๋กํ ํ์ ์ฃผ์**
* ํ์๋ฆฌํ๋ฅผ ๋ ๋๋ง ํ ๊ฒฝ์ฐ๋ง ๋ณด์ฌ์ง๋ค.
---
## ๐ช ๋ธ๋ก
![](https://images.velog.io/images/dkseodnd1201/post/2a4774d9-11ef-4c36-bbb1-0009394fdf16/image.png)
* ์ ์ฝ๋์์ ํ ํ๊ทธ์ each ๋ฐ๋ณต๋ฌธ์ ํ๋ฒ๋ฐ์ ์ฌ์ฉํ  ์ ์๋ ๊ฒฝ์ฐ์ฒ๋ผ ๋ถ๋์ดํ ๊ฒฝ์ฐ ํ์๋ฆฌํ ์์ฒด ํ๊ทธ **th:block** ๋ฅผ ์ฌ์ฉ


---

## โ๏ธ ์๋ฐ์คํฌ๋ฆฝํธ ์ธ๋ผ์ธ

![](https://images.velog.io/images/dkseodnd1201/post/8ac931a2-aa90-4255-a4a0-cc5838b5f494/image.png)

> * ์ธ๋ผ์ธ ์ฌ์ฉ ์ /ํ ๋ ๋๋ง
  userA ๐๐ป "userA"
  ์ฃผ์ ๋ถ๋ถ์ด ์ ๊ฑฐ๋๊ณ , "userA"๊ฐ ์ ์ฉ
  [[${user}]] ๊ฐ Json์ผ๋ก ๋ณํ 
 
 ---
 
 ## ๐ง ํํ๋ฆฟ ์กฐ๊ฐ
 
> ์น ํ์ด์ง ๊ฐ๋ฐ์์ ๊ณตํต์์ญ์ผ๋ก ์ฐ์ด๋ ๋ถ๋ถ๋ค(ํค๋,ํธํฐ ๋ฑ..)์ด ์๋ค. 
์ฝ๋๋ฅผ ์ฌ์ฌ์ฉ์ฑ์ ๋์ด๊ธฐ ์ํด

![](https://images.velog.io/images/dkseodnd1201/post/a7a4ef6d-8d48-43a1-a846-8577bd0983c2/image.png)

![](https://images.velog.io/images/dkseodnd1201/post/67681a97-ee31-4b64-aaa2-6b6f40072260/image.png)

~~~html
<div th:insert="~{template/fragment/footer :: copy}"></div>
~~~
* ๊ฒฝ๋ก์ ์๋ ฅํ fragment๋ช์ ์ฐพ์์ divํ๊ทธ์ ๋ด์ฉ์ ๋ถ๋ฌ์จ๋ค.

~~~html
<div th:replace="~{template/fragment/footer :: copy}"></div>
~~~
* ๊ฒฝ๋ก์ ์๋ ฅํ fragment๋ช์ ์ฐพ์์ ํ๊ทธ๊น์ง ๋ฎ์ด์์์ง๋ค.

~~~html
<div th:replace="~{template/fragment/footer :: copyParam ('๋ฐ์ดํฐ1', '๋ฐ์ดํฐ2')}"></div>
~~~
* ํ๋ผ๋ฏธํฐ๊ฐ์ ์ ๋ฌํด์ ์ฌ์ฉ ํ  ์๋ ์๋ค.

---

## ๐ก ํํ๋ฆฟ ๋ ์ด์์
> ํํ๋ฆฟ ์กฐ๊ฐ์ ๋ ํ์ฅํด์ ๋ ์ด์์์ผ๋ก ์ ๋ฌํด์ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ์ ์์๋ณด์.

![](https://images.velog.io/images/dkseodnd1201/post/7a71a63f-f437-436f-be7c-cfe56ddf284c/image.png)

![](https://images.velog.io/images/dkseodnd1201/post/48258e28-fb64-45e6-912e-5fe06c313800/image.png)

~~~html
<head th:replace="template/layout/base :: common_header(~{::title},~{::link})">
~~~
* ::title ์ ๊ธฐ์คํ์ด์ง์ title ํ๊ทธ๋ค์ ์ ๋ฌ
* ::link ๋ ๊ธฐ์คํ์ด์ง์ link ํ๊ทธ๋ค์ ์ ๋ฌ

> ํค๋๊ฐ ์ ๋๊ฐ ์๋๋ผ HTML์ ์ฒด์ ์ ์ฉํ  ์๋ ์๋ค.

![](https://images.velog.io/images/dkseodnd1201/post/521cfe2c-93e4-4f8c-84ea-c37b57b5662f/image.png)

![](https://images.velog.io/images/dkseodnd1201/post/26026317-5e5e-4876-b210-714f8753e2d5/image.png)
~~~html
<html th:replace="~{template/layoutExtend/layoutFile :: layout(~{::title}, ~{::section})}"
~~~
* ๊ณตํต์ผ๋ก ์ฐ์ด๋ HTML์ fragment๋ฅผ ์ฐพ์์ ๊ฐ์ ์ ๋ฌํด์ ๋ถ๋ถ ๋ณ๊ฒฝ ํ html ์์ฒด๋ฅผ replace ํ๊ฒ๋๋ค.

![](https://images.velog.io/images/dkseodnd1201/post/615437a4-bb02-4abc-ac50-104a24e1863c/image.png)


<br>

๋ณธ ๊ฒ์๊ธ์ Inflearn ๊น์ํ๋์ ๊ฐ์๋ด์ฉ ์ ๋ฆฌ์๋๋ค.

