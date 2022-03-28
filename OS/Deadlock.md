<!-- @format -->

# Deadlock

![deadlock](img/actual-deadlock.png)

두 개 이상의 작업이 서로 상대방의 작업이 끝나기 만을 기다리고 있기 때문에 결과적으로 아무것도 완료되지 못하는 상태를 가리킨다.

# Deadlock 발생 조건

- 상호배제 (Mutual exclusion)

- 점유대기 (Hold and Wait)

- 비선점 (No preemption)

- 환형대기 (Circular wait)

# Deadlock을 해결하기 위한 정책

- Deadlock prevention

- Deadlock avoidance

- Deadlock detection

# Deadlock Prevention

- 상호배제 (Mutual exclusion)

- 점유대기 (Hold and Wait)

- 비선점 (No preemption)

- 환형대기 (Circular wait)

# Deadlock avoidance

- 프로세스 시작 거부

- 자원 할당 거부
  - banker's algorithm

# Deadlock detection

- Deadlock 발견 알고리즘

- Deadlock 회복 알고리즘

# Dining Philosophers problem

- 세마포어를 이용한 해결 방법

```cpp

/* 첫번째 방법 */

semaphore fork [5] = {1};
int i;
void philosopher(int i) {
    while(1) {
        think();
        wait(fork[i]);
        wait(fork[(i+1)%5]);
        eat();
        signal(fork[(i+1)%5j]);
        signal(fork[i]);
    }
}

int main() {
    parbegin(philosopher(0), philosopher(1), philosopher(2), philosopher(3), philosopher(4))
}
```

```cpp

/* 첫번째 방법 */

semaphore fork[5] = {1};
semaphore room = {4};
int i;
void philosopher(int i) {
    while(1) {
        think();
        wait(room);
        wait(fork[i]);
        wait(fork[(i+1)%5]);
        eat();
        signal(fork[(i+1)%5]);
        signal(fork[i]);
        signal(room);
    }
}

int main() {
    parbegin(philosopher(0), philosopher(1), philosopher(2), philosopher(3), philosopher(4))
}
```

- 모니터를 이용한 해결 방법

```cpp
monitor dining_controller;
cond forkReady[5];
bool fork[5] = {true};

void get_forks(int pid) {
    int left = pid;
    int right = (++pid)%5;
    if(!fork[left]) {
        cwait(forkReady[left]);
    }
    fork(left) = false;
    if(!fork[right]) {
        cwait(forkReady[right]);
    }
    fork[right] = false;
}

void release_forks(int pid) {
    int left = pid;
    int right = (++pid)%5;

    if(empty(forkReady[left])) {
        fork[left] = true;
    } else {
        csignal(forkReady[left]);
    }

    if(empty(forkReady[right])) {
        fork[right] = true
    } else {
        csignal(forkReady[right])
    }
}

void philosopher[k=0 to 4] {
    while(1) {
        <think>;
        get_forks(k);
        <eat spaghetti>
        release_forks(k);
    }
}
```

# Reference

https://ko.wikipedia.org/wiki/%EA%B5%90%EC%B0%A9_%EC%83%81%ED%83%9C

Operating Systems Internals and Design Principles 8th, William Stallings
