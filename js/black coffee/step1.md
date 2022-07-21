# Black Coffee 스터디 Step 1

## 🎯 step1 요구사항 - 돔 조작과 이벤트 핸들링으로 메뉴 관리하기

- [x] 에스프레소 메뉴에 새로운 메뉴를 확인 버튼 또는 엔터키 입력으로 추가한다.
  - [x] 메뉴가 추가되고 나면, input은 빈 값으로 초기화한다.
  - [x] 사용자 입력값이 빈 값이라면 추가되지 않는다.

> - Event
> - \<form> & \<input> tag
> - 이벤트 위임 (Event Delegation)
> - 상태를 UI로 렌더링


- [x] 메뉴의 수정 버튼을 눌러 메뉴 이름 수정할 수 있다.
  - [x] 메뉴 수정시 브라우저에서 제공하는 `prompt` 인터페이스를 활용한다.

> - 상태 업데이트 (메뉴 수정)
> - `prompt` 인터페이스

- [x] 메뉴 삭제 버튼을 이용하여 메뉴 삭제할 수 있다.
  - [x] 메뉴 삭제시 브라우저에서 제공하는 `confirm` 인터페이스를 활용한다.

> - 상태 업데이트 (메뉴 삭제)
> - `confirm` 인터페이스


- [x] 총 메뉴 갯수를 count하여 상단에 보여준다.
- 추가되는 메뉴의 아래 마크업은 `<ul id="espresso-menu-list" class="mt-3 pl-0"></ul>` 안에 삽입해야 한다.

```js
<li class="menu-list-item d-flex items-center py-2">
  <span class="w-100 pl-2 menu-name">${name}</span>
  <button
    type="button"
    class="bg-gray-50 text-gray-500 text-sm mr-1 menu-edit-button"
  >
    수정
  </button>
  <button
    type="button"
    class="bg-gray-50 text-gray-500 text-sm menu-remove-button"
  >
    삭제
  </button>
</li>
```

<br>
<br>

## PR list

- [송지원](https://github.com/blackcoffee-study/moonbucks-menu/pull/249)
- [이하은](https://github.com/blackcoffee-study/moonbucks-menu/pull/251)
- [김동영](https://github.com/blackcoffee-study/moonbucks-menu/pull/247)
	- [빈번하게 사용될 selector 기반으로 DOM 에서 원하는 Element를 구하는 로직을 이렇게 함수화 + 에러처리까지 같이 묶어놓은 구조]()
- [이시현](https://github.com/blackcoffee-study/moonbucks-menu/pull/261)
- [이승효](https://github.com/blackcoffee-study/moonbucks-menu/pull/248)
	- 사용자 정의 컴포넌트

_다른 팀_

- 

<br>
<br>

# What I Learned 😎 

## \<input> "keydown" 이벤트 한글 입력시 오류

```js
const inputValue = inputTag.value;
const trimmedInputValueString = String(inputValue).trim();

if (e.key === "Enter" && !e.isComposing) {
    addNewMenu(trimmedInputValueString);
    inputTag.value = "";
}
```


참고한 글 :
- [[JS] keydown/keyup에서 한글 입력 시 함수가 두 번 실행되는 경우](https://velog.io/@corinthionia/JS-keydown%EC%97%90%EC%84%9C-%ED%95%9C%EA%B8%80-%EC%9E%85%EB%A0%A5-%EC%8B%9C-%EB%A7%88%EC%A7%80%EB%A7%89-%EC%9D%8C%EC%A0%88%EC%9D%B4-%EC%A4%91%EB%B3%B5-%EC%9E%85%EB%A0%A5%EB%90%98%EB%8A%94-%EA%B2%BD%EC%9A%B0-%ED%95%A8%EC%88%98%EA%B0%80-%EB%91%90-%EB%B2%88-%EC%8B%A4%ED%96%89%EB%90%98%EB%8A%94-%EA%B2%BD%EC%9A%B0)
- [JavaScript Events Handlers — Keyboard and Load Events](https://levelup.gitconnected.com/javascript-events-handlers-keyboard-and-load-events-1b3e46a6b0c3)

<br>
<br>



## \<form> tag

### 'onSubmit' event

```diff
- <form onsubmit="return false;">
+ <form onsubmit="e => e.preventDefault()">
```

### 'submit' event

submit event 하나만으로

- \<input>에 엔터 입력
- \<form> tag 안에 있는 type="submit" 으로 설정된 \<button> 클릭

두 이벤트를 한번에 처리 가능!


<br>
<br>



## innerHTML 사용 🙅‍♂️ 

> 단순 text 입력이라면, HTMLParser가 포함된 innerHTML보다는 innerText또는 textContent를 사용하는게 더좋을것같습니다!

> 메이커준님 강의를 보다가 새롭게 배우게된 점이 있어 공유해드립니다!  
> mdn에 따르면 innerHTML보다는 insertAdjacentHTML의 사용을 권장합니다.

사유? 🤔 

- XSS 공격

- "appendChild" 보다 "insertAdjacentHTML" 함수가 성능적으로 더 나은 것 같다

- innerHTML로 child Node 업데이트 할 때
	- 새로운 리스트로 업데이트 할때,
	- $menuList.innerHTML = htmls.join('');
	- 위와 같은 방법으로 innerHTML를 재할당하는 방법을 사용하면,
	- child Nodes의 이벤트 핸들러 들이 제거되지 않는다고 합니다!
		- [참고한 글](https://www.javascripttutorial.net/dom/manipulating/remove-all-child-nodes/#:~:text=However%2C%20it%20is%20not%20recommended%20because%20it%20doesn%E2%80%99t%20remove%20the%20event%20handlers%20of%20the%20child%20nodes%2C%20which%20might%20cause%20a%20memory%20leak.)




[참고]

- [mdn "insertAdjacentHTML"](https://developer.mozilla.org/ko/docs/Web/API/Element/insertAdjacentHTML)


<br>
<br>



## document으로부터 HTMLElement 구하기


```
내가 남긴 피드백>

Id를 통해서 HTMLElement 를 조회할때는 getElementById() 메소드를 사용하고
className, data- 속성, 다양한 CSS selector 등을 사용할때는 querySelector() 를 사용하는 걸 추천? 하는 것 같아요
```

- 참고한 글 : [getElementById와 querySelector, 어느 것을 사용할까?](https://bobbohee.github.io/2021-02-12/getelementbyid-versus-queryselector)


- id :`getElementById()` 
- class 및 그외 selectors : `querySelector` >> 'getElementsByClassName()'

  - querySelector()는 일치하는 첫번째 요소를 만나면 반환하고 탐색을 중단
  - getElementsByClassName()은 document 전체를 탐색하지만
  - => 여러 요소를 한번에 찾을게 아니라면 querySelector()를 사용하는게 좀더 효과적이라 생각했어요!





<br>
<br>



## 자식 노드 삭제

내가 짠 코드

```js
// 기존에 menuList의 innerHtml에 존재하던 <li> 모두 제거
while (menuList.firstChild) {
    menuList.removeChild(menuList.firstChild);
}
```

- []()


> 피드백> 단순 자식노드삭제라면 remove()를 이용하는것이 더 좋을것 같습니다!    
> [remove() 와 removeChild() 의 차이](https://blogpack.tistory.com/683)


<br>
<br>



## EOF 개행

- [파일 끝에 개행을 추가해야 하는 이유](https://coderifleman.tumblr.com/post/115464362564/%ED%8C%8C%EC%9D%BC-%EB%81%9D%EC%97%90-%EA%B0%9C%ED%96%89%EC%9D%84-%EC%B6%94%EA%B0%80%ED%95%B4%EC%95%BC-%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0)

- [파일마다 EOL(End Of Line)을 왜 넣어야 할까](https://avocado12-note.tistory.com/11)


<br>
<br>



## @ts-check


<br>
<br>



## DOM 에서 원하는 selector 불러오는 로직 + 에러 처리 랩핑한 함수

```
/**
 * @template {Element} T
 * @param {string} selector
 * @returns {T}
 */
export function select(selector) {
    /** @type {T | null} */
    const element = document.querySelector(selector);

    if (!element) {
        throw new Error(`No element found for selector: ${selector}`);
    }
    return element;
}
```


<br>
<br>



## Event Delegation (이벤트 위임)

[이벤트 위임](https://ko.javascript.info/event-delegation)

```js
let selectedTd;

table.onclick = function(event) {
    let target = event.target; // 클릭이 어디서 발생했을까요?

    if (target.tagName != 'TD') return; // TD에서 발생한 게 아니라면 아무 작업도 하지 않습니다,

    highlight(target); // 강조 함
};

function highlight(td) {
    if (selectedTd) { // 이미 강조되어있는 칸이 있다면 원상태로 바꿔줌
        selectedTd.classList.remove('highlight');
    }
    selectedTd = td;
    selectedTd.classList.add('highlight'); // 새로운 td를 강조 함
}
```

👆문제점> '클릭 이벤트가 <td>가 아닌 <td> 안에서 동작할 수 있음. ∴ \<strong>을 클릭하면 event.target에 <strong>에 해당하는 요소가 저장됨'

<br>

```js
table.onclick = function(event) {
    
    let td = event.target.closest('td');
    /**
     * elem.closest(selector) 메서드는 
     * elem의 상위 요소 중 selector와 일치하는 가장 근접한 조상 요소를 반환
     * 위 코드에선 이벤트가 발생한 요소부터 시작해 위로 올라가며 가장 가까운 <td> 요소를 찾음
     * 만약 없다면 null 리턴
     **/

    if (!td) return;
    // event.target이 <td>안에 있지 않으면 그 즉시 null을 반환하므로 아무 작업도 일어나지 않음		

    if (!table.contains(td)) return;
    /**
     * 중첩 테이블이 있는 경우 event.target은 현재 테이블 바깥에 있는 <td>가 될 수도 있음. 
     * 이런 경우를 처리하기 위해 <td>가 팔괘도 안에 있는지를 확인
     **/

    highlight(td);
    // 우리가 원하는 처리
};
```

### 이벤트 위임 활용

버튼 각각에 독립된 핸들러를 할당하는 방법 🙅‍♂️  
-> 메뉴 전체에 핸들러를 하나 추가해주고, 각 버튼의 data-action 속성에 호출할 메서드를 할당해 주는 방법


### 장점

- 많은 핸들러를 할당하지 않아도 되기 때문에 초기화가 단순해지고 메모리가 절약됩니다.
- 요소를 추가하거나 제거할 때 해당 요소에 할당된 핸들러를 추가하거나 제거할 필요가 없기 때문에 코드가 짧아집니다.
- innerHTML이나 유사한 기능을 하는 스크립트로 요소 덩어리를 더하거나 뺄 수 있기 때문에 DOM 수정이 쉬워집니다.

### 단점

- 이벤트 위임을 사용하려면 이벤트가 반드시 버블링 되어야 합니다. 하지만 몇몇 이벤트는 버블링 되지 않습니다. 그리고 낮은 레벨에 할당한 핸들러엔 event.stopPropagation()를 쓸 수 없습니다.
- 컨테이너 수준에 할당된 핸들러가 응답할 필요가 있는 이벤트이든 아니든 상관없이 모든 하위 컨테이너에서 발생하는 이벤트에 응답해야 하므로 CPU 작업 부하가 늘어날 수 있습니다. 그런데 이런 부하는 무시할만한 수준이므로 실제로는 잘 고려하지 않습니다.

<br>
<br>



## 사용자 정의 컴포넌트

- [mdn "사용자 정의 요소 사용하기"](https://developer.mozilla.org/ko/docs/Web/Web_Components/Using_custom_elements)
- [https://github.com/mdn/web-components-examples](https://github.com/mdn/web-components-examples)


<br>
<br>



##


<br>
<br>



##






