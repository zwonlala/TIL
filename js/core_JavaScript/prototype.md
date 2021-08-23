# 06 프로토타입

## 프로로타입 개념 이해

### constructor, prototype, instance

### constructor 프로퍼티




## 프로토타입 체인

### 메소드 오버라이드


### 프로토타입 체인

### 객체 전용 메소드의 예외사항


### 다중 프로토타입 체인

## 정리

어떤 생성자 함수를 new 키워드와 함께 호출
-> constructor에 정의된 내용을 바탕으로 새로운 인스턴스가 생성
-> 이 인스턴스에는 \__proto__라는 constructor의 prototype 프로퍼티를 참조하는 프로퍼티가 자동으로 부어됨
-> \__proto__ 프로퍼티는 생략이 가능하여 인스턴스에서 Constructor.prototype의 메소드를 자신의 메소드 처럼 호출이 가능!


Constructor.prototype에는 constructor이라는 프로퍼티가 있는데, 생성자 함수 자신을 가리킴
-> 인스턴스가 자의 생성자 함수가 무엇인지 알고자 할때 필요한 수단

Object.prototype은 모든 객체가 참조하고 있는 프로토타입이고,
\__proto__ 방향으로 계속 찾ㅇ가는 과정을 프로토타입 체이닝이라고 함