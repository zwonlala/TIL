이 문서는 fastcampus javascript 강의를 듣고 정리한 문서입니다


# JS란?

# Various JS Runtime

# Expression Statement

# Keywords, Reserved Words

# Identifier

# Comments

# 변수와 상수

# 변수의 유효범위

# var과 호이스팅

# 자료형

# 조건문

# 반복문

# 함수

- 선언적 함수를 만드는 방식

function hello() {}

함수를 만들 때 사용하는 키워드
가장 고전적인 방법


```javascript
function hello1() {
  console.log('hello1');
}

console.log(hello1, typeof hello1); //[Function: hello1] 'function'

//타입은 문자열로 'function'이라고 나온다
//기본 자료형을 배울때 'function'이라는 자료형을 배운 적 없음
// -> 이게 나왔다는 건, 객체 중에 하나라는 것('표준 내장 객체'라고 함)
// => 즉, 함수도 객체의 한 종류라는 것!
```


- 익명 함수
const hello = function() {}

위와 같이 function이라는 키워드를 사용하여 함수를 만드는데,
function이라는 키워드 바로 다음에 '함수 이름'이 나온 게 아니라
함수 이름 없이 함수를 만든 다음 결과물을 특정 변수에 담아두는 것

```javascript
const hello1 = function() {
  console.log('hello1');
}

console.log(hello1, typeof hello1); //[Function: hello1] 'function'

//위의 경우와 동일하게 출력!!!
```


- '선언적 function'과 '익명 함수를 만들어 변수에 할당하는 방법'의 차이

선언적 함수를 만드는 방식은,
함수를 정의하는 부분 전에 사용하는 부분이 나와도 가능!

```javascript
function hello1() {
  console.log('hello1');
}

hello1(); //가능. 당근🥕
```  

```javascript
hello1(); //이것도 가능함!!! 😳

function hello1() {
  console.log('hello1');
}
```  


익명함수를 만드는 방식으로 위 예제를 실행하면

```javascript
var hello2 = function() {
  console.log('hello2');
}

hello2(); //'hello2' 출력
```  

```javascript
hello2(); //'TypeError: hello2 is not a function...' 에러남..!

var hello2 = function() {
  console.log('hello2');
}
```  

위 현상은 전에 배운 호이스팅 개념으로 설명할 수 있다!

바로 위 예제에서 제일 첫번째 줄에 console.log(hello2);를 실행하면

```javascript
console.log(hello2); //'undefined'

hello2(); //'TypeError: hello2 is not a function...' 에러남..!

var hello2 = function() {
  console.log('hello2');
}
```  
undefined가 출력됨.

즉,

```javascript
var hello2;
console.log(hello2); //'undefined'

...

hello2 = function() {
  console.log('hello2');
}
```
이렇게 실행되고 있던것!!

hello2가 뭔진 알지만?(defined는 되었지만) 이게 함수가 아니고 undefined 상태이므로,
이걸 함수처럼 쓰려고 하니 타입 에러가 나는 것임!!!




그럼 바로위에서 본 예제를 var 키워드가 아닌 const 키워드로 사용하면 어떨까?

```javascript
hello2(); //'ReferenceError: hello3 is not defined...' 에러남..!

const hello2 = function() {
  console.log('hello2');
}

hello2(); //가능. 당근🥕
```  
이번에도 에러가 발생하긴 했는데, 발생한 에러의 종류가 다른다!

ReferenceError, 즉 hello2가 뭔지 아예모르고 있는 것!!!(undefined조차도 아닌, 선언한 적이 없다고 생각해서 에러가 남)


> ∴ 즉 선언적 방식으로 function 키워드를 사용하여 함수를 정의하면, JS 특성상 함수를 먼저 메모리에 올림! 
>
> 따라서 코드의 위치상 함수의 정의보다 먼저 사용한다 하더라도, 문제없이 돌아가는 것!!!!














```javascript

```




# 객체

# 클래스

# Promise

# Async / Await


  