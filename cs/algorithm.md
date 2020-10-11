# 정렬

### 1. Bubble Sort

#### <수도 코드>

``` C
void bubble_sort(int list[], int n) {
  int i, j, temp;

  for (i=0; i<n-1; i++) {
    for (j=0; j<n-1-i; j++) {
      if (list[j] > list[j+1]) 
        swap(&arr[j], &arr[j+1]);
    }
  }
}  

```

#### \<Time Complexity>


| Worst | Average | Best |
|-----------|--------|--------|
|**O(N^2)**|**O(N^2)**|**O(N) or O(N^2)**|

#### <특징>

**장점)** 
- 구현이 간단

**단)**
- 일반적으로 자료의 교환 작업(SWAP)이 자료의 이동작업(MOVE) 보다 더 복잡하기 때문에 버블 정렬은 단순성에도 불구하고 거의 쓰이지 않음.



<br>
<br>





### 2. Selection Sort

제자리 정렬(in-place sorting) 알고리즘의 하나(입력 배열 이외에 다른 추가 메모리를 요구하지 않음)

해당 순서에 넣을 위치(인덱스)는 정해져있고, 어떤 원소를 넣을지 선택하는 알고리즘

과정 :    
**1. 주어진 배열 중 가장 작은 값을 찾는다**  
**2. 그 값을 맨 앞에 위치한 값과 교체한다**  
**3. 맨 처음 위치를 제외한 나머지 리스트를 같은 방법으로 교체**  

#### <수도 코드>

``` C
void selection_sort(int list[], int n) {
  int i, j, least, temp;
  
  for (i=0; i<n-1; i++) {
    least = i; //i번째 위치에 새로운 원소 넣을 거임. 그리고 least는 일단 i번째 원소 값
    
    for (j=i+1; j<n; j++) { //for 문 돌면서 가장 작은 값의 index를 least 변수에 넣는다.
      if (list[j] < list[least])
        least = j;
    }

    if (i != least) { //만약 가장 작은 값 least가 i번째 원소라면 그냥 패스
      swap(&list[i], &list[least]); //가장 작은 값 least과 i번째 원소 바꿈
    }
}

```
#### \<Time Complexity>

| Worst | Average | Best |
|-----------|--------|--------|
|**O(N^2)**|**O(N^2)**|**O(N^2)**|

#### <특징>

**장점)** 
- 자료 이동횟수가 미리 결정된다.

**단점)**
- 안정성을 만족하지 않는다(..?)   
(값이 같은 레코드가 있는 경우에 상대적인 위치가 변경될 수 있다...?)




<br>
<br>





### 3. Insertion Sort

자료 배열의 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교하여, 자신의 위치를 찾아 삽입함으로써 정렬을 완성하는 알고리즘

두번째 자료부터 시작하여 그 앞 자료들과 비교하여 삽입할 위치를 지정한 후, 자료를 뒤로 옮기고 지정한 자리에 자료를 삽입하여 정렬하는 알고리즘

(즉, 두번째 자료는 첫번째 자료와, 세번째 자료는 두번째와 첫번째 자료와 비교하여 삽입할 위치를 찾는다. 삽입할 위치를 찾았으면 그 위치에 자료를 삽입하기 위해 자료를 한칸씩 뒤로 이동함)

처음 키 값은 두번째 자료부터 시작


#### <수도 코드>

``` C
void insertion_sort(int list[], int n) {
  int i, j, key;
  
  for (i=1; i<n; i++) {
    key = list[i]; //이번에 새로운 위치에 놓을 값을 key 값에 저장
    
    for (j=i-1; j>=0 && list[j]>key; j--) { //이전에 정렬된 i-1개의 원소들을 뒤에서 부터 찾으면서 key가 들어갈 위치가 나올때까지 한칸씩 뒤로 민다.
      list[j+1] = list[j];
    }
    
    list[j+1] = key; //다 밀렸으면 바른 위치에 key값 삽입
  }
}

```
#### \<Time Complexity>

| Worst | Average | Best |
|-----------|--------|--------|
|**O(N^2)**|**O(N^2)**|**O(N)**|


#### <특징>

**장점)** 
-  안정한 정렬 방법
- 레코드 수가 적을 경우 알고리즘 자체가 매우 간단하므로 다른 복잡한 정렬 방법보다 유리할 수 있음.
- 대부분의 레코드가 이미 정렬되어 있는 경우에 매우 효울적일 수 있다


**단점)**
- 비교적 많은 레코드들의 이동을 포함함
- 레코드 수가 많고 레코드 크기가 클 경우 적합하지 않다.



<br>
<br>






### 4. Merge Sort

분할정복(Divide and Conquer) 알고리즘 중 하나
(분할정복 방법은 문제를 작은 2개의 문제로 분리하여 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 방법. 분할정복 방법은 대개 순한 호출을 이용하여 구현함)

- 분할(Divide) : 입력 배열을 같은 크기의 2개의 부분 배열로 분할한다
- 정복(Conquer) : 부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면, 순환 호출을 이용하여 다시 분할 정복 방법을 적용한다
- 결합(Combine) : 정렬된 부분 배열들을 하나의 배열에 합병한다.

머지소트는 추가적인 리스트가 필요

각 부분 배열을 정렬할 때도 합병 정렬을 순환적으로 호출하여 적용


#### <수도 코드>

``` C
int sorted[MAX_SIZE]; //추가적인 공간이 필요!!

void merge(int list[], int left, int mid, int right) {
  //이 merge 함수에서는 나눠진 두 부분배열을 합치면서 정렬을 하는 과정!

  int i, j, k, l;
  i = left; //나눠진 왼쪽 부분 배열이 시작하는 인덱스
  j = mid + 1; //나눠진 오른쪽 부분 배열이 시작하는 인덱스
  k = left; //새로운 원소 삽입할 위치 저장하는 변수

  while (i<=mid && j<=right) { //투 포인터 기법
    if (list[i] <= list[j]) //나눠진 왼쪽 부분배열, 오른쪽 부분배열의 왼쪽부터 작은 값을 sorted 배열에 저장하고, 해당 부분 배열의 index 변수 i,j를 ++ 처리
      sorted[k++] = list[i++];
    else
      sorted[k++] = list[j++];
  }

  //부분 배열 중 어느 배열이 먼저 끝남!
  if (i > mid) { //왼쪽 부분 배열이 먼저 끝남
    for (l=j; l<=right; l++) //오른쪽 부분 배열 저장
      sorted[k++] = list[l];
  }
  else {
    for (l=i; l<=mid; l++)
      sorted[k++] = list[l];
  }

  for (l=left; l<=right; l++) {
    list[l] = sorted[l]; //추가적인 공간에 저장했던 값을 기존 공간으로 복붙
  }
}

void merge_sort(int list[], int left, int right) {
  int mid;

  if (left < right) {
    mid = (left + right)/2;
    merge_sort(list, left, mid); // 왼쪽 부분 배열
    merge_sort(list, mid+1, right); //오른쪽 부분 배열
    merge(list, left, mid, right); //실제 정렬하는 부분
  }
}
```
#### \<Time Complexity>

| Worst | Average | Best |
|-----------|--------|--------|
|**O(NlogN)**|**O(NlogN)**|**O(NlogN)**|


#### <특징>

**장점)** 

**단점)**


<br>
<br>





### 5. Quick Sort

#### <수도 코드>

``` C

```
#### \<Time Complexity>

| Worst | Average | Best |
|-----------|--------|--------|
|**O()**|**O()**|**O()**|


#### <특징>

**장점)** 

**단점)**



<br>
<br>





# 유명한 알고리즘

### 1. 다익스트라 알고리즘

#### <수도 코드>

``` C

```
#### \<Time Complexity>

| Worst | Average | Best |
|-----------|--------|--------|
|**O()**|**O()**|**O()**|





<br>
<br>




