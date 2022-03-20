## B-Tree

</br></br>

### 1) 정의
B-tree는 이진트리의 확장된 개념으로 **하나의 노드가 가질 수 있는 자식 노드가 2개 이상인 트리**를 말합니다. B-tree는 방대한 양의 데이터를 저장하고 관리하는 곳에 주로 쓰이며 데이터베이스와 파일 시스템에 사용됩니다. 

</br></br>



</br></br>



### 2) 노드의 구조와 특징
</br>

![노드의 구조](https://hyungjoon6876.github.io/jlog/assets/img/20180720/btree_3.png)


-  k개의 키 : 오름차순으로 정렬되어있음
-  k+1개의 포인터 
   -  왼쪽 : 해당 키 값보다 **작은** 키들이 있는 자식노드
   -  오른쪽 : 해당 키 값보다 **큰** 키들이 있는 자식노드
  
  </br>


 특징1) **차수** : 노드가 최대로 가질 수 있는 key개수   
   ex)그림은 3차 B트리

특징2) **균형**을 이뤄야한다(Balanced Tree) = 모든 리프노드로까지의 길이가 같아야한다

특징3) **중복된 값**을 입력할 수 없다

</br></br>


</br></br>

### 3) key검색 

  : **균형트리**이기때문에 어떤 키도 O(logN)안에 탐색에 가능하며, 이진트리와 다르게 자식노드를 여러개 갖기 때문에 레벨이 낮아 훨씬 빨리 탐색가능

**알고리즘**
- 루트노드부터 시작
  - 노드에 있는 키와 순차적으로 대소비교를 통해 포인터를 선택
  - 찾는 값과 같은 키 발견하면 종료
- 리프노드까지 반복, 끝까지 찾지못한다면 탐색실패
  
  </br></br>

![](https://media.vlpt.us/images/emplam27/post/b7df8287-2524-4ec0-ad03-b969a8830c8e/B%ED%8A%B8%EB%A6%AC%20%EA%B2%80%EC%83%89%201.png)

![](https://media.vlpt.us/images/emplam27/post/e20bdef7-e106-4c89-9560-d7f57154dce1/B%ED%8A%B8%EB%A6%AC%20%EA%B2%80%EC%83%89%202.png)




</br></br>



</br></br>


### 4) key삽입

**알고리즘**
- 아무것도 없을 때 : 루트노드만들고 key삽입
- 루트노드만 있을 때 
  - 꽉 찼을 때: 루트노드에 넣고 중간키를 노드로 만들어서 위로 올린뒤 중간보다 작은값들을 왼쪽노드로 중간보다 큰 값들을 오른쪽 노드로 분할한다.  
  - 자리 있을 때: 오름차순으로 키 값 삽입
- 여러 노드들 있을 때: 비교를 통해 삽입 값이 들어갈 적합한 리프노드까지 내려간다
  - 리프노드 꽉 찼을 때: 리프노드에 넣고 중간키를 부모노드로 올리고 포인터를 알맞게 매치해준다 *
  - 리프노드 자리 있을 때: 오름차순으로 키 값 삽입

</br></br>

*인 경우 
![](https://media.vlpt.us/images/emplam27/post/4b5003e5-55de-441c-a3ee-15e4db7a2abd/B%ED%8A%B8%EB%A6%AC%20%EC%82%BD%EC%9E%85%202-1.png)

![](https://media.vlpt.us/images/emplam27/post/13ab96a4-04cc-42a7-bb01-eac1276bdf67/B%ED%8A%B8%EB%A6%AC%20%EC%82%BD%EC%9E%85%202-2.png)

![](https://media.vlpt.us/images/emplam27/post/d99cdbc8-c5b4-4667-be7d-2589adca45e8/B%ED%8A%B8%EB%A6%AC%20%EC%82%BD%EC%9E%85%202-3.png)
</br></br>



</br>

### 5) key삭제

**알고리즘**
- 삭제할 키가 리프에 있는 경우
  - 노드에 최소 키 이상있는 경우 : 삭제
  - 노드가 최소 키인 경우 
    - 형제노드가 최소가 키가 아닌 경우 : 삭제 후 부모키를 내리고 부모키자리에 적절한 형제 노드의 키를 올린다 (1)
    - 형제노드가 모두 최소 키인 경우 : 삭제 후 부모키와 형제노드 병합 (2)
  
  </br></br>

(1)
![](https://media.vlpt.us/images/emplam27/post/8e7b0f78-ae26-48df-8925-47171c588c48/B%ED%8A%B8%EB%A6%AC%20%EC%82%AD%EC%A0%9C%201-2.png)

</br></br>

(2)
![](https://media.vlpt.us/images/emplam27/post/dde5e5ae-892c-4d1c-9299-4710023f7531/B%ED%8A%B8%EB%A6%AC%20%EC%82%AD%EC%A0%9C%201-3.png)


</br></br></br></br>

**알골리즘** 
- 삭제할 키가 내부노드에 있는 경우
    - 노드나 자식노드의 키 수가 최소 키보다 많을 경우 : 자식 중 가장큰값(or 가장작은값)과 교환 후 삭제 -> 리프노드삭제로 변환 (3)
    - 노드나 자식노드의 키 수가 최소 키일경우  : 삭제 후 자식노드를 합치고 부모키도 인접 자식키와 합칩니다. 그뒤에 그 부모키의 자식노드를 합친 자식노드들로 갖게 합니다.  (4)

</br>

(3)
![](https://media.vlpt.us/images/emplam27/post/6d4a5d37-1633-45a1-8225-c6e558031865/B%ED%8A%B8%EB%A6%AC%20%EC%82%AD%EC%A0%9C%202.png)

</br></br>

(4-1) 최대키수 넘는 경우  : 재분배 

![](https://media.vlpt.us/images/emplam27/post/84dbc50f-fff4-4207-8e27-a34b9043f798/B%ED%8A%B8%EB%A6%AC%20%EC%82%AD%EC%A0%9C%203-1.png)

</br></br>

(4-2) 균형이 망가지는 경우 : 병합

![](https://media.vlpt.us/images/emplam27/post/e2f82f30-2f9c-4177-a908-1b5333f8e9d6/B%ED%8A%B8%EB%A6%AC%20%EC%82%AD%EC%A0%9C%203-2.png)



</br></br></br></br>


참고
- https://zorba91.tistory.com/293
- https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Tree
- https://ko.wikipedia.org/wiki/B_%ED%8A%B8%EB%A6%AC
  