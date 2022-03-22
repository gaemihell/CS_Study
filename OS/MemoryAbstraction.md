## A Memory Abstraction (메모리 추상화)

</br></br>

### 1) Memory Hierarchy

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/37c202a4-6e7c-40cc-aea0-4de847bc839e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-11-06_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_7.37.31.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220321%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220321T122636Z&X-Amz-Expires=86400&X-Amz-Signature=947a11e5e5c768ce88ced1da5e7ecd43aef6566663dd4b88ddbf6c353349a7ef&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA%25202021-11-06%2520%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE%25207.37.31.png%22&x-id=GetObject)

- CPU register : 컴파일러가 배정
- Main Memory(DRAM) : OS가 프로세스들의 메모리 경쟁을 관리
- Secondary Storage(Disk, SSD), Tertiary Storage : file system

</br></br></br>

### 2) No memory Abstraction : DRAM의 주소를 그대로 쓴다 
: 하나의 프로세스 but 거의 없다 

</br></br></br></br>

### 3) Memory Abstraction

</br>

#### 1. 여러프로그램이 같이 DRAM주소 그대로 쓰는 경우 (no memory abstraction):

![](https://blog.kakaocdn.net/dn/lOywx/btqLXSCuAOl/LPTpOXdK639DBymXRI6Pq1/img.png)

- 문제1. 사용자가 실수로나 의도적으로 잘못 다른 DRAM 주소에 접근할 수 있음 -> No Protection
- 문제2. C에서 보면 JMP 28에서 16412로 가는게 아니라 DRAM상에 28주소로 가버리기 때문에 프로그램에서 쓰던 주소를 그대로 쓰면 안된다 -> Relocation필요 (주소를 DRAM용으로 바꾸는)
  
</br></br>

#### 2. Memory Management Concepts
- Address Space : 프로세스마다 주소공간을 확보
  - Physical address space : main memory(DRAM)의 주소공간 -> 하드웨어가 결정
  - Logical/Virtual address space : 프로세스(프로그램)가 사용하는 주소공간(32bits, 64bits)

> virtual address는 하드웨어를 통해 Physical address로 변경되어 매핑된다

</br></br></br></br></br>

### 4) 매핑방법

#### 1. Base and Limit Registers (swapping system 전제: 전체가 왔다갔다)
- base : 모든 VA에 자동적으로 더해진다
- limit : 프로세스가 가질 수 있는 VA범위
    
    → 둘다 프로세스마다 다르며 PCD에 저장되어있다

![](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F10f4800d-214e-411a-b3dc-4ec928a883bc%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-11-06_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_8.04.16.png?table=block&id=17035c3f-0b4f-4289-a766-d35f136fe075&spaceId=4d9d3b27-bb1b-411b-a1a8-7cb1102cd8b0&width=2000&userId=f780b332-6c42-48fa-a9a1-d8836ed7aec7&cache=v2)


</br>

> 모든 프로세스의 메모리를 DRAM에 넣을 수 없음!!

</br></br></br></br></br>

### 5) Main memory와 Disk사이에 메모리 관리

- swapping : 프로세스 전체 메모리가 disk와 DRAM을 왔다갔다 하며 관리

- paging & segmentation : 프로세스 데이터 일부만 main memory에 있어도 됨

</br></br></br></br></br></br></br>

참고 
- https://velog.io/@holicme7/OS-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B4%80%EB%A6%AC1-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%B6%94%EC%83%81%ED%99%94%EA%B0%80-%EC%97%86%EB%8A%94-%EC%BB%B4%ED%93%A8%ED%84%B0
  