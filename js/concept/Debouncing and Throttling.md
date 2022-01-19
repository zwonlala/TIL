## 디바운싱(Debouncing)과 쓰로틀링(Throttling)


비제어 컴포넌트, 제어 컴포넌트에 대해 react 공식 문서를 읽던 중 잘 이해가 되지 않아,    
해당 내용을 구글링하여 [이 블로그 글 "React: 제어 컴포넌트와 비제어 컴포넌트의 차이점👍"](https://velog.io/@yukyung/React-%EC%A0%9C%EC%96%B4-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%99%80-%EB%B9%84%EC%A0%9C%EC%96%B4-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90-%ED%86%BA%EC%95%84%EB%B3%B4%EA%B8%B0)을 보게 됨   


내용이 잘 정리되어 있어 SSG~ SSG~ 잘 읽다가,
 
"제어 컴포넌트를 사용할 때 문제점" 부분에서 불필요한 갱신을 막기위해    
**"스로틀링이나 디바운싱 (throttle&debounce)을 사용할 수 있다."** 라고 나와 있었음
 

우선 위 개념을 잘 몰라서 여러 글을 참고하여 이해를 함.

<br>
<br>
<br>

#### 참고한 글 목록

- [zerocho 블로그 "쓰로틀링과 디바운싱"](https://www.zerocho.com/category/JavaScript/post/59a8e9cb15ac0000182794fa)
- [개발자 아저씨들 힘을 모아 "[JS] 디바운싱(Debouncing)과 쓰로틀링(Throttling)"](https://programming119.tistory.com/241)
  - 언어적 의미를 잘 설명해줌 👍


<br>
<br>
<br>

### 디바운싱(Debouncing)

우선 `bouncing`의 뜻은 
```
[전자] 스위치들이 접점에서 떨어지거나 붙는 시점에 물리적으로 미세하게 여러번의 ON/OFF 가 되는 현상
```

임

![bouncing](https://i0.wp.com/embedds.com/wp-content/uploads/2013/08/button_bounce.jpeg?ssl=1)


근데 해당 현상이 의도하지 않은 현상이니, 해당 현상을 수정? 발생하지 않게 해야했고

이런 불필요한 ON/OFF 들을 방지하는게 `debouncing` 이다.


그런데 이런 개념? 처리가 전자에만 있는게 아니라 CS 쪽에도 존재함

Ex)
- ajax 요청을 보낼때, input 이벤트에 해당하는 e.target.value 값을 바뀔때마다 보내는게 아닌 입력이 종료된 후에 보내기

<br>


**```즉, 계속해서 요청을 들어올 때, 모든 요청을 처리하지 않고 요청을 그룹으로 묶어 하나로 처리하는 것임!```**

<br>
<br>

예시 코드
<details> 
<summary>zerocho debouncing 예시</summary>

```js
//텍스트 입력이 완료되었을 때만 ajax 요청(console.log) 하게 하는 코드
// -> 텍스트 입력이 완료되고 200ms가 지나야지만 console.log() 실행

var timer;
document.querySelector('#input').addEventListener('input', function(e) {
  if (timer) {
    clearTimeout(timer);
  }
  timer = setTimeout(function() {
    console.log('여기에 ajax 요청', e.target.value);
  }, 200);
});
```
</details>

<details> 
<summary>개발자 아저씨들 힘을모아 debouncing 예시</summary>

```js
// 마우스 스크롤이 끝났을때만 숫자를 1 증가시켜 출력하는 예제
// -> 마우스 스크롤이 완료되고 300ms가 지나야지만 count 값을 1 증가시킴
//    300ms가 지나기 전에 다음 이벤트가 발생하면, 이전 이벤트에 기록된 debounce를 지우고 다시 debouncer를 설정
//    결과적으로 마지막에 발생한 이벤트에 대해서만 300ms가 지난 후 이벤트 콜백함수가 호출 

var debouncer;

window.addEventListener('scroll', function (e) {
    if (debouncer) {
        clearTimeout(debouncer);
    } 
    
    debouncer = setTimeout(function() {
        console.log('스크롤 이벤트 발생!');
        const count = document.getElementById('count');
        count.innerText = parseInt(count.innerText) + 1 
    }, 300); 
})
```
</details>


<br>
<br>
<br>
<br>

### 쓰로틀링(Throttling)

사전에 찾아보면 뜻이 '목을 조르다', '압력 조절' 이렇게 나와 있음

![throttling](https://i.pinimg.com/originals/5e/22/30/5e223039bfb59934d5dd94e86044d805.gif)

_~ㅎ 이짤이 생각남~_   
_~호머가 바트를 디바운싱하면 큰일남.. 중간중간 조르다 풀어야함(...?).. 그래서 쓰로틀링~_   
_위에 쓴 말은 좀 (많이) 이상한 것 같긴한데, 이렇게 생각하면 헷갈리지 않고 오래 기억할 것 같아서 적음_

예시 설명
수도꼭지에서 물이 나오는데 조여서 압력을 조절하는 이미지

<br>

**```요청이나 이벤트가 의도한 바 보다 너무 과도하게 발생할때,```**   
**```일정 delay를 주고 delay 동안 발생한 이벤트/요청/함수 등은 무시하는 것```**

<br>
<br>

예시 코드
<details> 
<summary>zerocho throttling 예시</summary>

```js
// 200ms 간격으로만 ajax 요청(console.log) 하게 하는 코드
// -> 타이머가 설정되어 있으면 아무 동작도 하지 않고, 타이머가 없다면 타이머를 설정
//    타이머는 200ms 이후에 스스로를 해제하고 ajax 요청을 날리게 됨

var timer;
document.querySelector('#input').addEventListener('input', function (e) {
  if (!timer) {
    timer = setTimeout(function() {
      timer = null;
      console.log('여기에 ajax 요청', e.target.value);
    }, 200);
  }
});
```
</details>

<details> 
<summary>개발자 아저씨들 힘을모아 throttling 예시</summary>

```js
// 마우스 스크롤 이벤트에 쓰로틀러를 200ms동안 적용시켜 숫자 1 증가 후 출력하는 예제
// -> 쓰로틀러를 200ms동안 작동시킴
//    쓰로틀러가 이벤트를 조이고 있는 경우, 해당 이벤트는 무시됨
//    결과적으로 200ms 동안 최대 1번의 이벤트만이 발생이 가능하게 됨 

var throttler;

window.addEventListener('scroll', function (e) {
    if (throttler) { 
        return 
    } 
    
    throttler = setTimeout(function() {
        console.log('스크롤 이벤트 발생!');
        const count = document.getElementById('count');
        count.innerText = parseInt(count.innerText) + 1;
        throttler = null;
    }, 200); 
}
```
</details>



<br>
<br>
<br>
<br>

## 정리

### - `쓰로틀링`: 마지막 함수가 호출된 후 일정 시간이 지나기 전에 다시 호출되지 않도록 하는 것

### - `디바운싱`: 연이어 호출되는 함수들 중 마지막 함수(또는 제일 처음)만 호출하도록 하는 것

<br>
<br>
<br>
<br>

