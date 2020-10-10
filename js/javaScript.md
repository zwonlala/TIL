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






- 생성자 함수로 만드는 방법

const hello = new Function();

- function 과 new Function() 차이점
...생략 송지원 https://www.fastcampus.co.kr/courses/200543/clips/# 00~57 다시 정리

- arrow function
() => {}

es6에 새로 생긴 문법


```javascript
//arrow function를 만들어 이름이 hello1인 변수에 할당

const hello1 = () => {
  console.log('hello1');
}
//함수를 만들어서 변수에 넣어주는 형태!
//선언적 방식으로는 쓸 수 없음(항상 익명함수!)



/* 함수의 매개변수 */
//매개변수가 하나일 때, 괄호 생략 가능

const hello2 = (name) => { //일반적인 표현
  console.log('hello2', name);
}

const hello2 = name => { //이런 방식도 사용 가능!
  console.log('hello2', name);
}

const hello3 = (name, age) => { //매개변수가 2개 이상일땐, 항상 괄호 사용해야 함!
  console.log('hello2', name, age);
}



/* 함수의 리턴 */

const hello4 = name => {
  return `hello4 ${name}`;
};

const hello4 = name => `hello5 ${name}`; //이렇게 간략하게 표현 가능.
//만약 함수 바디에 리턴 문 말고 다른 로직이 있다면 중괄호 사용해야 함!
```





- new 함수();

함수를 new 라는 키워드 사용하여 객체를 생성하는 데 사용할 수 있다.

새로운 객체를 만들어 갈때 function이라는 키워드를 사용하여 틀을 만들고

new를 사용하여 하나의 인스턴스, 객체를 만들 수 있는 기능이 있음

```javascript
// 생성자 함수를 이용하여 새로운 객체를 만들어 내는 방법

function Person(name, age) {
  this.name = name;
  this.age = age;
}

const a = new Person('jw', 26);
console.log(a, a.name, a.age); //'Person { name: 'jw', age: 26} 'jw' 26'

const b = new Person('hg', 23);
console.log(b, b.name, b.age); //'Person { name: 'hg', age: 23} 'hg' 23'
```

위와 같이 만들 수 있는 이유는 Person이라는 function이 함수 내에서 this 라는 context를 만들기 때문

```javascript
function Person(name, age) {
  console.log(this); //'Person {}'
  this.name = name;
  this.age = age;
}
```

this가 하는 역할이 객체가 만들어졌을때, 그 객체를 가리키는 그런 역할을 함




반면 arrow function 같은 경우는 함수 내에 this 라는 context 만들어 지지 않음 

```javascript
const Cat = (name, age) => {
  this.name = name;
  this.age = age;
}

const c = new Cat('cat', 2); //'TypeError: Cat is not a constructor...'
```

Cat() 함수 내에 this라는 것을 가지고 있지 않기 때문에 TypeError 남!

∴ 모든 생성자 함수로 사용되는 함수는 function 키워드를 사용하는 함수!



- 함수 안에서 함수를 만들어 리턴

...생략 송지원 [05:00 ~ 07:40]다시 정리



- 함수를 호출할 때, 인자로 함수를 사용

```javascript
function hello(c) {
  console.log('hello');
  c();
}

hello(function() {
  console.log("콜백");
});
//`hello
//콜백` 
```


```javascript

```




# 객체

# 클래스

# Promise

# Async / Await


  