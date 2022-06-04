[[Javascript] 비동기, Promise, async, await 확실하게 이해하기](https://elvanov.com/2597) 글을 읽고 정리한 문서


## 함수

함수는 정의한다고 실행되지 않음.   
함수가 호출되어야 함수의 내용이 실행됨.

JS 는 함수를 변수처럼 이용 가능.

a 함수를 호출할때 b 함수를 전달하는 것.  
=> "콜백 함수를 전달한다"

<br> 
<br> 


## 비동기

`동시에 여러 작업을 할 수 있다!`

<br> 

### * setTimeout()

1. setTimeout()은 인자로 들어온 콜백함수를 예약하기만 하고 바로 끝남   
(호출 스택에서 비워짐)
2. setTimeout()에 의해 기다리는 동작은 본래 코드 흐름과는 상관없이 따로따로 독립적으로 돌아감   
(아래 사진 처럼 3개 동시에 기다리는 모습)
3. 이렇게 따로따로 독립적으로 돌아가는 작업을 비동기라고 함
![setTimeout 예시](https://i0.wp.com/elvanov.com/elvanov/wp-content/uploads/2021/07/IMG_0368.jpeg?resize=1536%2C992&ssl=1)

<br> 

- `동기`의 대략적인 특징
	- 동시에 여러 작업을 수행할 수 **_없다_**
	- 한 순간에 한 가지 일만하니 **_흐름을 예측하기 쉽고_**
	- 먼저 수행되고 후에 수행되는 것이 **_명확함_**

- `비동기`의 대략적인 특징
	- 동시에 여러 작업을 수행할 수 **_있다_**
	- **_흐름을 예측하기 어렵다_**
		- 위 setTimeout() 예시에서,    
인자로 소요되는 시간이 제공되니 3 2 1 순으로 실행되는 것을 알지만,    
얼마의 시간이 소요될지 모르는 api 요청 등이었다면    
1, 2, 3 중 어떤 게 먼저 올지 모르는 일

<br> 

### 비동기 작업 예시

- AJAX (XMLHttpRequest 객체를 활용한 비동기적 요청)
- Fetch API
- File IO


<br> 

### 문제점

여러 작업을 동시에 수행할 수 있는 장점은 있으나,   
의존성이 길게 이어져 있는 비동기 작업을 처리하기엔 애매할 수 있음.  
- _비동기 작업이 시작되는 시점은 함수 호출이며, 이 함수 호출 시점에 다음 작업(콜백함수)도 넘겨줘야 하기 때문 ???_
- 콜백 지옥

<br> 
<br> 

## Promise

Promise 는 비동기 작업의 단위


### 기본 사용법

```
const promise1 = new Promise((resolve, reject) => {
	// 비동기 작업
});
```

1. promise1 이라는 상수를 선언. (하나의 이름으로 끝까지 해당 Promise를 관리하는 것이 가독성도 좋고 유지보수 하기 좋음)
2. new Promise() 로 Promise 객체를 새롭게 만듦
3. Promise 생성자는 특별한 함수 하나를 인자로 받음. 이 특별한 함수를 executor라는 이름으로 부름.


executor 함수 설명

- executor의 첫번째 인자는 `resolve`이고, 두번째 인자는 `reject`임.(국룰)
- `resolve`는 executor 함수 내에서 호출할 수 있는 또 다른 함수. `resolve`가 호출되면, "이 비동기 작업이 성공했어" 라는 뜻
- `reject`는 executor 함수 내에서 호출할 수 있는 또 다른 함수. `reject`가 호출되면, "이 비동기 작업이 실패했어" 라는 뜻


Promise 의 특징
- `new Promise(...)` 하는 순간 할당된 비동기 작업은 바로 시작.
- 비동기 작업의 특징은 작업이 언제 끝날지 모르니 일단 배를 떠나보낸다.
	- 그 이후에 작업이 성공/실패 하는 순간에 뒷 처리를 해줘야 함.
	- Promise가 끝난 후의 동작을 설정하는 방법은 `then()`메소드와 `catch()`메소드

- `then()`메소드   
해당 Promise가 성공했을 때의 동작을 지정함   
인자로 함수 받음  
체인 형태로 활용 가능  

- `catch()`메소드  
해당 Promise가 실패했을 때의 동작을 지정함    
인자로 함수 받음   
체인 형태로 활용 가능  


```js
const promise1 = new Promise((resolve, reject) => {
  resolve();
});
promise1
  .then(() => {
    console.log("then!");
  })
  .catch(() => {
    console.log("catch!");
  });

// then!
```


### 재사용하기

new Promise(...) 를 하는 순간 비동기 작업이 시작되는데, 비슷한 비동기 작업을 수행할 때마다 매번 new Promise(...) 를 해줘야 하나?

Nope.

그냥 new Promise(...) 한 것을 그대로 리턴하는 함수를 만들어 사용하면 됨.


```js
function startAsync(age) {
  return new Promise((resolve, reject) => {
    if (age > 20) resolve();
    else reject();
  });
}

setTimeout(() => {
  const promise1 = startAsync(25);
  promise1
    .then(() => {
      console.log("1 then!");
    })
    .catch(() => {
      console.log("1 catch!");
    });
  const promise2 = startAsync(15);
  promise2
    .then(() => {
      console.log("2 then!");
    })
    .catch(() => {
      console.log("2 catch!");
    });
}, 1000);
```

위 예제에서 startAsync 함수를 호출하는 순간 new Promise(...) 가 실행하게 되어 비동기 작업이 시작됨.


### executor 함수 주의사항

- executor 함수 내부에서 Error throw 된다면 해당 Error 로 reject가 수행됨
- executor 함수의 리턴값을 무시됨
- 첫번째로 호출되는 resolve 함수 혹은 reject 함수만 유효함


### Promise 의 세가지 상태

- **대기**(pending)
- **이행**(fulfilled)
	- then() 함수로 등록한 동작들이 실행됨
- **거부**(rejected)
	- catch() 함수로 등록한 동작들이 실행됨


### Promise의 의의

> 비동기 작업을 생성/시작하는 부분 `new Promise(~)`과   
작업 이후의 동작을 정의(지정)한 부분 `then`,`catch` 을 분리함으로서,   
기존의 러프한? callback으로 구성되어 있는? 비동기 작업보다 유연한 설계를 가능하게 함


### Promise 요약

- Promise 객체를 생성하는 순간 비동기 작업이 시작됨.
- 비동기 작업이 성공으로 간주되고 싶을때 resolve를 호출하고,   
실패라고 간주하고 싶으면 reject 함수를 호출한다
- 비동기 작업이 성공했을때 후속 조치를 지정하고 싶으면 then으로,   
실패시의 후속 조치는 catch로 지정하면 됨

<br> 
<br> 

## async : `비동기 작업을 만드는 손쉬운 방법`

async 키워드는 함수를 선언할때 붙여줄 수 있는 키워드

async 함수의 리턴 값은 무조건 Promise 객체 !


### new Promise(...)를 리턴하는 함수를 async 함수로 변환하기

- 함수에 async 키워드를 붙인다.
- new Promise(...) 부분을 없애고, executor 함수의 바디? 본문? 내용만 남김
- resolve(value); 부분을  return value;로 변경
- reject(new Error(...)); 부분을  throw new Error(...); 로 수정


```js
// 기존
function startAsync(age) {
  return new Promise((resolve, reject) => {
    if (age > 20) { 
      resolve(`${age} success`);    
    } else { 
      reject(new Error("Something went wrong"));
    }
  });
}


// async 함수
async function startAsync(age) {
  if (age > 20) {
    return `${age} success`;
  } else {
    throw new Error(`${age} is not over 20`);
  }
}
```

원래라면, async 함수를 실행시킨 다음 then과 catch를 사용하여 흐름을 제어해야 함.

하지만 await 키워드를 사용하면 조금더 코드를 직관적으로 구현 가능함

<br> 
<br> 

## await : `Promise 작업이 끝날 때까지 기다려!`

await 는 Promise 가 fulfilled 가 되든지 rejected 가 되든지 간에 끝날 때까지 기다리도록 하는 연산자.

- async 함수에서만 사용할 수 있다


<br> 
<br> 

## Promise.all : `여러 비동기 동작을 한꺼번에 기다리기`

- Promise.al() 함수는  
인자로 Promise 의 배열을 받으며, 하나의 특별한 Promise 를 새로 생성
- 이 Promise는 배열로 받은 모든 비동기 작업이 성공했다면 내부적으로 resolve 를 호출,   
하나라도 비동기 작업이 실패한다면 reject 를 호출합니다.



