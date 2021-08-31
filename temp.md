for jwSong
-----
- [X] [Learning JavaScript] 도서 9.2.3 프로토타입 파트 -> 읽어봤는데 잘 와닫지 않음. 나중에 다시 읽어보기.
- [X] [Notion JS 스터디](https://www.notion.so/2-prototype-ab56849772574304b93b6e1d57f7b527)
- [ ] [MDN 'Object prototypes' 문서](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Object_prototypes)
- [ ] [MDN '상속과 프로토타입' 문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
- [ ] [Poiemaweb 'Prototype' 문서](https://poiemaweb.com/js-prototype)

- [ ] [medium '[Javascript] 프로토타입 이해하기' 블로그 글](https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67)
1. - [ ] [넥스트리 'JavaScript: 프로토타입(prototype) 이해'](https://www.nextree.co.kr/p7323/)
- [ ] [velog '자바스크립트 Prototype 완벽 정리' 블로그 글](https://velog.io/@adam2/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Prototype-%EC%99%84%EB%B2%BD-%EC%A0%95%EB%A6%AC)
----



---
title: Prototype
---

# Prototype

말해야 할 키워드 : 프로토 타입, 프로토타입 체이닝, prototype에서의 this



# 프로토타입 체인

## 프로토타입 체인과 프로토타입 체이닝

## 자바스크립트 내장함수



자바스크립트는 프로토타입 기반 언어(prototype-based language)입니다. 모든 자바스크립트 객체들은 메소드와 속성들을 상속 받기 위한 템플릿으로 프로토타입 객체(prototype object)를 가진다는 의미입니다. 
프로토타입 기반 언어에서는 어떤 객체를 원형(prototype)으로 삼고 이를 참조함으로써 상속과 비슷한 효과를 얻습니다.
다음의 간단한 예제를 보며 무슨 의미인지 알아가보도록 하겠습니다.
자바스크립트의 프로토타입을 이해하기 위해서는 prototype 프로퍼티를 우선 이해해야 합니다. 간단한 예제로 시작해보겠습니다.


지금 보고계신 브라우저의 개발자 모드에서 간단한 object를 정의한 후 출력해보면 다음 화면과 같이 나올 것입니다. 이번엔 간단한 Array를 정의한 후 출력해보면 다음 화면과 같이 나올 것 입니다. 출력된 결과를 보면, toString, forEach, map, pop 과 같은 익숙한 함수들이 보입니다. 저희는 해당 함수를 정의하지 않았는데 그럼 어디에 해당 함수들이 정의되어 있고, 어떻게 해당 함수들을 쓸 수 있는 걸까요?

바로 위 예제에서 사용한 예제를 다르게 표현하면 다음의 new 키워드를 사용하는 문장과 동일합니다.
```js
// var simpleArray = [];
var simpleArray = new Array();
```

위 문장을 실행하면 일어나는 일을 순서대로 설명하면

1. 생성자 함수 Array를 new 키워드와 함께 호출하면
2. 함수 Array에 정의된 내용을 바탕으로 새로운 인스턴스 simpleArray가 생성됩니다.
3. 이때 생성된 인스턴스인 simpleArray에는 __proto__ 라는 프로퍼티가 자동으로 부여되는데
4. __proto__ 프로퍼티는 생성자함수 Array의 prototype 프로퍼티를 참조합니다.

즉 우리가 맨 처음 봤던 예제에서 봤던 toString, forEach, map, pop과 같은 함수들은 Array.prototype에 정의되어 있고, simpleArray 인스턴스에서 참조를 하고 있던 것 입니다.


```js
Array.prototype === simpleArray.__proto__; //true 
```

위 예제에서 알아본 __ㅔ개새__ 와 prototype 프로퍼티의 관계가 바로 자바스크립트 프로토타입 개념의 핵심입니다.

protype 의 타입은 객체이고, prototype을 참조하는__proto__또한 객체입니다.

prototype 내부에는 인스턴스가 사용할 메소드를 저장합니다.
그럼 인스턴스에서 자동으로 __proto__ 프로퍼티를 통해 protype 내부에 정의된 메소드들을 사용할 수 있습니다.


다음으로 prototype 프로퍼티를 직접 사용는 예제를 통해 prototype 프로퍼티를 더 이해해보겠습니다

```js
function Person (name) {
  this.name = name;
}

Person.prototype.printName = function() {
	console.log(this.name);
}
```

위 코드를 보면 Person이라는 생성자 함수의 prototype에 printName이라는 메소드를 지정하였습니다.
그럼 Person의 인스턴스는 __proto__ 프로퍼티를 통해 printName 함수를 호출할 수 있습니다.

```js
// ...

var ironMan = new Person('Tony Stark');
ironMan.__proto__.printName();	// undefined
```

위 예제를 보면 우리가 설정한 이름인 'Tony Stark'가 아닌 undefined를 출력합니다. 메소드를 출력할때는 메소드 바로 앞의 객체가 this가 되는데, ironMan.__proto__ 에는 name이라는 프로퍼티가 존재하지 않아 undefined가 출력된 것 입니다.

 그럼 우리가 설정한 이름을 출력하려면 어떻게 해야할까요?
원하는 결과를 얻기위해 this를 ironMan 인스턴스로 설정하는 방법은 __proto__ 없이 인스턴스에서 바로 메소드를 사용하는 것입니다.


```js
// ...

var ironMan = new Person('Tony Stark');
ironMan.printName();	// Tony Stark

var captainAmerica = new Person('Steve Rogers');
captainAmerica.printName();	// Steve Rogers
```

위와 같이 실행할 수 있는 이유는 __proto__ 프로퍼티가 생략 가능한 프로퍼티이기 때문입니다.
즉,
```js
captainAmerica.__proto__.printName()
-> captainAmerica(.__proto__.)printName()
-> captainAmerica.printName()
```




