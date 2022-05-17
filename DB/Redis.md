# Redis

### 1. 특징
- 고성능의 Key-Value 저장소이며 Value로는 List, Hash, Set등을 지원하는 NoSQL입니다. 
- in-memory database로 보통 Disk에서 데이터를 가져오는 RDB에 비해 작업속도가 빠릅니다. 
- Message Queue, Cache, Remote Dictionary등등으로 쓰입니다.
- single thread

### 2. 장점
- key-value 그리고 in-memory 라는 특징을 통해 메모리를 빠르게 관리할 수 있습니다. 
- 다양한 자료형을 Value로 제공

### 3. 단점
- in-memory database이기 때문에 장애발생시 데이터유실가능

### 4. 정책 
  #### persistence

  #### sharding

  #### maxmemory policy

