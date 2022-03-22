## Swapping

</br></br>

### 1) 특징
- **External fragmentation** : 공간이 쪼개져있는 것들을 합하면 들어갈 수 있는 경우
    
    → memory compaction (밀어서 공간 합치기) : overhead가 크다 (❌)
    
    → extra space : 공간을 여유롭게 할당 (👍)

</br></br>

![](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F4dcbe048-df7a-4567-963e-241c0f359ae0%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-11-06_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_8.39.56.png?table=block&id=d084da2c-fe53-44cc-a5f3-3538d39dde23&spaceId=4d9d3b27-bb1b-411b-a1a8-7cb1102cd8b0&width=2000&userId=f780b332-6c42-48fa-a9a1-d8836ed7aec7&cache=v2)

</br></br></br></br>

### 2) 구현방법

#### 1. Bits Maps

- MM의 allocation units를 설정(최소단위) → bit단위 ( 4.1 unit짜리 메모리는 5unit만큼 할당가능)
- 이에 따라 bit map 작성 (빈부분 : 0, 찬부분 : 1) → MM에 저장되어있음
- allocation unit 작으면 → bit map 커짐
- allocation unit 커지면 → 낭비되는 메모리가 늘어남 **(Internal fragmentation)**
- 찾는데 시간걸림
  
</br></br>

#### 2. Linked List
- [ P or H ] start ] size ] : 프로세스인지 홀인지 / 시작실제 주소 / 사이즈
- double linked lists
- internal fragmentation은 없음
- allocation unit 필요없음
- 홀이 붙어있는경우 따로 노드 x → 합쳐서 한 노드로

</br></br></br></br>

### 3) 새로운 자리로 할당하는 방법
1. first fit : 매번 처음부터 빈자리 찾음 (계속 앞부분만 씀)
2. next fit : 이전 탐색이 끝난 부분부터 탐색 
3. best fit : 가장 공간이 딱 맞는 곳으로 배정  (다 찾아야해서 오래걸림)
4. worst fit : 가장 공간이 큰곳에 배정  (다 찾아야해서 오래걸림)
5. quick fit : 많이 쓰이는 사이즈만 따로 빼서 관리 (유지비용든다)
6. others : 홀과 프로세스 노드를 나눠서 저장 (유지비용든다)
7. 홀 자체를 linked-list정보 저장소로 쓰자 (메모리를 아끼자)