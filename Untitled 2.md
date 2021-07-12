# 함수

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


