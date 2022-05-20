# Redis

</br></br>

## 1. 특징
- 고성능의 Key-Value 저장소이며 Value로는 List, Hash, Set등을 지원하는 NoSQL입니다. 
- in-memory database로 보통 Disk에서 데이터를 가져오는 RDB에 비해 작업속도가 빠릅니다. 
- Message Queue, Cache, Remote Dictionary등등으로 쓰입니다.
- single thread

</br></br></br>

## 2. 장점
- key-value 그리고 in-memory 라는 특징을 통해 메모리를 빠르게 관리할 수 있습니다. 
- 다양한 자료형을 Value로 제공

</br></br></br>

## 3. 주의점 
- in-memory database이기 때문에 장애발생시 데이터유실가능

</br></br></br>

## 4. 정책 
  ### persistence
  Redis는 데이터를 메모리에 저장하기 때문에 서버가 다운되면 데이터가 유실될 수 있습니다. 따라서 disk에도 데이터를 저장해놓습니다.

  </br>

  1) SNAPSHOT
  
    
  
  - SAVE(blocking) : 순간적으로 redis의 모든 동작을 정지시키고 메모리의 snapshot을 디스크에 저장합니다. 


  - BGSAVE(non-blocking) : 별도의 process로 명령어 수행 당시의 메모리 snapshop을 디스크에 저장합니다.
  
</br></br>


2) AOF
- Redis의 모든 연산을 log파일에 기록하는 방식으로 서버가 재시작할 때 저장해둔 로그를 순차적으로 실행해 데이터를 복구합니다

</br></br>

> 두 방식을 혼용하는 것이 좋습니다. 주기적으로 SnapShot을 저장하고 주기 사이에는 AOF로 로그를 남겨서 데이터 유실을 방지 

</br></br>

### maxmemory policy
: 최대 memeory만큼 메모리를 사용하게 되면 아래의 정책들에 따라 과거에 만들어진 키들을 삭제합니다

</br>

1) Noeviction : 키들을 삭제하지 않고 메모리를 최대이상 사용하면 error를 발생시킵니다.

2) Allkey : 특정 알고리즘을 기반으로 모든 키를 대상으로 삭제
   1) LRU :least recently used
   2) Random
   3) LFU : least frequently used

3) Volatile : 특정 알고리즘을 기반으로 EXPIRE SET에 있는 키들을 삭제
   1) LRU
   2) Random
   3) TTL : Time To Live가 작은 순으로 삭제
   4) LFU
