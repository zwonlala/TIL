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

Persion.prototype.getName = function() {
    return this._name;
}
```

위 예시를 보면, Person이라는 생성자 함수의 prototype에 getName이라는 메소드를 지정하였습니다.

그럼 Person의 인스턴스는 \_\_proto__ 프로퍼티를 통해 getName() 함수를 호출 할 수 있음

```javascript
var suzi = new Persion('Suzi');
suzi.__proto__.getName();    //undefined
```

<br>
<br>


Instance의 \_\_proto__ 가 Constructor의 prototype 프로퍼티를 참조하므로 둘은 같은 객체를 바라봄

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

그렇다면 원하는 결과를 얻기 위해 this를 Instance로 설정하는 방법은 \_\_proto__ 없이 인스턴스에서 바로 메소드를 사용하는 것입니다


```javascript
var suzi = new Persion('Suzi');
suzi.getName();    // Suzi

var iu = new Persion('Jieun');
iu.getName();      // Jieun
```

위와 같이 실행할 수 있는 이유는 바로 \_\_proto__ 생략 가능한 프로퍼티이기 때문입니다.

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

생성자 함수의 Prototype에 어떤 메소드나 프로퍼티가 있다면 인스턴스에서도 자신의 것 처럼 해당 메소드나 프로 퍼티를 접근 할 수 있게 됩니다.

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
실무에서 사용할 때는 Object.getPrototypeOf(instance), Refelect.getPrototypeOf(instance), Object.create()등을 이용하시기 바랍니다.


<br>
<br>
<br>






### constructor 프로퍼티

<br>
<br>
<br>
<br>
<br>
<br>

## 프로토타입 체인

### 메소드 오버라이드


### 프로토타입 체인

### 객체 전용 메소드의 예외사항


### 다중 프로토타입 체인


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
-> `__proto__` 프로퍼티는 생략이 가능하여 인스턴스에서 Constructor.prototype의 메소드를 자신의 메소드처럼 호출이 가능!   


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
