# <코딩 테스트를 위한 파이썬 문법>

<details>
<summary><b>목차</b></summary>

## [1. 자료형]()
## [2. 조건문]()
## [3. 반복문]()
## [4. 함수]()
## [5. 입출력]()
## [6. 주요 라이브러리 문법 & 유의점]()
</details>


<br>
<br>
<br>
<br>


<div style="text-align:center;">

## 자료형

</div>

<div style ="padding-left: 2%;">


<div style="padding-left: 3%"> 

### 정수형
</div>

<div style="padding-left: 3%"> 

### 실수형
</div>
정수부나 소수부가 0이면 생략 가능  
  
ex)
송지원 예제 417 첫번째 중간부터 0없는 애들만

<div style="padding-left: 3%"> 

### 지수 표현방식
</div>

-> ex) 최단 경로 문제 같은 경우 '무한'같은 값을 사용해야 할 때,               
최단 경로의 최댓값이 10억 미만이면, '무한'으로 10억 값을 사용할 수 있는데,   
이때 숫자 0을 9개 사용하는 방식은 내가 제대로 9개를 사용했는지 확인이 어렵고 또 확인해야 한다는 단점이 있음
  
=> 1e9 라고 지수 표현방식을 사용하면 깔끔하게 헷갈리지 않게 실수할 확률이 적게 표현할 수 있다


<div style="padding-left: 3%"> 

### IEEE 754
</div>
부동 소수점 표현방식  
-> 2진수로 실수를 저장하고 표현하는데 정확도의 한계가 있다

ex) 0.3 + 0.9 != 0.9
송지원 예제 418 두번째

그래서 이럴땐, round() 함수 사용  
round() 함수는 ~~하는 함수로,   
첫번째 인자로는 실수형 데이터이고,    
두번째 인자로는 (반올림하고자 하는 위치 - 1)이다.   

ex) 송지원 사용 예제 419 첫번째

그리고 일반적으로 코테에서 실수형 데이터를 비교할 때,   
소수점 5번째 자리에서 반올림한 결과가 같으면 정답으로 인정!   

송지원 예시 코드 예제 ?? 이건 뭐지? 없어도 되는 것 같은데..?

<div style="padding-left: 3%"> 

### 수 자료형의 연산
</div>
+
-
*
/ -> 주의! 기본적으로 파이썬에서는 나눠진 결과를 기본적으로 실수형으로 처리!!!   
% : ex)변수가 홀수인지 짝수인지 -> 나머지가 1인가?   
// : 나눈 결과에서 몫만 얻고자 할때!(일반적인 /연산).  
\** : 거듭제곱 연산자.  

송지원 / % // 예제 419 마지막 


<div style="padding-left: 3%"> 

### 리스트 자료형
</div>

C, Java의 Array와 비슷한 자료형  
내부적으로 연결 리스트 자료형을 채택하고 있어, append(), remove() 등 메소드 지원  
CPP STL Vector와 유사  

리스트 만드는 법   
대괄호 안에 원소를 넣어 초기화, 쉼표로 원소 구분,   
원소에 접근할때는 인덱스 값(0부터 카운트)을 대괄호 안에 넣음  
비어있는 리스트 선언할때 list() 혹은 [] 사용할 수 있음  

Tip) 코테에서는 크기가 N인 리스트를 초기화 해야하는데 다음과 같은 방법 사용하면 편리   
//크기가 N이고, 모든 값이 0인 1차원 리스트 초기화 하는 코드  
송지원 예제 421 두번째     

리스트 인덱싱과 슬라이싱.  

인덱싱 : 인덱스 값을 이용하여 리ㅌ스트의 특정한 원소에 접근하는 것.  
->양의 정수, 음의 정수, 0 모두 사용할 수 있다!   
ex) 인덱스 -1 이면 마지막 원소.  

슬라이싱 : 리스트에서 연속적인 위치를 갖는 원소들을 가뎌와야 할때 사용.  
대괄호 안에 콜론(:)을 넣어 시작 인덱스와 (끝 인덱스 - 1) 을 설정할 수 있다.  

리스트 컴프리헨션.  
리스트를 초기화 하는 방법 중 하나대괄화 안에 조건문과 반복문을 넣는 방식으로 리스트 초기화 할 수 있음.  

송지원 예제 페이지 422 중간.  
리스트 컴프리헨션은 코테에서 2차원 리스트를 초기화할때 매우 효과적!  
송지원 예제 페이지 423 첫번째. 
특정 크기의 2차원 리스트를 초기화 할때는 반드시 리스트 컴프리 핸션을 이용해야 함!   

//리스트컴프리헨션을 사용하지 않을 경우 발생할 수 있는 의도치 않은 결과.  
송지원 예제 페이지 423 마지막.  
-> ∵ 내부적으로 포함된 3개의 리스트가 모두 동일한 객ㅊ에 대한 3개의 래퍼런스로 인식되기 때문.  
=> ∴ 특정한 크기를 가지는 2차원 리스트를 초기활 할땐 리스트 컴프리핸션을 사용해야 함.  

리스트 자주 사용하는 메소드
append()
sort()
reverse()
insert()
count()
remove()

주의!
insert(), append(), remove() 함수!   
insert() 함수는 시간 복잡도가 O(N)!   
append() 함수는 시간 복잡도가 O(1)!   
따라서 insert() 함수 남발하면 시간 초과 날 수 있다!   
(∵ insert() 함수는 특정 위치에 원소 삽입하고, 리스트 원소 위치 조정해줘야 하기 때문).  

remove() 함수 또한 시간 복잡도가 O(N).  
-> 특정한 값의 원소를 모두 제거하려면? 어캐?   
=> 다음과 같은 방법 사용.  

송지원 예제 페이지 425 마지막    
//리스트에 있는 모든 원소에 한번씩 접근하여, 삭제 원소에 존재하는지 확인하고 없을시에만 새로운 리스트를 (리스트 컴프리헨션을 사용하여) 만드는 방식.  



<div style="padding-left: 3%"> 

### 문자열
</div>
문자열 변수 초기화 할때, 큰 따옴표나, 작은 따옴표 사용.  
따옴표 들어가야 할때는 다른 따옴표로 문자열을 묶거나,    
백슬래쉬 사용!   


문자열 연산

+ 두 문자열을 더해짐.  

* (뒤에 양의 정수) 문자열이 양의 정수 만큼 더해짐.  

파이썬 문자열을 기본적으로 리스트와 같이 처리됨.   
-> 인덱싱, 슬라이싱 모두 사용 가능함.  

<div style="padding-left: 3%"> 

### 튜플 자료형
</div>

리스트와 거의 비슷한 자료형이나,   
한번 선언된 값을 바꿀 수 없고,   
대괄호([])가 아닌 소괄호(())를 사용.  

=> 튜플 자료형은 그래프 알고리즘을 구현할 때 자주 사용!   
ex) 다익스트라 최단 경로 알고리즘 같은 최단 경로를 찾아주는 알고리즘 내부에서는 우선순위 큐를 이용하는데,  
해당 알고리즘에서 우선 순위 쿠에 한번 들어간 값을 변경되지 않음.  


=> 튜플은 값이 변경되면 안되는 곳에서 사용하여 실수로 값이 변경되고 있진 않은가 체크할 수 있음.  
 
또한 튜플은 리스트에 비해 상대적으로 공간 효율적이고,  
일반적으로 각 원소의 성징리 서로 다를때 주로 사용.  


ex)다익스트라 최단 경로 알고리즘에서 '비용'과 'Node.js번호'라는 서로 다른 성질의 데이터를 튜플로 묶음.  



<div style="padding-left: 3%"> 

### 사전 자료형
</div>

사전 자료형은 키와 값의 쌍으로 이루어진 자료형.  
앞서 소개한 리스트나 튜플은 값을 순차적으로 저장하지만,   
사전 자료형은 키-값 쌍을 데이터로 가진다는 점에서 우리가 원하느 변경 불가능한 데이터를 키로 사용할 수 있음??????   

파이썬의 사전 자료형은 내부적으로 해시 테이블을 이용.  
-> 데이터의 검색 및 수정에 있어 O(1)의 시간에 처리할 수 있음.  


활용방법
ex) '많은 수의 데이터 중 선택되었는지 확인 할때'.  
리스트를 쓰면 많은 수 만큼의 메모리 공간이 낭비.   
But 사전 자료형을 사용하면, 우리가 저장한 만큼만 저장하므로 효율적으로 저장 가능!   

사전 자료형에 특정한 원소가 있는지 검사할땐 '원소 in 사전' 형태로 사용할 수 있음.  
->이건 리스트나, 튜플도 사용할 수 있음.  

keys().  
values().  

송지원 예제 페이지 430 중간.  

<div style="padding-left: 3%"> 

### 집합 자료형
</div>

파이썬에서는 집합을 처리하기 위햔 집합 자료형 제공.  

특징.  
중복을 허용하지 않는다.  
순서가 없다.  


집합 자료형은 사전 자료형과 마찬가지로 순서가 ㅇ없다는 공통점이 있지만,   
집합 자료형에서는 키가 존재하지 않고, 값 데이터만 담게 됨.  

특정 원소가 존재하는지 검사하는 연산의 시간 복잡도는 사전 자료형과 마찬가지로 O(1).  

앞에서 말한 특정한 데이터가 이미 등장한적이 있는지 여부를 체크할때, 집합 자료형 사용 가능.  

초기화 할때는 set() 함수를 이용하거나.  
중괄호({}) 안에 각 원소를 콤마를 기준으로 구분해서 넣으면 된다.  


집합 자료형의 연산에는 '합집합', '교집합', '차집합' 연산이 있음

'|' 합집합.  
'&' 교집합. 
'-' 차집합. 

송지원 예제 페이지 431 마지막. 



add() O(1).  
update() 여러개 값을 한번에 추가. 
remove() O(1). 


</div>
<br>
<br>
<br>
<br>




<div style="text-align:center;">

## 조건문
</div>

if ~ elif ~ else 문 사용
파이썬에서는 {}를 사용하지 않고 들여쓰기로 블록 나눔 
-> 들여쓰기의 기준은 스페이스 바 4회 (탭 1회도 가능함)

in 연산자, not in 연산자
리스트 튜플, 문자열 사전과 같은 자료형에 어떠한 갑싱 존재하는지 확인하는 연산


pass문
조건문이 참이어도 아무것도 실행하고 싶지 않을때 사용
코드 디버깅 시 일단 조건문의 형태만 만들때 사용

조건부 표현식
송지원 436 마지막 예제
송지원 437 첫번째 예제



+ 파이썬에서는 부등호 중첩일때 일반적인 수학 처럼 사용 가능 
<br>
<br>
<br>
<br>




<div style="text-align:center;">

## 반복문
</div>

while 문

괄호 사용 X
괄호 대신 콜론 찍고 
다음 줄에 들여쓰기 하여 사용

송지원 439 첫번째 예제

for 문

for in - 리스트를 사용하는 구조로,
in 다음에 있는 데이터에 포함되어 있는 모든 원소를 첫번째 인덱스 부터 마지막까지 차례대로 방문
in 뒤에 리스트, 튜플, 문자열 사용 가능

송지원 439 마지막 예제
송지원 for in tuple 쓰는 예제 검색해서 작성
송지원 for in 문자열 쓰는 예제 검색해서 작성

for in range(~) 형태로 많이 쓰임
- range(시작 값, 끝 값 + 1) 형태로 쓰임
- range(값) 형태면 시작 값은 자동으로 0이고, 입력한 값은 (끝 값 + 1)이 됨
송지원 439 마지막 예제


<br>
<br>
<br>
<br>




<div style="text-align:center;">

## 함수
</div>

파이썬 함수의 형태

송지원 페이지 441 첫번째 예제

파라미터의 변수를 직접 지정해서 값을 넣어주는 방법
송지원 페이지 442 첫번째 예제


global 키워드
함수 안에서 함수 밖의 변수를 수정할 때 사용

gloal 키워드로 변수 지정하면, 해당 함수에서는 지역 변수 만들지 않고,
함수 바깥에 선언된 변수를 바로 참조
송지원 페이지 442 두번째 예제

람다 표현식
특정한 기능을 수행하는 함수를 한 줄에 작성할 수 있음
송지원 이건 검색해서 예제 + 컴공특 예제가 나은듯

Ex) 파이썬의 정렬 라이브러리를 사용할 때. 정렬 기준(key)을 설정할 때 자주 사용

<br>
<br>
<br>
<br>




<div style="text-align:center;">

## 입출력
</div>


### 입력


input() 함수 사용
한 줄의 문자열 입력
-> 숫자도 문자열로 입력받기 때문에, 입력을 정수형 데이터로 처리하기 위해서는 문자열을 정수로 바꾸는 int() 함수를 사용해야 함

#### 일반적인 경우

또 입력받을 때 데이터가 공백으로 나눠지는 경우가 많음
-> 입력받은 문자열을 띄어쓰기로 구분하여 각각 정수 자료형의 데이터로 저장하는 코드의 사용빈도가 매우 높음!!!
=> list(map(int, input().split())) 을 사용하면 됨!!!

~위에 식~의 의미
1. 먼저 input()으로 한 줄을 입력 받는다
2. 함수를 이용하여 공백으로 나눈 리스트로 바꾼다
3. 함수를 이용하여 해당 리스트의 모든 원소에 함수를 적용. 즉 모든 문자열이 정수형 데이터로 변경됨
4. 마지막으로 결과를 로 다시 바꿈으로 입력받은 문자열을 띄어쓰기로 구분하여 각각 숫자 자료형으로 저장!

=> 정말정말 자주 쓰는 코드이니 꼭 외우기!!!

대부분의 경우 공백 혹은 줄 바꿈으로 데이터를 구분
-> C 나 C++ 같은 경우는 scanf() 함수가 위 케이스를 모두 동일하게 처리
=> But Python 같은 경우는 줄 바꿈과 공백에 따라 다른 처리를 요구함

- 줄 바꿈 : int(input())을 여러 번 사용
- 공백 :  이렇게 사용

송지원 예제 445 첫번째


#### 데이터 개수 많지 않은 경우

단순히 map(int, input().split())을 이용

송지원 예제 445 두번째


#### 데이터 입력을 빠르게 받아야 하는 경우
Ex)정렬, 이진 탐색, 최당 경로...
1000만개가 넘는 라인이 입력 -> 입력만으로 시간 초과 날 수 있음

Python의 경우 sys 라이브러리에 정의되어 있는 sys.stdin.readline() 함수를 이용
(input() 함수와 동일하게 한 줄씩 입력받기 위해 사용)

송지원 페이지 336 첫번째

주의!
sys 라이브러리를 사용할 땐, 한 줄 입력을 받고 꼭 rstrip() 함수를 호출해야 함
∵ readline() 함수를 사용하면, 엔터가 줄 바꿈 기호로 입력되는데,
이 공백 문자를 제거하려면 rstrip() 함수를 사용해야 함

송지원 페이지 446 두번째 예제
+ 송지원 검색해서 Python 함수 별명? 붙이는 방법? 찾아서 위 함수 짧게 쓸 수 있는 꿀팁 알아보기




### 출력

print() 문을 입력하여 출력을 진행할 수 있음
print()는 변수나 상수를 매개변수로 입력받아 표준 출력으로 출력

각 매개변수를 콤마(,)로 구분하여 받을 수 있고, 각 매개변수라 띄어쓰기로 구분되어 출력됨

그리고 print() 함수는 기본적으로 출력 이후에 줄 바꿈이 수행됨

일부 문제의 경우 문자열 내 변수를 출력해야 하는 경우가 있음
-> 이때 문자열과 변수를 + 연산자를 이용하면 오류(TypeError)가 남
∵ 문자열 자료형 끼리만 + 연산이 가능하기 때문

해결법
1. str() 함수를 이용하여 변수를 문자열로 변환

송지원 447 맨 마지막 예제

2. 각 자료형을 콤마(,)를 기준으로 구분하여 출력

송지원 448 첫번째 예제

주의!
콤마를 사용하는 경우 사이사이에 불필요한 공백이 삽입될 수 있음!

3. f-string 문법 사용

Python3.6 이상부터 사용할 수 있는 문법(JS의 템플릿 리터럴과 비슷)
문자열 앞에 접두사 'f'를 붙임으로 사용할 수 있고,
단순히 중괄호 안에 변수를 넣음으로써, 자료형의 변환 없이 간단히 문자열 내 정수를 넣을 수 있음

송지원 448 마지막 예제


<br>
<br>
<br>
<br>




<div style="text-align:center;">

## 주요 라이브러리 문법 & 유의점
</div>

<div style="padding-left: 3%;"> 

### - 내장함수
</div>

print(), input() ~ 기본 I/O.   
sort() 정렬.   

sum() : 입력으로 받은 리스트의 합을 계산하여 리턴    
min() : 입력 받은 두개 이상의 값들 중 최소 값 리턴.  
max() : 입력 받은 두개 이상의 값들 중 최대 값 리턴.  
eval() : 수학수식을 문자열 형식으로 입력받아 계산한 결과 number type으로 리턴??    
sorted() : iterable 객체가 들어 왔을 때, 정렬된 결과 반환(<-> iterable 객체의 sort 함수와 다름!).   
			key 속성으로 정렬 기준 명시 가능 ~> 리스트 원소로 리스트나 튜플이 들어왔을. 경우    
			reverse 속성으로 (reverse=True) 설정하면 내림차순으로 정렬.    

송지원 페이지 452 첫번째 예제


<div style="padding-left: 3%;"> 

### - itertools
</div>

python에서 반복되는 형태의 data 처리하는 기능 제공하는 라이브러리.  
(순열과 조합 lib 제공)

permutations(순열) -> tuple로 리턴 & 객체 초기화 이후에는 리스트 자료형으로 변환하여 사용
combinations(조합)
product(permutations && 반복 허용)
combinations_with_replace


<div style="padding-left: 3%;"> 

### - heapq
</div>

힙(Heap) 기능
~> 다익스트라 최단경로 알고리즘 등 우선순위 큐 기능을 구현하고자 할때 사용
~> Py는 최소 힙(Min Heap)으로 구성

- heapq.heappush() : 원소 삽입
- heapq.heappop() : 원소 삭제

Ex)힙 정렬을 heapq를 통해 구현하는 예제
송지원 페이지 455 첫번째 예제

Ex)Py에서 최대 힙 사용하는 법
-> - 부호 처리 했다가 다 꺼내고 난 후 복구
송지원 페이지 455 마지막 예제


<div style="padding-left: 3%;"> 

### - bisect
</div>

송지원 456 부터 다시 정리~


<div style="padding-left: 3%;"> 

### - collections
</div>



<div style="padding-left: 3%;"> 

### - math
</div>



<br>
<br>
<br>
<br>




