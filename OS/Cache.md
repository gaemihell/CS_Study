<!-- @format -->

# Cache

## 장점

# Cache Placement Strategies

- 기본적인 설정

  32bit의 Physical Address 이므로 주소의 한계는 2^32

  따라서 메모리의 최대 크기는 4GB

  Word 의 크기 : 32bit = 4byte

  Block의 크기 : 4 Word = 16byte

  Block이 16byte 이므로, `Physical Memory`의 Block 갯수는 총 2^28개 (2^32 / 2^4)

  `Cache Memory`의 용량은 32KB 이므로 `Cache Memory`의 Block 갯수는 2^11개 (2^15/2^4)

**_Cache의 어느 곳에 Memory Block을 넣을 것인가?_**

## Fully Associative Cache

![fully-associative-cache](img/fully-associative-cache.png)

그냥 빈곳에 넣을 수 있음 ㅋㅋ

<p align="center">
  <img src="img/fully-associative-cache-architecture.png">
실제 구조
</p>

|                  tag                  |             tag ram             |           offset            |
| :-----------------------------------: | :-----------------------------: | :-------------------------: |
| `Physical Memory`의 몇 번째 block인지 | `Cache` 내부 데이터의 실제 위치 | Block 내 몇 번째 데이터인지 |

tag bit와 tag ram의 비트들을 동시에 전부 `XNOR`연산을 이용하여 (같으면 1, 다르면 0) True가 나올 경우, 그 Cache를 찾아가서 CPU에게 데이터를 주고 `Cache HIT`를 알린다.

- 장점
  - Conflict Misses가 발생하지 않는다.
  * Cache Hit 비율이 높다. 따라서 빠르다.

* 단점
  - 비교기가 Cache Block의 갯수(2^11) 만큼 필요하므로 비용이 많이든다.

## Direct Mapped Cache

![direct-mapped-cache](img/direct-mapped-cache.png)

정해진 곳에만 들어갈 수 있음 ㅋㅋ

-> Cache와 Memory 사이에 Mapping이 되어있음

![direct-mapped-cache](img/direct-mapped-cache-architecture.png)

2^11개의 Block을 한 덩이로 만듦

그러면 한 덩이가 하나의 Cache 전체에 대응됨

그러므로 각 덩이 안의 Block들은 Cache Block에 맵핑됨

Physical Address는 Block이 2^28개 있음

따라서 덩이들은 2^17(2^28/2^11)개 존재

|    tag     |        index         |         offset         |
| :--------: | :------------------: | :--------------------: |
| 몇 번 덩이 | 덩이 내 몇 번째 블럭 | 블럭 내 몇 번째 데이터 |

Decoder가 가리키는 `TAG RAM` 내부의 데이터와 tag 비트가 동일하고, write가 안되었다면 `Cache HIT`

- 장점
  - 하드웨어 설계가 간편함 (비교기가 1개)
  - 값이 상대적으로 저렴함

* 단점
  - Cache Hit 비율이 낮음
  * 실제 Memory Block의 위치에 따라 Cache 내의 위치가 정해져있으므로, `Collision Miss` 발생 가능

## Set Associative Cache

![set-associative-cache](img/set-associative-cache.png)

`Direct Mapped Cache` + `Fully Associative Cache`

![set-associative-cache](img/set-associative-cache-architecture.png)

Way의 크기만큼을 하나의 덩이로 본다.

기본적으로, Way 하나만 놓고 보았을 때, `Direct Mapped Cache`와 동일하다.

그러나, Way 중 "아무 곳이나 들어갈 수 있다" 는 자유로움이 존재한다.

예를들어, Way = 3 이라면, 하나의 Memory Block이 3가지의 Cache Block에 들어갈 수 있는 것이다.

- 장점

  - `Direct Mapped Cache`에 비해서 Cache Hit 비율이 높다.

  * 비교기가 Way 수 만큼 있기 때문에, `Fully Associative Cache`보다 가격이 저렴하다.

- 단점
  - Mux를 통과하기 때문에, `Direct Mapped Cache` 보다 느리다.

# Cache Block Replacement

- Random

  - 그냥 랜덤으로 한 block을 대체한다.

- LRU (least recently used)

  - timestamp 저장 필요

# Types of Cache Miss

- Cold-start Misses

  - 첫 접근은 무조~건 miss가 발생한다. why? 캐시에 없으니깐!

- Capacity Misses

  - 캐시의 크기보다 현재 프로그래밍 필요로 하는 `Memory block`이 더 클 경우 발생 가능!

  * Fully-Associative Cache여도 발생할 수 있는 Cache Miss이다.

- Conflict Misses

  - Direct-Mapped Cache, Set-Associative Cache 에서만 발생

  * Full-Associative Cache에선 발생 X

  * 여러 block들이 하나의 Cache block에 Mapping 되었을 때 발생하는 Cache Miss이다.

- Invalidation Misses

  - Cache에 데이터를 저장했는데, 원본이 수정이 되었을 때 발생하는 Cache Miss 이다.

# Reference

https://www.geeksforgeeks.org/types-of-cache-misses/
