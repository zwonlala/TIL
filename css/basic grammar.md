<h1 style="display: inline-block; line-height:0pt; margin:10px padding:10px">CSS</h1>

<details>
<summary ><b style="font-size: 25px">목차</b></summary>

<ol>

## <li>선언방식</li>
## <li>기본 선택자</li>
## <li>복합 선택자</li>
## <li>가상 클래스 선택자</li>
## <li>가상 요소 선택자</li>
## <li>속성 선택자</li>
## <li>상속</li>
## <li>우선순위</li>


</ol>
</details>
<br>


## 선언방식
- 콜론 세미콜론이 한 세트!

```
선택자 {
  속성: 속성값;
  속성: 속성값;
}
```

선택자는 속성과 속성값을 지정할 대상을 검색하는 역할

주석의 경우 `/* ~~ */` 사용가능 
`//` 사용 가능한지...?


1. in-line 방식
태그에 직접 작성하는 방법
태그 안에 style 속성에 문자열로 css 값을 설정
선택자가 필요 없음
**~~하기 때문에 비추하는 방법!**
`<div style="color: red;">태그에 직접 작성하는 inline 방식</div>`

2. embedded 방식
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

3. link 방식

CSS 파일로 정의하여 사용하는 방법
가장 일반적인 방식
HTML에 \<head> 태그에 \<link> 태그를 삽입하여 사용

```
<link rel="stylesheet" href="/css/main.css">
```

4. import 방식

`@import`를 사용하여 외부 문서로 CSS를 불러와 적용하는 방식

```HTML
<head>
  <link rel="stylesheet" href="css/common1.css">
</head>
<body>
  <div>HELLO</div>
</body
```

```CSS
//common1.css
@import url("./common2.css");
```

```CSS
//common2.css
div {
  color: red;
  font-size: 20px;
  font-weight: bold;
}
```

주의할 점!

link 방식으로 여러 CSS 파일을 불러오면 파일들을 병렬적으로 불러와 시간이 단축되지만,
import 방식으로 여러 CSS 파일을 불러오면, 파일들이 순차적으로(직렬적으로?) 불러와져 로딩 시간이 오래 걸릴 수 있다

## 기본 선택자

1. 전체 `*`

모든 태그를 다 선택하는 것
(요소 내부의) 모든 요소를 선택

2. 태그 `E`

선택자를 입력하는 부분에 적용하려는 태그의 이름을 입력
태그 이름이 E 인 요소 선택

3. 클래스 `.CLASS_NAME`

선택자를 입력하는 부분에 적용하려는 클래스 이름에 온점(`.`)을 붙여 사용
HTML class 속성의 값이 CLASS_NAME인 요소 선택

4. id `#ID`

HTML id 속성의 값이 ID 인 요소 선택










## 복합 선택자

1. 일치 선택자(Basic Combinator) `EF`
E와 F를 동시에 만족하는 요소 선택

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

2. 자식 선택자(Child Combinator) `E > F`
`E`의 자식 요소 `F`를 선택
여기서 자식이란 바로 다이렉트 아래를 의미함!

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

3. 후손(하위) 선택자(Descendant Combinator) `E F`
`E`의 후손(하위)요소 `F`를 선택

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



4. 인접 형제 선택자(Adjacent Sibling Combinator) `E + F`
`E`의 다음 형제 요소 `F` 하나만 선택

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

5. 일반 형제 선택자(General Sibling Combinator) `E ~ F`
`E`의 다음 형제 요소 `F` 모두 선택

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

 
## 가상 클래스 선택자(Pseudo-Classes Selectors)

송지원 여기 설명 다시 적기 
특징이라

- 문법 :
1. hover `E:hover`  
`E`에 마우스(포인터)가 올라가 있는 동안에만 `E` 선택


ex)a 태그 마우스 올리면 글자 색상 바뀌는 예제

```CSS
a:hover {
  color: red;
}
```
```HTML
<a href="http://www.naver.com">NAVER</a>
```



2. active `E:active`   
`E`를 마우스로 클릭하는 동안에만 `E` 선택


ex)마우스로 div 태그 눌렀을 때만 가로 길이 2배 늘어나는 예제
(+transition 속성 추가하여 전환이 부드러워 짐)

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



3. focus `E:focus`  
`E`가 포커스 된 동안에만 `E` 선택
대화형 콘텐츠에서 사용 가능
https://developer.mozilla.org/ko/docs/Web/Guide/HTML/Content_categories#%EB%8C%80%ED%99%94%ED%98%95_%EC%BD%98%ED%85%90%EC%B8%A0


ex)

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


4. first-child `E:first-child`  
`E`가 형제 요소 중 첫번째 요소라면 선택

ex)

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


5. last-child `E:last-child`  
`E`가 형제 요소 중 마지막 요소라면 선택

ex)

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

6. nth-child `E:nth-child(n)`
`E`가 형제 요소 중 n번째 요소라면 선택
(n 키워스 사용시, n에 0부터 대입하여 적용 && 요소는 1번째 부터 카운트!)


ex)

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


ex)짝수 번째 요소들만 선택하는 예제

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


ex)3번째 요소 이후부터 선택하는 예제

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




7. xxx-child 주의사항 

ex)예상과 달리 잘 적용되지 않는 예제

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
.fruits의 첫번째 자식 요소가 <p> 태그가 아니기 때문에 선택되지 않습니다.
@송지원 내 부연 설명 적기


8. nth of type `E:nth-of-type(n)`
`E`의 타입(태그이름)과 동일한 타입인 형제 요소 중 `E`가 n번째 요소라면 선택
(n 키워스 사용시, n에 0부터 대입하여 적용 && 요소는 1번째 부터 카운트!)


ex)

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
<p></p>들 중에서 첫번째 요소를 선택합니다.



ex)

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
2번째와 4번째에 있는 .red 요소의 타입(태그이름)은 li 이기 때문에, :nth-of-type(1) 선택자는 <li></li>들 중에서 첫번째 요소를 선택하고 .red 인지 체크하게 됩니다.
따라서 조건에 맞는 요소가 없으므로 선택되지 않습니다.




9. 부정 선택자 NOT `E:not(S)`  
`S`가 아닌 `E` 선택

ex)

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






## 가상 요소 선택자

Pseudo-Element Selectors


- 문법 : 
1. before `E::before`  
E 요소 내부의 앞에, 내용을 삽입!

ex)

```CSS
ul li:before { /* support IE 8 */
  content: "$";
}
ul li::before {
  content: "$";
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

각 <li></li> 내부의 앞에 내용(content)으로 $ 문자를 삽입했습니다.
내용을 넣기 위해서는 content 속성이 필수입니다.

content 속성이 없으면 아무것도 적용 안됨


ex)

```CSS
div::before {
  content: url("../images/smile.png");
}
```

url()을 통해서 이미지를 삽입할 수 있습니다.


2. after `E::after`  
E 요소 **내부의 뒤**에, 내용을 삽입!

ex)

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

각 <li></li> 내부의 뒤에 내용(content)으로 .0 문자를 삽입했습니다.






ex)

```CSS

```
```HTML

```



## 속성 선택자

1. [ATTR] `[attr]`
속성 attr을 포함한 요소 선택

ex)

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
2. ATTR = VALUE `[attr=value]`
속성 attr을 포함하며 속성 값이 value인 요소 선택

ex)

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


3. ATTR ^= VALUE `[attr^=value]`
속성 attr을 포함하며 속성 값이 value로 시작하는 요소 선택

ex)

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

4. ATTR $= VALUE `[attr$=value]`  
속성 attr을 포함하며 속성 값이 value로 끝나는 요소 선택
ex)

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

## 상속

1. 상속

상위 요소에 적용된 속성이 하위 요소에도 적용됨

상속되는 속성들
- font
	- font-style
	- font-weight
	- font-size
	- line-height
	- font-family
- color
- text-align
- text-indent
- text-decoration
- letter-spacing
- opacity
- ...



	
2. 강제 상속

ex)

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

상속되지 않는 속성(값)도 inherit이라는 값을 사용하여 '부모'에서 '자식'으로 강제 상속시킬 수 있습니다. '자식'를 제외한 '후손'에게는 적용되지 않으며, 모든 속성이 강제 상속을 사용할 수 있는 것은 아닙니다.

## 우선순위

같은 요소에 여러 선언이 되어 있을 경우, 어떤 선언의 CSS 속성을 적용시킬지 결정하는 방법

1. 명시도
명시도 점수가 높은 선언이 우선
2. 선언 순서
명시도 점수가 같은 경우 가장 마지막에 해석된 선언이 우선
3. 중요도
명시도 점수는 '상속' 규칙보다 우선
`!important` 가 적용된 선언 방식이 다른 모든 방식보다 우선



점수
 - `!important`: 모든 선언을 무시하고 가장 우선(∞)
 - 인라인 선언 방식 : 1000
- ID 선택자 : 100
- Class 선택자 : 10
- 태그 선택자 : 1
- 전체 선택자 : 0
- 상속 : X(상속은 점수 계산하지 않음)


점수 예시

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

:hover 처럼 '가상 클래스'는 '클래스' 선택자의 점수(10pt)를 가지며, ::before 처럼 '가상 요소'는 '태그' 선택자의 점수(1pt)를 가집니다.
부정 선택자 :not()은 점수를 가지지 않습니다.



https://happy-noether-c87ffa.netlify.app/presentations/level1/css/summary/