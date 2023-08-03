
# item 2 "타입스크립트 설정 이해하기"


> $ tsc --noImplicitAny program.ts

> tsconfig.json  
> "_tsc --init_" 으로 생성함

cli로 하거나 설정 파일을 사용 가능함.

설정 파일 사용하는 걸 추천    
∵ 어떻게 사용것인지에 대해 동료들이나 다른 도구들이 알 수 있음

&nbsp;
&nbsp;


## noImplicitAny

> ### 변수들이 미리 정의된 타입을 가져야하는지 여부를 제어

&nbsp;

"any 타입" => 유용하지만 주의 깊게 사용해야 함(타입 체커가 무의미해짐)


```ts
// "a" 매개변수에는 암시적으로 'any' 형식이 포함됨
// "b" 매개변수에는 암시적으로 'any' 형식이 포함됨
function add(a, b) {
	return a + b;
}
```

any를 코드에서 사용하진 않았지만, any 타입으로 간주되기 때문에

이를 "암시적 any"라고 부름

> ### 암시적 (implicit)   
> <-> 명시적 (explicit)의 반대말   
> "암묵적으로 합의된" 이라는 의미

&nbsp;


```ts
// "noImplicitAny" 가 설정되었다면 오류가 됨.
function add(a, b) {
	return a + b;
}
```
&nbsp;

#### Solution) 명시적으로 ": any" 라고 선언해주거나, 더 명시적인 타입을 사용하면 해결됨


- 웬만하면 noImplicitAny 설정해야 함(∵ ㅌㅅ 는 타입 정보를 가질때 가장 효과적)
- ㅌㅅ가 문제를 발견하기 수월해짐
- 코드 가독성 증가
- 개발 생산성 향상
- noImplicitAny 옵션을 해제하는 것은 기존 JS 프로젝트를 ㅌㅅ로 마이그레이션 하는 과정에서만 필요함


&nbsp;
&nbsp;


## strictNullCheck

> ### null 과 undefiend 가 모든 타입에서 허용되는지 확인하는 설정

&nbsp;


```ts
// "strictNullCheck" 가 해제되었다면 유효한 코드.
const x: number = null;
```

&nbsp;


```ts
// "strictNullCheck" 가 설정되었다면 오류가 됨.
const x: number = null;
// ~ 'null' 타입은 'number' 타입에 할당할 수 없습니다.

// null을 허용하고자 한다면 명시적으로 드러냄으로 오류 수정 가능
const x: number | null = null;
```
![](https://media.geeksforgeeks.org/wp-content/uploads/20220214161708/Screenshot20220214at41119PM.png)

&nbsp;


- strictNullCheck는 null과 undefined 관련된 오류들을 잡아내는 데 많은 도움이 되나, 코드 작성을 어렵게 함
- 새 프로젝트를 시작한다면 strictNullCheck 설정을 추천
- 기존 JS 프로젝트를 마이그레이션한다면 strictNullCheck 설정을 좀 고민
- 그리고 strictNullCheck를 설정하려면 먼저 noImplicitAny를 설정해야 함
- 프로젝트가 거대해질 수록 설정을 변경하는 것은 어려울 것이므로, 가능한 초반에 설정하는게 좋음

&nbsp;
&nbsp;

## 기타 설정

- _noImplicitThis_
- _strictFunctionTypes_
- ...

등등 설정이 많지만 `noImplicitAny`, `strictNullCheck`가 제일 중요.

모든 체크를 설정하고 싶다면 `strict` 설정 하면 됨


&nbsp;
&nbsp;
&nbsp;
&nbsp;
