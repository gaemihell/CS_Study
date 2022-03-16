<!-- @format -->

- [선택정렬 (Selection Sort)](#선택정렬-selection-sort)
  - [동작 원리](#동작-원리)
  - [특징](#특징)
  - [pseudo code](#pseudo-code)
  - [시간복잡도](#시간복잡도)
    - [최악의 경우](#최악의-경우)
    - [최선의 경우](#최선의-경우)
    - [평균](#평균)
- [삽입정렬 (Insertion Sort)](#삽입정렬-insertion-sort)
  - [동작 원리](#동작-원리-1)
  - [특징](#특징-1)
  - [pseudo code](#pseudo-code-1)
  - [시간복잡도](#시간복잡도-1)
    - [최악의 경우](#최악의-경우-1)
    - [최선의 경우](#최선의-경우-1)
    - [평균](#평균-1)
- [버블정렬 (Bubble Sort)](#버블정렬-bubble-sort)
  - [동작 원리](#동작-원리-2)
  - [pseudo code](#pseudo-code-2)
  - [시간복잡도](#시간복잡도-2)
- [병합정렬 (Merge Sort)](#병합정렬-merge-sort)
  - [동작 원리](#동작-원리-3)
  - [pseudo code](#pseudo-code-3)
  - [시간복잡도](#시간복잡도-3)
    - [최악의 경우](#최악의-경우-2)
    - [최선의 경우](#최선의-경우-2)
    - [평균](#평균-2)
- [퀵정렬 (Quick Sort)](#퀵정렬-quick-sort)
  - [동작 원리](#동작-원리-4)
  - [pseudo code](#pseudo-code-4)
  - [시간복잡도](#시간복잡도-4)
    - [최악의 경우](#최악의-경우-3)
    - [최선의 경우](#최선의-경우-3)
    - [평균](#평균-3)
- [힙정렬 (Heap Sort)](#힙정렬-heap-sort)
  - [동작 원리](#동작-원리-5)
  - [pseudo code](#pseudo-code-5)
  - [시간복잡도](#시간복잡도-5)
    - [최악의 경우](#최악의-경우-4)
    - [최선의 경우](#최선의-경우-4)
    - [평균](#평균-4)
- [기수정렬 (Radix Sort)](#기수정렬-radix-sort)
  - [동작 원리](#동작-원리-6)
  - [pseudo code](#pseudo-code-6)
  - [시간복잡도](#시간복잡도-6)
    - [최악의 경우](#최악의-경우-5)
    - [최선의 경우](#최선의-경우-5)
    - [평균](#평균-5)
- [계수정렬 (Count Sort)](#계수정렬-count-sort)
  - [동작 원리](#동작-원리-7)
  - [pseudo code](#pseudo-code-7)
  - [시간복잡도](#시간복잡도-7)
    - [최악의 경우](#최악의-경우-6)
    - [최선의 경우](#최선의-경우-6)
    - [평균](#평균-6)
- [정리](#정리)
- [QnA](#qna)
- [Reference](#reference)

# 선택정렬 (Selection Sort)

## 동작 원리

![selection-sort](img/SelectionSort.png)

정렬되지 않는 배열들 중 가장 작은 인덱스를 가진 원소와 최솟값을 가지는 원소를 교환하여 정렬하는 정렬 알고리즘 이다.

## 특징

- `in-place` 한 정렬이다.

  > `in-place` 란 추가적인 메모리가 필요없는 상태를 의미한다.

- `unstable` 한 정렬이다.

> unstable 이란 같은 값을 가진 원소들이 정렬 후에 같은 값을 가진 원소들 사이의 상대적 위치를 유지하는 것이 보장되지 않는 것을 의미한다.

- 자료의 이동횟수가 `3(n-1)` 로 정해져있다.

> swap 함수의 작업이 3번의 이동을 필요로 하며, (n-1)개의 자료에 swap이 일어나므로 3(n-1) 이다.

## pseudo code

```
for i <- 0 to n-2 do {
    min <- i
    for j <- i+1 to n-1 do {         // unsorted list A[i+1]...A[n-1]
        if(A[j]<A[min]) min <- j    // A[j]가 A[min]보다 작다면 min을 j로 덮어씌우고 for문을 지속한다.
    }
    swap(A[i], A[min])              // 최종적인 최솟값 A[min]와 A[i]의 값을 바꿈
}                                   // 이 과정을 반복하면 정렬이 됨.
```

## 시간복잡도

첫번째 원소는 `n-1`번 탐색..  
두번째 원소는 `n-2`번 탐색..  
...

n-1번째 원소는 `1`번 탐색

(n-1) + (n-2) + ... + 1 = n(n-1)/2

따라서 `O(N^2)` 이다.

최악, 최선의 경우에도 무조건 탐색을 하기 때문에 변함 없다.

### 최악의 경우

- O(N^2)

### 최선의 경우

- O(N^2)

### 평균

- O(N^2)

<br />

# 삽입정렬 (Insertion Sort)

## 동작 원리

![insertion-sort-1](img/InsertionSort-1.png)
![insertion-sort-2](img/InsertionSort-2.png)
![insertion-sort-3](img/InsertionSort-3.png)

배열을 정렬되지 않은 부분과 정렬된 부분으로 나눈 후, 정렬되지 않은 부분에 있는 데이터를 정렬된 부분의 특정 인덱스에 `삽입` 하며 정렬을 진행하는 알고리즘이다.

## 특징

- 원소가 이미 정렬되어 있는 경우엔 효율적이다.
- `in-place` 정렬이다.

- `stable` 정렬이다.

  > `stable` 이란 같은 값을 가진 원소들이 정렬 후에 같은 값을 가진 원소들 사이의 상대적 위치를 유지하는 것이 보장되는 것을 의미한다.

- 같은 시간복잡도`O(N^2)`를 가진 정렬 알고리즘들보다 빠르다.

  > 데이터들이 정렬되었을 때 O(N)의 시간복잡도를 가지므로, O(N^2) 시간복잡도를 가지는 정렬들 중에선 비교적 빠르다고 할 수있다.

## pseudo code

오름차순 정렬을 기준으로 한다.

```
int i, j, data

for i = 1 to n-1
    data = arr[i]   // 정렬안된 데이터 중 고름

    for j = i-1 to 0
        if arr[j] > data
        // 고른 데이터가 해당 인덱스 데이터보다 값이 작다면
        // 해당 인덱스 데이터를 뒤로 옮김 (데이터가 삽입될 수 있는 자리를 만들어줌)
            then arr[j+1] = arr[j]
        else
        // 크거나 같다면, 이곳에 삽입된다!
            break

    arr[j+1] = data
```

## 시간복잡도

### 최악의 경우

오름차순 정렬을 하는 삽입정렬일 때, 배열이 내림차순으로 (역순으로) 되어있을 때 최악의 경우이다.

매번 내부의 for문을 전부 순회하므로  
1번째엔 1번  
2번째엔 2번  
...
n-1번째엔 n-1번을 탐색한다.

따라서 총 `n(n-1)/2`번 탐색하며 이를 Big-O 표기법으로 나타내면

`O(N^2)`가 된다.

### 최선의 경우

전부 정렬이 되어있을때가 최선의 경우이다.
`pseudo code`의

```if
if arr[j] > data
```

이 부분을 항상 만족하지 못하므로 전부 break가 되어 `O(N)`의 시간복잡도를 가진다.

### 평균

`O(N^2)`

<br />

# 버블정렬 (Bubble Sort)

## 동작 원리

![bubble-sort](img/BubbleSort.png)

인접한 두 데이터를 비교해가며 정렬을 진행하는 방식이다.

오름차순으로 정렬한다고 가정하였을 때, 오른쪽 데이터가 더 작다면 swap하는 방식으로 정렬한다.

사실 할 말은 별로 없다.

## pseudo code

```
int i, j
for i = 0 to n-2
    for j = 0 to n-i-2
        if arr[j] > arr[j+1]
            then
                temp = arr[j]
                arr[j] = arr[j+1]
                arr[j+1] = temp
```

## 시간복잡도

i = 0 일 때 (n-1)번 탐색
i = 1 일 때 (n-2)번 탐색
...
i = n-2 일 때 1번 탐색

(n-1) + (n-2) + (n-3) + ... + 1 = n(n-1)/2

`O(N^2)`

# 병합정렬 (Merge Sort)

## 동작 원리

## pseudo code

## 시간복잡도

### 최악의 경우

### 최선의 경우

### 평균

# 퀵정렬 (Quick Sort)

## 동작 원리

## pseudo code

## 시간복잡도

### 최악의 경우

### 최선의 경우

### 평균

# 힙정렬 (Heap Sort)

## 동작 원리

## pseudo code

## 시간복잡도

### 최악의 경우

### 최선의 경우

### 평균

# 기수정렬 (Radix Sort)

## 동작 원리

## pseudo code

## 시간복잡도

### 최악의 경우

### 최선의 경우

### 평균

# 계수정렬 (Count Sort)

## 동작 원리

## pseudo code

## 시간복잡도

### 최악의 경우

### 최선의 경우

### 평균

# 정리

# QnA

# Reference

윤성우의 열혈 자료구조

https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html

https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html
