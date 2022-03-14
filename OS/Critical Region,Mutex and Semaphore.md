# Critical Region(임계 구역)과 Race Condition

`Critical Region`은 자원이 공유될 수 있는 코드 블럭을 의미한다.

`Race Condition(경쟁 조건)`의 의미는, 두 개 이상의 프로세스/스레드가 공유 자원을 동시에 사용할 때 그 순서에 따라 결과가 달라지는 문제를 얘기한다.
예를 들면, 내 은행계좌에 2만원 밖에 없는데, 1번 ATM기기와 2번 ATM기기에서 동시에 2만원을 출금하려고 할 때, 접근 제어를 하지 않으면 2만원짜리 계좌에서 4만원이 출금되는 일이 발생한다.

이러한 문제를 해결하기 위해 임계 구역에 대한 여러가지 제어를 하게 된다.

## Critical Regions의 4가지 조건

- `Mutual Exclusion`(상호 배제) : 한 프로세스가 임계 구역에 진입 했다면, 다른 프로세스는 진입할 수 없다.
- `Bounded Waiting` : 한 프로세스가 임계 구역에 진입 하기 위해 무한히 대기하는 일은 발생하면 안된다.
- 임계 구역 외부에서 실행되고 있는 프로세스가 다른 프로세스들을 블록시켜서는 안된다.
- CPU 개수나 속도에 대한 어떠한 가정도 하지 않는다.

이 조건과 관련된 문제의 예시를 들어보면 아래 그림과 같다. 아래 그림은 생산자 - 소비자 문제이다.(Sleep and Wake Up)
![생산자-소비자](./img/saw.png)

이 임계구역 문제를 해결하기 위해 사용되는 것들 중 대표 적인 것이 뮤텍스와 세마포어 이다.

# Semaphore(세마포어)

- 동시에 접근할 수 있는 프로세스, 스레드의 수 (허용 가능한 갯수)를 가지고 있는 Counter이다.
- 공유된 자원의 데이터를 여러 프로세스, 스레드가 접근하는 것을 막기 위해 사용한다.
- 세마포어는 소유할 수 없다. 세마포어가 소유권이 있다면, 세마포어를 소유하지 않은 스레드가 세마포어를 해제할 수 있는 문제가 발생한다.

예를 들면서 이해해 보자. 잠겨 있는 화장실 칸이 있다. 세마포어는 칸을 열 수 있는 열쇠에 해당한다.(칸은 모두 같은 열쇠로 열린다) 화장실 칸이 4개이고, 열쇠가 4개라면, 4명까지는 대기없이 바로 사용할 수 있다. 4명이 넘어가면 대기를 해야한다. 이것이 바로 세마포어이다.

그리고 세마포어는 Counter의 갯수에 따라 나뉜다.

- 1개 : `Binary Semaphore` (=뮤텍스)
- 2개 이상 : `Counting Semaphore`

# Mutex

- 임계 구역을 가진 스레드들의 `Running Time`이 서로 겹치지 않게 단독으로 실행되게 하는 기술이다.
- 세마포어와 같이 공유된 자원의 데이터를 여러 프로세스, 스레드가 접근하는 것을 막기 위해 사용한다.
- 두 스레드가 뮤텍스 객체를 동시에 사용할 수 없다.

공유자원에 대한 접근을 조율하기 위해 Locking과 Unlocking을 사용한다.

- lock : 현재 임계 구역에 들어갈 권한을 얻어옴 ( 만약 다른 프로세스/스레드가 임계 구역 수행 중이면 종료할 때까지 대기 )
- unlock : 현재 임계 구역을 모두 사용했음을 알림. ( 대기 중인 다른 프로세스/스레드가 임계 구역에 진입할 수 있음 )

뮤텍스는 상태가 0,1이며, Counter가 1개인 `Binary Semaphore(이진 세마포어)`와 같다.

## 세마포어와 뮤텍스의 차이는?

- 세마포어는 뮤텍스가 될 수 있지만, 뮤텍스는 세마포어가 될 수 없다.
- 세마포어는 소유할 수 없으며, 뮤텍스는 소유할 수 있고 소유주가 그 책임을 진다.
- 뮤텍스의 경우 뮤텍스를 소유하고 있는 스레드가 이 뮤텍스를 해제할 수 있다. 하지만 세마포어는 소유하지 않고 있는 다른 - - 스레드가 세마포어를 해제할 수 있다.
- 뮤텍스는 동기화 대상이 1개일 때 사용하고 세마포어는 동기화 대상이 여러 개일때 사용한다.