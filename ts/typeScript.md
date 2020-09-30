# 타입스크립트

#### 이 문서는 [fastcampus 강의](https://www.fastcampus.co.kr/dev_online_react/) 를 듣고 정리한 문서입니다. 문제가 있을 경우 <s26788761@naver.com> 으로 문의주세요! 😀


- 읽어볼 자료

[우아한 타입 스크립트](http://slides.com/woongjae/woowahan-ts)  
[타입스크립트 핸드북(한글) 문서](https://typescript-kr.github.io/)

<details>
<summary><b>강의 목록</b></summary>

- [<1강> TS?]()
- [<2강> TS 시작하기]()
- [<3강> TS 컴파일러]()
- [<4강> TS 컴파일러 설정 파일]()
- [<5강> 변수 선언]()
- [<강> ]()

</details>

## 개요

<이 강의를 통해 얻을 수 있는 것?>

- TS 사용하여 어캐 프로그래밍 하는지?
- TS 장점이 무엇인지?
- TS 제공 기능 무엇?

<br>

<배울 내용>

- TS 소개와 기본 문법
- TS 컴파일러
- ES6+와 TS 
- 제네릭, 데코레이터 그리고 고급타입(Partial, Pick, ...)
- 사자잡기 게임을 TS로 만들기

<br>

## TS?

- 오픈 소스
- JS의 상위 집합, ECMAScript의 최신 표준 지원
- 정적 언어로 컴파일 시간에 타입 검사  
	-> JS는 동적언어(프로그램 런타임에 타입이 결정) 즉, 타입이 계속 바뀜  
	-> But, TS는 컴파일 시간을 가지는 정적언어  
	컴파일 되어 만들어진 JS 파일을 브라우져나 Node.js 와 같은 JS 구동시킬 수 있는 환경에서 돌아감      

<br>

<장점>

- 강력한 타입  
	-> 대규모 어플리케이션 개발에 용이  
	(여러명의 개발자와 협업을 할 때, 메소드 등에서 특정한 타입을 요구 -> 실수를 방지 할 수 있다!)

- 유명한 JS 라이브러리의 편리한 사용 가능  
	Ex) JQuery, Moment.js, ... 쉽게 사용할 수 있음

- 개발도구에서의 강력한 지원

<br>

<b>
∴ TS는 PL로서 모든 JS 기능을 지원
         
&nbsp;&nbsp;&nbsp;  & 최신 JS 기능도 지원해서 컴파일을 통해 JS 파일을 만들어내는 하나의 PL      
</b>

<br>
<br>
<br>
<br>


## 개발환경

TS 컴파일러 - Node.js에서 구동

VS Code 설치    
&nbsp;&nbsp;&nbsp;&nbsp;-> 설정에서 'breadCrumbs' 검색 & 체크(활성화)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;파일 생성 시 상단에 네비게이션 생성

Terminal  
&nbsp;&nbsp;&nbsp;&nbsp;-> `npm install typescript -g` (전역으로 설치)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`sudo npm install typescript -g` (if MAC)

TS 컴파일러는 `tsc`라는 명령어를 통해 실행시킬 수 있음

<br>
<br>
<br>
<br>

## 컴파일

#### TS 컴파일러

- 기본 사용법: `tsc [options] [file...]` *//options, file 위치 바뀌어도 ㄱㅊ*
- 다양한 옵션 존재

<br>

#### TS 컴파일러 옵션

- **옵션 X**  
같은 위치에 같은 이름의 JS 파일 생성  
let 키워드 => var 키워드 (∵ 기본적으로 구형 브라우져도 지원되게 ES5로 구성)

- **target 옵션**   
`tsc hello.js --target es6`   
es6나 다른 버젼의 JS 파일 만들때, `--target` 옵션 사용  

- **lib 옵션**  
Ex) *ES6에 기능적으로 추가된 Promise와 같은 새로운 타입을 ES5 코드로 바꾼다면...?*    
-> error: 'Promise' only refuse to a type.... //Promise를 찾을 수 없다고 나옴<br>   
Promise와 같은 것은 ES5에서 문법적이라기 보단, 새로운 기능(**새로운 타입**)이 추가된 것!!!    
-> Promise를 지원하기 위해서는 별도의 폴리필?(라이브러리..?)이 필요!<br>    
-> 해당 라이브러리를 \<script> 태그를 전역에 추가를 하기 때문에 hello.js가 동작하는데 아무 문제가 없다! 라고 TS에게 말해줄 수 있어야 하는게 그게바로 `--lib` 옵션.<br>   
`tsc hello.js --lib es2015.promise`     
`tsc hello.js --lib es5,es2015.promise,es2015.iterable, dom`<br>  
∴ lib 옵션을 이용해서 전역이나 TS에서 쓰는 타입들이 어디까지가 제공되는지 컴파일러에게 말해줄 수 있음!  


- **module 옵션**  
모듈 시스템(ES6의 Module 시스템, CommonJS, RequireJS, ...)   
어떠한 종류의 모듈 시스템 사용할 지 TS 컴파일 시 정의 가능 <br><br> 
... 생략 ...<br>   
∴ `--module` 옵션 사용하여서 원하는 모듈 시스템으로 변경하여 컴파일 된 JS 파일 생성할 수 있다!
   
<br>

#### TS 컴파일러 설정 파일

tsconfig.json이라는 TS 컴파일러 설정 파일 생성

JSON 형태로 설정을 주게 됨

```JSON
{
  "include": ~~
  "exclude": ~~
  "compilerOptions": ~~
}
```

<br>

- "include"  
compile 시 포함될 파일을 명시, 여러개의 파일 목록 줄 수 있음.    
  
```JSON
"include": [
  "src/**/*.ts" //src 폴더 안의 전체 TS 파일들
], 
```

<br>

- "exclude"   
compile 시 제외할 파일을 명시

```JSON
"exclude": [
  "node_modules" 
  //일반적으로 Node.js 기반으로 만들기 때문에 npm init -y 로 프로젝트 생성하고, 
  // 후에 설치하는 모듈들은 "node_modules" 디렉터리에 저장 
  // -> 이 페키지들을 TS 컴파일 대상에서 제외
],
```

<br>

- "compilerOptions"   
컴파일과 관련된 설정들    
객체로 정의

```JSON
"compilerOptions": {
  "module": "commonjs",
  "rootDir": "src",
  "outDir": "dist",
  "target": "es5"
}
```


<br>
<br>
<br>
<br>

## 변수선언

#### 변수 선언, 어떻게 타입이 지정되는지...?

- **`var`** vs **`let`**   
차이? **스코프**!   
	 -	**`var`** : 함수 단위.  
함수 내에서는 코드 어디에서든지 접근 가능!   
Ex) if 문 안에 var 키워드 사용하여 변수 선언해도, 해당 함수 전체에서 해당 변수 사용 가능

	 -	**`let`** : 블록 단위.  
블록 안에서만 접근이 가능!

	 -	TS 는 변수에 처음 값을 할당 할 경우 하나의 타입으로 지정됨.   
&nbsp;&nbsp;&nbsp;&nbsp;후에 같은 타입으로 할당 -> 문제가 안됨!    
&nbsp;&nbsp;&nbsp;&nbsp;But, 다른 타입으로 할당 -> error! 

	 -	초기에 변수를 선언할 때    
&nbsp;&nbsp;&nbsp;&nbsp;a. 바로 값을 할당  
&nbsp;&nbsp;&nbsp;&nbsp;b. 바로 값을 할당 X  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-> 기본적으로 any 타입이 됨!    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-> 즉, 어떤 타입의 값도 저장할 수 있는 변수가 되는 것.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-> 다른 타입의 변수 넣어도 에러나지 않음.  
&nbsp;&nbsp;&nbsp;&nbsp;=> 이 경우, 타입 고정하고 싶으면 **`type-annotation`** 해주면 됨!       
`let scroe: number;`


<br>

<details>
<summary>var 헷갈리는 예제</summary>

```javascript
for (var i=0; i<3; i++) {
  setTimeout(function() {
    console.log(i);
  }, 100);
}
```

```
//results
3
3
3
```
</details>

<details>
<summary>위의 헷갈리는 예제 let 버젼</summary>


```javascript
for (let i=0; i<3; i++) {
  setTimeout(function() {
    console.log(i);
  }, 100);
}
```

```
//results
0
1
2
```
</details>


  
<br><br>
 

- **`const`**  
상수  
-> 선언시 무조건 초기값을 설정해 줘야함!    
&nbsp;&nbsp;&nbsp;&nbsp;∴ **`type-annotation`** 해주지 않아도 어떤 타입인지 바로 알 수 있다!   
-> 재할당이 불가.  
-> **`const`** 는 **`let`** 과 동일하게 블록 스코프 지님!

<br>
<br>
<br>
<br>

## 기본 타입

TS는 JS 기본 타입 다 지원 +a 지원



<div style="width:100%; height:100%; background-color:rgba(242, 243, 244, 0.7); display:flex; justify-contents: center; align-items:center;">
	<div style="width:30%; height:100%; background-color:white; border-top-right-radius:30px; border-bottom-right-radius:30px;">

- number
- string
- boolean
- undefined
- null
- object
- symbol 

	</div>

	<div style="width:70%; height:100%; padding-left:10px">
	ES6 기준 총 7개 타입
  
	(6개의 원시타입(primitive type), 1개의 참조형 타입(reference type))
	</div>
</div>

<br><br>


```javascript
let numberValue: number;
let stringValue: string;
let booleanValue: boolean;
let undefinedValue: undefined;
let nullValue: null;
let objectValue: object;
let symbolValue: Symbol;
```

#### - **`number`**
숫자형 타입.  
소숫점, 8진수/16진수 표현 가능

<br>

#### - **`string`**
- 리터럴 표현.  
""와 '' 사용 가능  
개행 시 에러
- (ES6) 템플릿 리터럴(string interpolation).  
문자열 내 개행 넣을 수 있음  

<br>

#### - **`boolean`**
true / false 만

<br>

#### - **`undefined`**
undefinedValue에는 **`undefined`** 값과 **`null`** 값 줄 수 있음

<br>

#### - **`null`**

**`undefined`** 와 **`null`** 은 모든 타입의 하위 타입.  
-> 어떤 타입의 변수라도 **`undefined`** 와  **`null`** 할당할 수 있음!   
(하위 타입은 상위 타입으로 정의된변수에 할당할 수 있다)

\+ **`any`** 타입은 모든 타입의 상위 타입!   
(**`any`**  타입의 변수에는 어떤 값도 할당할 수 있다)

<br>

#### - **`object`**
**`object`** 타입으로 명시된 변수는 원시타입(primitive type)을 제외한 값들이 할당될 수 O.  

ex) wrapper 타입

```
objectValue = String(33); //X
objectValue = new String(33); //O (∵ 33 문자열이 아닌 객체!)
```

<br>

#### - **`symbol`**
ES6에 추가된 primitive 타입.  
Symbol() 함수를 통해서만 생성할 수 있음!    
-> 유니크한 값 만들어짐.   
=> 대체로 객체의 프로퍼티로 쓰이게 됨.    
(하나의 객체를 정의할 때, 프로퍼티의 키로 사용)

<br>

#### - **`배열`**

let nameList: string[];

해당 배열에 어떤 배열을 할당하거나,   
push 함수등을 사용하여 값을 추가할 때는  
위에서 명시한 타입의 Data 만 추가 가능!

만약 여러 타입의 값을 넣어주고 싶다면, any[]로 만들어 줘야함!

<br>

#### - **`inline`** 타입? 형식?
객체가 어떤 속성들로 구성되어지는 지를 명시  
-> 별도의 타입을 정의하지 않고, 변수 선언과 동시에 인라인으로 정의할 수 O

```
let user1: { name: string, score: number };

user1 = { //name과 score 프로퍼티 없는 객체 할당 불가!
  color: 'red',
  width: 20
};

user1 = {
  name: 'jiwon',
  score: 100
}
```

-> 설정하고 나면, primitive 타입이나 다른 형태의? 객체 할당 불가!

만약 매번 재사용되어야 하는 타입은 inline으로 정의하지 않고,   
type alias나 interface나 class를 통해 타입을 정의할 수 있다!   

<br>

#### - **`tuple`**
배열과 유사  
원소의 갯수와 타입을 정의하는 것   
-> 갯수와 타입이 모두 맞아야 함!

```
let tuple1: [number, string];
let tuple2: [number, number, number];

tuple1 = [1, 'hello'];
tuple2 = [1, 2, 3];
//tuple2 = [1, 2, '3']; //X

```

<b><br><br>

∴ TS는 JS와 유사하게 6개의 primitive type과     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1개의 reference type에 대해 정의할 수 있고

이 이외에도 **`any`** 타입이라는 최상위 타입이 존재하여 모든 타입의 값을 할당할 수 있다

**`undefined`** 와 **`null`** 은 최하위 타입으로 상위 타입인 **`number`** , **`string`** 타입 변수들에 할당될 수 있다

**`객체`** 타입은 primitive type을 제외한 타입을 객체 타입이라고 하며

**`심볼`** 타입도 있고

TS에서는 추가로 **`tuple`** 이라는 것도 제공한다
</b>


<br>
<br>
<br>
<br>

 
