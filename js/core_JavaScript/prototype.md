# 06 프로토타입

## 프로로타입 개념 이해

### constructor, prototype, instance

```javascript
var instance = new Constructor();
```

위 문장을 나누어 설명하면

- 어떤 생성자 함수 `Constructor`를 `new` 연산자와 함께 호출하면
- `Constructor`에서 정의된 내용을 바탕으로 새로운 인스턴스 `instance`가 생성됨
- 이때 `instance`에는 **`__proto__`** 라는 프로퍼티가 자동으로 부여되는데
- 이 프로퍼티는 `Constructor`의 **`prototype`** 이라는 프로퍼티를 참조함

<br>
<br>


위에서 설명하는 `__proto__`, `prototype` 프로퍼티의 관계가 JS 프로토타입 개념의 핵심임


먼저 prototype은 객체이고, prototype을 참조하는 \_\_proto__ 역시 객체임

prototype 내부에는 인스턴스가 사용할 메소드를 저장함

그러면 인스턴스에서도 자동으로 생성된 \_\_proto__ 프로퍼티를 통해 prototype 내부에 저장한 메소드들을 사용할 수 있음

<br>
<br>


```javascript
var Person = function (name) {
    this._name = name;
};

Person.prototype.getName = function() {
    return this._name;
}
```

위 예시를 보면, Person이라는 생성자 함수의 prototype에 getName이라는 메소드를 지정하였습니다.

그럼 Person의 인스턴스는 \_\_proto__ 프로퍼티를 통해 getName() 함수를 호출 할 수 있음

```javascript
var suzi = new Person('Suzi');
suzi.__proto__.getName();    //undefined
```

<br>
<br>


instance의 \_\_proto__ 가 Constructor의 prototype 프로퍼티를 참조하므로 둘은 같은 객체를 바라봄

```javascript
Person.prototype === suzi.__proto__ 	//true
```

<br>
<br>


어떤 함수를 메소드로서 호출할 때는 메소드명 바로 앞의 객체가 this가 됩니다.

즉, `suzi.__proto__.getName();` 의 getName 함수 내부에서 this는 `suzi.__proto__`가 되고,   
`suzi.__proto__` 안에는 name 프로퍼티가 없으므로 undefined를 반환한 것입니다.

<br>
<br>

그렇다면 원하는 결과를 얻기 위해 this를 instance로 설정하는 방법은 \_\_proto__ 없이 인스턴스에서 바로 메소드를 사용하는 것입니다


```javascript
var suzi = new Person('Suzi');
suzi.getName();    // Suzi

var iu = new Person('Jieun');
iu.getName();      // Jieun
```

위와 같이 실행할 수 있는 이유는 바로 \_\_proto__가 생략 가능한 프로퍼티이기 때문입니다.

즉,

```javascript
suzi.__proto__.getName()
-> suzi(.__proto__.)getName()
-> suzi.getName()
```

JS는 함수에 자동으로 객체인 **`prototype`** 프로퍼티를 생성합니다.    

`new` 연산자와 함께 함수를 호출할 경우, 즉 해당 함수를 생성자 함수로서 사용할 경우,   
생성된 인스턴스에는 숨겨진 프로퍼티인 **`__proto__`** 가 자동으로 생성되며,    
이 프로퍼티는 생성자 함수의 **`prototype`** 프로퍼티를 참조함!   

위에서 설명한 대로  \_\_proto__은 생략 가능한 프로퍼티이기 때문에 

생성자 함수의 prototype에 어떤 메소드나 프로퍼티가 있다면 인스턴스에서도 자신의 것 처럼 해당 메소드나 프로 퍼티를 접근 할 수 있게 됩니다.

<br>
<br>

> - _tip_
>> \_\_proto__를 읽을 때는 'dunder proto'('던더 프로토') 라고 읽으면 됩니다.
dunder는 'double underscore'의 줄임말   

<br>
<br>

> - _tip_   
>> \_\_proto__ 와 [[prototype]]  
자바스크립트 명세에는 \_\_proto__가 아닌 [[prototype]]로 정의되어 있으며,   
\_\_proto__ 프로퍼티는 단지 브라우저에서 [[prototype]]을 구현한 대상이고 권장되는 방식이 아닙니다.   
이 문서에서는 이해하기 쉽게 하기 위하여 설명에 \_\_proto__ 프로퍼티를 사용하였으며,   
실무에서 사용할 때는 `Object.getPrototypeOf(instance)`, `Refelect.getPrototypeOf(instance)`, `Object.create()` 등을 이용하시기 바랍니다.   
참고 : ["프로토타입 상속" 문서 '__proto__는 [[Prototype]]용 getter·setter입니다.' 부분](https://ko.javascript.info/prototype-inheritance)


<br>
<br>
<br>






### constructor 프로퍼티

생성자 함수의 프로퍼티인 prototype 객체 내부에는 Constructor라는 프로퍼티가 있습니다.   
이 프로퍼티는 원래의 생성자 함수(자기 자신)를 참조함.  
인스턴스로부터 그 원형이 무엇인지 알 수 있는 수단이기 때문에 인스턴스와의 관계에 있어서 필요한 정보임

```javascript
var arr = [1, 2];

Array.prototype.constructor === Array	// true
arr.__proto__.constructor === Array 	// true
arr.constructor === Array

var arr2 = new arr.constructor(3, 4);
console.log(arr2);  // [3, 4]
```


<br>
<br>
<br>
<br>
<br>
<br>

## 프로토타입 체인

### 메소드 오버라이드

인스턴스에서 생성자 함수의 prototype 프로퍼티를 참조하는 \_\_proto__를 생략하면,   
인스턴스는 prototype에 정의된 프로퍼티나 메소드를 자신의 것 처럼 사용할 수 있다고 위에서 설명을 하였음

그럼 만약 인스턴스에서 동일한 이름의 프로퍼티나 메소드를 가지고 있는 상황이라면 어떨까요?


<br>
<br>


```javascript
var Person = function (name) {
  this.name = name;
};
Person.prototype.getName = function () {
  return this.name;
};

var iu = new Persion('지금');
iu.getName = function () {
  return '바로 ' + this.name;
};

console.log(iu.getName());	// 바로 지금
```

위 예제의 실행 결과를 보면, iu.\_\_proto__.getName이 아닌, iu 객체에 있는 getName 메소드가 호출되었음.   
이와 같은 현상을 '메소드 오버라이드'라고 함.

<br>
<br>

메소드 위에 메소드를 덮어 씌웠다는 표현으로, 원본을 제거하고 다른 대상으로 교체하는 것이 아닌 원본이 그대로 있는 상태에서 다른 대상을 그 위에 얹는 개념임

<br>
<br>

자바스크립트 엔진이 getName이라는 메소드를 찾는 방식은 먼저 실행 컨텍스트의 프로퍼티를 검색하고,
존재하지 않는 다면, \_\_proto__을 순차적으로 검색하는 순서로 진행합니다


<br>
<br>
<br>


### 프로토타입 체인

바로 위에서 메소드 오버라이드의 개념을 알아보았습니다.

그럼 다음 예제를 한번 살펴보겠습니다

```javascript
var arr = new Array(1, 2); //[1, 2]
arr.push(3); //[1, 2, 3]
arr.hasOwnProperty(2); // true
```

Array() 생성자 함수를 사용하여 배열을 하나 정의하고, 
push() 함수와 hasOwnProperty() 함수를 사용하였습니다.

<br>
<br>

`arr` 인스턴스에 `push()` 함수와 `hasOwnProperty()` 을 정의하지 않았지만, 위와 같이 사용할 수 있는 이유는 자바스크립트 엔진이 메소드를 찾는 방식이 프로퍼티를 검색하고, 없으면 그 다음으로 가까운 대상인 \_\_proto__를 검색하는 순서로 진행하기 때문입니다.


<br>
<br>


위 예제에서 `console.dir(arr);` 명령을 실행해보면 `push()` 함수와 `hasOwnProperty()` 함수가 어디에 정의되어 있는지 확인할 수 있습니다

![console.dir(arr)의 결과](https://user-images.githubusercontent.com/13375734/131215778-14d2fa75-2732-4fce-ac7f-f5b2da72e58f.png)
<br>
<br>

우리가 사용했던 함수들은 사실

```javascript
arr(.__proto__).push(3);
// arr.__proto__ === Array.prototype // true

arr(.__proto__)(.__proto__).hasOwnProperty();
// arr.__proto__.__proto__ === Object.prototype // true
```

위와 같이 Array.prototype에 정의된 `push()` 함수와
Object.prototype에 정의된 `hasOwnProperty()` 함수를 호출한 것입니다.

<br>
<br>

어떤 데이터의 \_\_proto__ 프로퍼티 내부에 다시 \_\_proto__ 프로퍼티가 연쇄적으로 이어진 것을 **`프로토타입 체인(prototype chain)`** 이라 하고,
이 체인을 따라가며 검색하는 것을 **`프로토타입 체이닝(prototype chaining)`** 이라고 합니다.


<br>
<br>
<br>


### 객체 전용 메소드의 예외사항

생략


<br>
<br>
<br>


### 다중 프로토타입 체인

생략

<br>
<br>
<br>
<br>
<br>
<br>


## 정리

어떤 생성자 함수를 `new` 키워드와 함께 호출   
-> `constructor`에 정의된 내용을 바탕으로 새로운 인스턴스가 생성    
-> 이 인스턴스에는 **`__proto__`** 라는 constructor의 **`prototype`** 프로퍼티를 참조하는 프로퍼티가 자동으로 부어됨    
-> **`__proto__`** 프로퍼티는 생략이 가능하여 인스턴스에서 Constructor.prototype의 메소드를 자신의 메소드처럼 호출이 가능!   


Constructor.prototype에는 constructor이라는 프로퍼티가 있는데, 생성자 함수 자신을 가리킴    
-> 인스턴스가 자의 생성자 함수가 무엇인지 알고자 할 때 필요한 수단   

Object.prototype은 모든 객체가 참조하고 있는 프로토타입이고,    
\_\_proto__ 방향으로 계속 찾아가는 과정을 **`프로토타입 체이닝`** 이라고 함

<br>
<br>
<br>
<br>
<br>
<br>
