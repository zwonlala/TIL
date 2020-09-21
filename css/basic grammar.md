<h1 style="display: inline-block; line-height:0pt; margin:10px padding:10px">CSS</h1>

<details>
<summary ><b style="font-size: 25px">목차</b></summary>

<ol>

## <li>[선언방식](#%EC%84%A0%EC%96%B8%EB%B0%A9%EC%8B%9D-1)</li>
## <li>[기본 선택자](#%EA%B8%B0%EB%B3%B8-%EC%84%A0%ED%83%9D%EC%9E%90-basic-selectors)</li>
## <li>[복합 선택자](#%EB%B3%B5%ED%95%A9-%EC%84%A0%ED%83%9D%EC%9E%90-1)</li>
## <li>[가상 클래스 선택자](#%EA%B0%80%EC%83%81-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%84%A0%ED%83%9D%EC%9E%90pseudo-classes-selectors)</li>
## <li>[가상 요소 선택자](#%EA%B0%80%EC%83%81-%EC%9A%94%EC%86%8C-%EC%84%A0%ED%83%9D%EC%9E%90-pseudo-element-selectors)</li>
## <li>[속성 선택자](#%EC%86%8D%EC%84%B1-%EC%84%A0%ED%83%9D%EC%9E%90-attribute-selectors)</li>
## <li>[상속](#%EC%83%81%EC%86%8D-1)</li>
## <li>[우선순위](#%EC%9A%B0%EC%84%A0%EC%88%9C%EC%9C%84-1)</li>


</ol>
</details>
<br>


## 선언방식

`속성 : 속성값;` 이 한 세트!

```
선택자 {
  속성: 속성값;
  속성: 속성값;
}
```

`선택자`는 HTML의 **속성**과 **속성값**을 지정할 대상을 검색하는 역할

주석의 경우 `/* ~~ */`~~, `//`~~  사용가능 


<details>
<summary>HTML / CSS / JS 주석처리</summary>

- HTML : \<!--내용--> 

- CSS : ~~//내용 ,~~ /* 내용 */

- JS : //내용 , /* 내용 */
</details>

<br><br>


### **1. in-line 방식**  
태그에 직접 작성하는 방법  
태그 안에 style 속성에 문자열로 css 값을 설정  
선택자가 필요 없음  

*유지보수가 힘들어지기 때문에 비추하는 방법!*

그래서 아예사용하지 않는 방법이냐...? -> 그건 아님!     
코드에 직접 작성하는 것이 아니라 특정 기능들을 사용해서 삽입될 수 있음..!

`<div style="color: red;">태그에 직접 작성하는 inline 방식</div>`

<br>

### **2. embedded 방식**   
HTML의 \<style> 태그 안에 작성하는 방법  

```
<head>
  <style>
    div {
      color: red;
    }
  </style>
...
```

<br>

### **3. link 방식**

CSS 파일로 정의하여 사용하는 방법  
link 태그 사용하여 외부에 정의된 CSS 받아옴  
가장 일반적인 방식  
HTML에 \<head> 태그에 \<link> 태그를 삽입하여 사용  

```
<link rel="stylesheet" href="/css/main.css">
```

<br>

### **4. import 방식**

CSS에는`@규칙`이라는 것이 있는데 그중에 하나!(Ex) 미디어 쿼리)  
`@import`를 사용하여 외부 문서로 CSS를 불러와 적용하는 방식

```HTML
<head>
  <link rel="stylesheet" href="css/common1.css"> //link 방식
</head>
<body>
  <div>HELLO</div>
</body
```

```CSS
//common1.css
@import url("./common2.css"); //import 방식
```

```CSS
//common2.css
div {
  color: red;
  font-size: 20px;
  font-weight: bold;
}
```

`link` `import ` 방식 모두 외부에 있는 CSS 파일을 가져온다는 점에서 동일하나,   
`link` 방식은 HTML에서 외부 CSS를 가져온다는 점  
`import` 방식은 CSS에서 외부 CSS를 가져온다는 점에서 다르다!   

<br>

**주의할 점!**

link 방식으로 여러 CSS 파일을 불러오면,   
파일들을 동시에(병렬적으로) 불러와 시간이 단축되지만,  
 
import 방식으로 여러 CSS 파일을 불러오면,    
파일들이 순차적으로(직렬적으로? 현재 불러와지는 파일이 다 불러와져야지 다음 CSS 파일 불러옴) 불러와져 로딩 시간이 오래 걸릴 수 있다  

**그럼 import 방식은 별로인것이냐...?**

만약에 1번 CSS 파일에 참조하는 내용이 있어, 1번 CSS 파일이 불러와져야 2번 CSS 파일이 정상적으로 동작을 하는 경우에 사용한다!   

<br><br><br><br>




## 기본 선택자 (Basic Selectors)

### 1. 전체 선택자(Universal Selector) `*`

모든 태그를 다 선택하는 것  
(요소 내부의) 모든 요소를 선택   

<br>

### 2. 태그 선택자(Type Selector)  `E`

선택자를 입력하는 부분에 적용하려는 태그의 이름을 입력.  
태그 이름이 E 인 요소 선택.  
태그 선택자 앞뒤에 아무것도 없다 -> 태그로서 해석이 된다...!

<br>

### 3. 클래스 선택자(Class Selector)  `.CLASS_NAME`

선택자를 입력하는 부분에 적용하려는 클래스 이름 앞에 온점(`.`)을 붙여 사용  
HTML class 속성의 값이 `CLASS_NAME`인 요소 선택

<br>

### 4. id 선택자(ID Selector)  `#ID`

선택자를 입력하는 부분에 적용하려는 id 이름 앞에 온점(`#`)을 붙여 사용    
HTML id 속성의 값이 ID 인 요소 선택


<br><br><br><br>




## 복합 선택자

### 1. 일치 선택자(Basic Combinator) `EF`
선택자 E와 선택자 F를 동시에 만족하는 요소 선택(E, F는 기본 선택자!)  
선택자 두개 붙여서 사용
    
ex)
```HTML
<div>
  <ul>
    <li>사과</li>
    <li>딸기</li>
    <li class="orange">오렌지</li>
  </ul>
  <div>당근</div>
  <p>토마토</p>
  <span class="orange">오렌지</span>  <!--선택-->
</div>
```

```CSS
span.orange { //span 태그이며, class에 "orange" 있는 요소 선택
  color: red;
}
```

<br>

### 2. 자식 선택자(Child Combinator) `E > F`
`E`의 자식 요소 `F`를 선택(E, F는 기본 선택자!)  
여기서 자식이란 바로 다이렉트 아래를 의미함!   
`E`는 조건이고 `F`는 우리가 검색하고자 하는 대상  

ex)
```HTML
<div>
  <ul>
    <li>사과</li>
    <li>딸기</li>
    <li class="orange">오렌지</li>  <!--선택-->
  </ul>
  <div>당근</div>
  <p>토마토</p>
  <span class="orange">오렌지</span>
</div>
```

```CSS
ul > .orange { //ul 태그의 자식 요소 중 class에 "orange" 있는 요소 선택
  color: red;
}

```

<br>

### 3. 후손(하위) 선택자(Descendant Combinator) `E F`  
`E`의 후손(하위)요소 `F`를 선택  
여기서 후손이란, `E` 태그 내부에 있는 모든 요소를 의미함(즉, 자식도 포함!)  
   
자손 선택자, 후손 선택자, 하위 선택자, ... 으로 불림     

`'띄어쓰기'`가 선택자의 기호로 사용됨  

`E`는 조건이고 `F`는 우리가 검색하고자 하는 대상     

ex)
```HTML
<div>
  <ul>
    <li>사과</li>
    <li>딸기</li>
    <li class="orange">오렌지</li>  <!--선택-->
  </ul>
  <div>당근</div>
  <p>토마토</p>
  <span class="orange">오렌지</span>  <!--선택-->
</div>
```

```CSS
div .orange { //div 태그 아래(후손,하위)에 있는 요소 중 class에 "orage" 있는 요소 선택
  color: red;
}
```

<br>

### 위 예제로 보는 부모/자식/조상/후손/형제 용어 정리
<details>
<summary><b></b></summary>

- div는 부모, ul은 자식 관계
- ul은 부모, li는 자식 관계
- div는 조상(상위), li는 후손(하위)

- ul, div, span은 형제 관계

- 가장 상위의 div 태그 입장에서 자기보다 밑에 있는(자신이 감싸고 있는) 모든게 후손(하위)!!!   
(바로 한단계 밑에 있는 요소만 자식으로 말하는 것. 자식도 후손에 포함!)

- li 태그 입장에서 자기보다 위에 있는(자신을 감싸고 있는) 모든게 조상(상위)!!!    
(바로 한단계 위에 있는 요소만 부모라고 말하는 것. 부모도 조상에 포함!)
</p>
</details>

<br>

### 4. 인접 형제 선택자(Adjacent Sibling Combinator) `E + F`
`E`의 **다음** 형제 요소 `F` **하나**만 선택  
(형제 : 같은 '부모' 요소를 공유하는 요소)     

일반 형제 선택자와 인접 형제 선택자 모두 **"다음"** 형제 요소 찾는 것!!      
(이전 형제 요소를 찾는 건 없다!!)      

`E`는 조건이고 `F`는 우리가 검색하고자 하는 대상         

ex)
```HTML
<ul>
  <li>딸기</li>
  <li>수박</li>
  <li class="orange">오렌지</li>
  <li>망고</li>  <!--선택-->
  <li>사과</li>
</ul>
```

```CSS
.orange + li { //@송지원 설명 다시 적기!
  color: red;
}
```

<br>

### 5. 일반 형제 선택자(General Sibling Combinator) `E ~ F`
`E`의 **다음** 형제 요소 `F` **모두** 선택  
(형제 : 같은 '부모' 요소를 공유하는 요소) 
    
일반 형제 선택자와 인접 형제 선택자 모두 **"다음"** 형제 요소 찾는 것!!     
(이전 형제 요소를 찾는 건 없다!!)      

`E`는 조건이고 `F`는 우리가 검색하고자 하는 대상        

ex)
```HTML
<ul>
  <li>딸기</li>
  <li>수박</li>
  <li class="orange">오렌지</li>
  <li>망고</li>  <!--선택-->
  <li>사과</li>  <!--선택-->
</ul>
```

```CSS
.orange ~ li { //@송지원 설명 다시 적기!
  color: red;
}
```

<br><br><br><br>



 
## 가상 클래스 선택자(Pseudo-Classes Selectors)

복합 선택자와 마찬가지로 기본 선택자를 활용하는 개념
  
`가상 클래스 선택자` 앞에 콜론(`:`) 기호가 붙음   

*+ 콜론 기호가 두개(`::`) 있는 것은 가상 요소 선택자!*    

### 1. hover `E:hover`  
`E`에 마우스(포인터)가 올라가 있는 동안에만 `E` 선택.   
(`E`는 기본 선택자!)     


ex) a 태그 마우스 올리면 글자 색상 바뀌는 예제  

```CSS
a:hover {
  color: red;
}
```
```HTML
<a href="http://www.naver.com">NAVER</a>
```

<br>

### 2. active `E:active`   
`E`를 마우스로 클릭하는 동안에만 `E` 선택.  
(`E`는 기본 선택자!)     


ex) 마우스로 div 태그 눌렀을 때만 가로 길이 2배 늘어나는 예제      
(+ transition 속성 추가하여 전환이 부드러워 짐)  

```CSS
div {
  width: 100px;
  height: 100px;
  background: tomato;
  transition: 0.4s;
}
div:active {
  width: 200px;
}
```

<br>

### 3. focus `E:focus`  
`E`가 포커스 된 동안에만 `E` 선택    
(`E`는 기본 선택자!)     
 
[대화형 콘텐츠](https://developer.mozilla.org/ko/docs/Web/Guide/HTML/Content_categories#%EB%8C%80%ED%99%94%ED%98%95_%EC%BD%98%ED%85%90%EC%B8%A0) 에서 사용 가능 (대화형 콘텐츠 : input, img, tabindex, ...)  



ex) input 태그에 입력을 하려고 focus 될때 디자인 변하는 예제  

```CSS
input {
  width: 100px;
  outline: none;
  padding: 5px 10px;
  border: 1px solid lightgray;
  transition: 0.4s;
}
input:focus {
  width: 200px;
  border-color: red;
}
```
```HTML
<input type="text">
```

<br>

### 4. first-child `E:first-child`  
`E`가 형제 요소 중 첫번째 요소라면 선택     

(`E`는 기본 선택자!    
일반적인 예시 등에 태그 선택자만 사용하는데, id 선택자도 사용 가능한 듯! [참고](https://thrillfighter.tistory.com/575))   

(형제 요소 -> **같은 부모**를 공유하는 요소. ~~같은 조상 공유~~🙅🏻)  


ex) 첫번째 li 태그 선택하는 예제  

```CSS
.fruits li:first-child {
  color: red;
}
```
```HTML
<ul class="fruits">
  <li>딸기</li>  <!--선택-->
  <li>사과</li>
  <li>오렌지</li>
  <li>망고</li>
</ul>
```

<br>

### 5. last-child `E:last-child`  
`E`가 형제 요소 중 마지막 요소라면 선택
  
(`E`는 기본 선택자!    
일반적인 예시 등에 태그 선택자만 사용하는데, id 선택자도 사용 가능한 듯! [참고](https://thrillfighter.tistory.com/575))    

(형제 요소 -> **같은 부모**를 공유하는 요소. ~~같은 조상 공유~~🙅🏻)     
 


ex) 마지막 li 태그 선택하는 예제  

```CSS
.fruits li:last-child {
  color: red;
}
```
```HTML
<ul class="fruits">
  <li>딸기</li>  
  <li>사과</li>
  <li>오렌지</li>
  <li>망고</li> <!--선택-->
</ul>
```

<br>

### 6. nth-child `E:nth-child(n)`
`E`가 형제 요소 중 n번째 요소라면 선택  

(`E`는 기본 선택자!    
일반적인 예시 등에 태그 선택자만 사용하는데, id 선택자도 사용 가능한 듯! [참고](https://thrillfighter.tistory.com/575))   

(형제 요소 -> **같은 부모**를 공유하는 요소. ~~같은 조상 공유~~🙅🏻)     
  

(n 키워스 사용시, n에 0부터 대입하여 적용 && 요소는 1번째 부터 카운트!)   


ex) 두번째 li 태그 선택하는 예제  

```CSS
.fruits li:nth-child(2) {
  color: red;
}
```
```HTML
<ul class="fruits">
  <li>딸기</li>
  <li>사과</li>  <!--선택-->
  <li>오렌지</li>
  <li>망고</li>
</ul>
```


ex) 짝수 번째 요소들만 선택하는 예제   

```CSS
//n에 0부터 1, 2, 3, ... 대입하면, 
//(0,) 2, 4, ... 번째 요소 선택함!
//0번째 요소는 없음!
.fruits li:nth-child(2n) {
  color: red;
}
```
```HTML
<ul class="fruits">
  <li>딸기</li>
  <li>사과</li>  <!--선택-->
  <li>오렌지</li>
  <li>망고</li>  <!--선택-->
</ul>
```


ex) 3번째 요소 이후부터 선택하는 예제   

```CSS
//n에 0부터 1, 2, 3, ... 대입하면, 
//3, 4, 5, ... 번째 요소 선택함!
.fruits li:nth-child(n+3) { 
  color: red;
}
```
```HTML
<ul class="fruits">
  <li>딸기</li>
  <li>사과</li>
  <li>오렌지</li>  <!--선택-->
  <li>망고</li>  <!--선택-->
</ul>
```

<br>

### 7. xxx-child 주의사항 

ex) 예상과 달리 잘 적용되지 않는 예제   

```CSS
//n에 0부터 1, 2, 3, ... 대입하면, 
//3, 4, 5, ... 번째 요소 선택함!
.fruits p:nth-child(1) {
  color: red;
}
```
```HTML
<!--선택된 요소 없음-->
<div class="fruits">
  <div>딸기</div>
  <p>사과</p>
  <p>망고</p>
  <span>오렌지</span>
</div>
```
.fruits의 첫번째 자식 요소가 \<p> 태그가 아니기 때문에 선택되지 않습니다    

**<설명>**   

먼저 CSS를 대충 해석해 보면, *"fruits" 클래스가 있는 요소의 자손들 중에, 첫번째 p 태그*가 선택자 임.     

하지만 위 해석은 잘못된 해석임!!!!     

해석을 할때는 `좌 -> 우`가 아니라 `우 -> 좌`로 해석해야지 정확한 해석을 할 수 있다!    

즉 CSS를 해석하면    

`"(우)~의 자식요소 첫번째 것을 찾는데, 그것은 p 태그여야 하고,`     
`(좌)p 태그는 "fruits"를 클래스로 가지고 있는 것의 자식요소 여야 합니다!"`    

이게 정확한 해석이다!     


ex) :first-child 여러곳에 적용하는 예제

```HTML
<div class="box-group">
  <div>1</div>
  <div>2</div>
  <div>3
    <p>3-1</p>
    <div>3-2</div>
    <div>3-3</div>
  </div>
</div>
```

위와 같은 HTML에서 first-child인 1과 3-1에 모두 스타일을 적용해주고 싶다면,    

```CSS
.box-group :first-child {
  ~~~
}
```

이렇게 해줄 수 있다, 만약   

```CSS
.box-group div:first-child {
  ~~~
}
```

```CSS
.box-group p:first-child {
  ~~~
}
```

위와 같이 구현하면, 1 또는 3-1만 선택된다!     
:first-child 의 앞부분을 공간으로 놓으면 1, 3-1 모두 선택할 수 있다!    

<br>

### 8. nth of type `E:nth-of-type(n)`
`E`의 타입(태그이름)과 동일한 타입인 형제 요소 중 `E`가 n번째 요소라면 선택  
(`E`는 **태그** 선택자! not 기본 선택자!)
     
(n 키워스 사용시, n에 0부터 대입하여 적용 && 요소는 1번째 부터 카운트!)    

nth-of-type에서 type이라는 것은 태그 이름을 의미하는 것이다!      


ex) \<p>들 중에서 첫번째 요소를 선택하는 예제

```CSS
.fruits p:nth-of-type(1) {
  color: red;
}
```
```HTML
<div class="fruits">
  <div>딸기</div>
  <p>사과</p>  <!--선택-->
  <p>망고</p>
  <span>오렌지</span>
</div>
```
    



ex) nth-of-type에 태그 선택자가 아닌 클래스 선택자를 사용한 경우   

```CSS
.fruits .red:nth-of-type(1) {
  color: red;
}
```
```HTML
<!--선택된 요소 없음-->
<ul class="fruits">
  <li>오렌지</li>
  <li class="red">딸기</li>
  <li>망고</li>
  <li class="red">사과</li>
</ul>
```

**<설명>**

2번째와 4번째에 있는 .red 요소의 타입(태그이름)은 li 이기 때문에,   
:nth-of-type(1) 선택자는 \<li>들 중에서 첫번째 요소를 선택하고 "red" class가 있는지 체크하게 됩니다   
 
:nth-of-child(1)에 해당하는 요소는 \<li>오렌지\</li> 이지만, "red" 클래스가 없음  
 
따라서 조건에 맞는 요소가 없으므로 선택되지 않는다.

<br>

### 9. 부정 선택자 NOT `E:not(S)`  
`S`가 아닌 `E` 선택
기본적으로는 E라고 나온 것을 기반으로 검색을 하는데,    
`S` 선택자를 빼겠다(제외하겠다)   
(`E`, `S`는 기본 선택자!)      


ex) 모든 요소에 빨간색 글자를 설정하고, "strawberry"만 빨간색 글자를 설정하고 싶지 않을 때 예시

```CSS
.fruits li:not(.strawberry) {
  color: red;
}
```
```HTML
<ul class="fruits">
  <li>오렌지</li>  <!--선택-->
  <li class="strawberry">딸기</li>
  <li>망고</li>  <!--선택-->
  <li>사과</li>  <!--선택-->
</ul>
```

<br><br><br><br>




## 가상 요소 선택자 (Pseudo-Element Selectors)

가상 요소 선택자는 CSS를 통해 HTML에 가상의 요소를 생성해, 추가적인 텍스트 삽입/스타일을 먹일 수 있음!

가상 클래스 선택자는 콜론이 한개! Ex)div:first-child     
가상 요소 선택자는 콜론이 두개! Ex)li::before   

해당문법이 콜론을 하나 사용하는 문법에서 두개를 사용하는 형태로 변경됨!    
(그래서 이전 블로그는 콜론 하나 사용하는 것으로 설명하기도 함..!)       

### 1. before `E::before`  
E 요소 **내부의 앞**에, 내용(content)을 삽입!    
그리고 위의 내용은 가상의 요소(내용)! 

**(중요!)** content 속성 무조건 사용해야 함!!    
content 속성이 없으면 아무것도 적용 안됨

그리고 삽입되는 특정 부분만 다른 스타일을 먹이는 것도 가능!


ex) 각 li 태그 앞쪽에 특정 문구 삽입 예제

```CSS
ul li:before { /* support IE 8 */
  content: "$";
  font-weight: bold;
  color: red;
}
ul li::before {
  content: "$";
  font-weight: bold;
  color: red;
}
```
```HTML
<ul>
  <li>1</li>  <!-- $1 -->
  <li>2</li>  <!-- $2 -->
  <li>3</li>  <!-- $3 -->
  <li>4</li>  <!-- $4 -->
</ul>
```




ex) content로 이미지 삽입도 가능!

```CSS
div::before {
  content: url("../images/smile.png");
}
```

url()을 통해서 이미지를 삽입할 수 있습니다.

<br>

### 2. after `E::after`  
E 요소 **내부의 뒤**에, 내용을 삽입!   
그리고 위의 내용은 가상의 요소(내용)!    

**(중요!)** content 속성 무조건 사용해야 함!!   

ex) 숫자 뒤에 ".0" :after 사용해서 붙여주는 예제     

```CSS
ul li:after { /* support IE 8 */
  content: ".0";
}
ul li::after {
  content: ".0";
}
```
```HTML
<ul>
  <li>1</li>  <!-- 1.0 -->
  <li>2</li>  <!-- 2.0 -->
  <li>3</li>  <!-- 3.0 -->
  <li>4</li>  <!-- 4.0 -->
</ul>
```

<br><br><br><br>




## 속성 선택자 (Attribute Selectors)

HTML의 속성은 **Attribute** &nbsp;&nbsp;&nbsp; *(ex) \<div class="~">*  
CSS의 속성은 **Property** &nbsp;&nbsp;&nbsp; *(ex) color: red;*  
라고 함  

속성 선택자는 **HTML의 속성(Attribute)** 을 가지고 선택하는 것  

속성 선택자 사용시 매번 id나 class를 부여하지 않아도, 속성이 있는 것 만으로도 스타일을 지정할 수 있다!   

<br>

### 1. ATTR `[attr]`
속성 attr을 포함한 요소 선택  

ex) div 요소 중 class 속성이 있는 요소를 선택하겠다  

```CSS
[class] { ~ }
```

ex) 속성에 disabled 있는 요소 선택 예제  

```CSS
[disabled] {
  opacity: 0.2;
}
```
```HTML
<input type="text" value="HEROPY">
<input type="password" value="1234">
<input type="text" value="disabled text" disabled>
```

<br>

### 2. ATTR = VALUE `[attr=value]`  
속성 attr을 포함하며 **속성 값이 value**인 요소 선택  

`[type="password"]` 이런 형태, `[type=password]` 이런 형태 모두 가능!   


ex) type이 password인 input 태그 선택하는 예제  

```CSS
[type="password"] {
  color: red;
}
```
```HTML
<input type="text" value="HEROPY">
<input type="password" value="1234">
<input type="text" value="disabled text" disabled>
```

<br>

### 3. ATTR ^= VALUE `[attr^=value]`
속성 attr을 포함하며 속성 값이 value로 **시작하는** 요소 선택   

ex) class 명이 'btn-'으로 시작하는 요소만 선택하는 예제   

```CSS
[class^="btn-"] {
  font-weight: bold;
  border-radius: 4px;
}
```
```HTML
<button class="btn-success">Success</button>
<button class="btn-danger">Danger</button>
<button>Normal</button>
```

<br>

### 4. ATTR $= VALUE `[attr$=value]`  
속성 attr을 포함하며 속성 값이 value로 **끝나는** 요소 선택   

ex) class 명이 'success'으로 끝나는 요소만 선택하는 예제   


```CSS
[class^="btn-"] {
  font-weight: bold;
  border-radius: 4px;
}
[class$="success"] {
  color: green;
}
[class$="danger"] {
  color: red;
}
```
```HTML
<button class="btn-success">Success</button>
<button class="btn-danger">Danger</button>
<button>Normal</button>
```

<br><br><br><br>




## 상속

### 1. 상속

상위 요소에 적용된 속성이 하위 요소에도 적용됨

**<상속되는 속성들>**  
주로 글자와 관련된 내용이 상속됨!    
글자와 관련된 다음 속성들이 아닌 속성들은 상속이 안된다..!(기본적으로)  

- font
	- font-size &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\*글자 크기*/
	- font-weight &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\*글자 두께*/
	- font-style &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\*글자 기울기*/
	- line-height &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\*글자 줄 높이*/
	- font-family &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\*글자 폰트*/
- color &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\*글자 색상*/
- text-align &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\*글자 정렬*/
- text-indent &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\*글자 들여쓰기*/
- text-decoration
- letter-spacing
- opacity
- ...

<br>

	
### 2. 강제 상속

글자들을 다루는 속성을 제외하고 강제적으로 필요에 의해서 부모 요소가 가지고 있는 속성을 자녀 요소에게 강제적으로 상속하는 개념

ex) 강제 상속 예제

```CSS
.parent {
  position: absolute;  /* 상속되지 않는 속성과 값 */
}
.child {
  position: inherit;  /* 강제 상속 받아 position: absolute; 와 동일 */
}
```
```HTML
<div class="parent">
  <div class="child"></div>
</div>
```

상속되지 않는 속성(값)도 inherit이라는 값을 사용하여 '부모'에서 '자식'으로 강제 상속시킬 수 있음
   
'자식'를 제외한 '후손'에게는 적용되지 않으며, 모든 속성이 강제 상속을 사용할 수 있는 것은 아님!

<br><br><br><br>




## 우선순위

같은 요소에 여러 선언이 되어 있을 경우, 어떤 선언의 CSS 속성을 적용시킬지 (브라우져가) 결정하는 방법

<br>

### 1. 명시도
명시도 점수가 높은 선언이 우선
  
### 2. 선언 순서
명시도 점수가 같은 경우 가장 마지막에 해석된 선언이 우선
 
### 3. 중요도
명시도 점수는 '상속' 규칙보다 우선  
`!important` 가 적용된 선언 방식이 다른 모든 방식보다 우선  

<br>

### <점수>

- `!important`: 모든 선언을 무시하고 가장 우선(∞)
- 인라인 선언 방식 : 1000
- ID 선택자 : 100
- Class 선택자 : 10
- 태그 선택자 : 1
- 전체 선택자 : 0
- 상속 : X(상속은 점수 계산하지 않음)

<br>

### 점수 예시

```
.list li.item { color: red; }  /* 21pt */

.list li:hover { color: red; }  /* 21pt */

.box::before { content: "Good "; color: red; }  /* 11pt */

#submit span { color: red; }  /* 101pt */

header .menu li:nth-child(2) { color: red; }  /* 22pt */

h1 { color: red; }  /* 1pt */

:not(.box) { color: red; }  /* 10pt */

:not(span) { color: red; }  /* 1pt */ 
```

`:hover` 처럼 '가상 클래스'는 '클래스' 선택자의 점수(10pt)를 가지며,    
`::before` 처럼 '가상 요소'는 '태그' 선택자의 점수(1pt)를 가집니다.

부정 선택자 :not()은 점수를 가지지 않음

<br><br><br><br>


**참고한 블로그**

[heropy 블로그](https://heropy.blog/2019/04/24/html-css-starter/)   

[heropy 블로그_CSS개요](https://happy-noether-c87ffa.netlify.app/presentations/level1/css/summary/)

   

<br><br><br><br>

