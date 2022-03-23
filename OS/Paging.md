## Paging(Virtual Memory)

</br></br></br>

### 1) Virtual Memroy
-  Swapping의 해결책
-  실제 사용되는 코드와 데이터 영역만을 Main Memroy로 로딩 되면 프로그램 수행가능
-  paging, segmentation 등등이 있음


</br></br></br>

### 2) Paging

</br></br>


- CPU
![](https://t1.daumcdn.net/cfile/tistory/2346B74E5919A26716)


</br></br>

- paging
![](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F6f160dc8-1c3b-4675-b148-d420a4930fea%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-11-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_12.16.59.png?table=block&id=1c5e0cdc-d852-45ee-976f-d0cc9f30c369&spaceId=4d9d3b27-bb1b-411b-a1a8-7cb1102cd8b0&width=2000&userId=f780b332-6c42-48fa-a9a1-d8836ed7aec7&cache=v2
)


</br>

- MMU : VA → PA 바꿔준다
- page : Virtual address space를 같은 유닛으로 나눈 것
- frame : Physical address space를 같은 유닛으로 나눈 것
- mapping : page 와 frame이 연결되는
- page table : 어떤 page가 어떤 frame에 연결되어있는지 (mapping의 정보를 담고있음)


</br></br></br>

#### 1. MMU에서 주소변환
</br>

![](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F30c0ef9a-48a6-4751-8716-efd032ce63d5%2FUntitled.png?table=block&id=a8ed6d3e-85d0-4c85-b3c1-c6da0b32d6d0&spaceId=4d9d3b27-bb1b-411b-a1a8-7cb1102cd8b0&width=2000&userId=f780b332-6c42-48fa-a9a1-d8836ed7aec7&cache=v2)

- VA를 16bits로 나타냈을 때 상위 4bits(VPN)에 해당하는 index를 PT에서 찾는다 
- 찾은 PTE의 page frame번호(PFN)를 찾는다
- page frame 번호 4bits(PFN) + VA의 하위 12bits(offset) = PA

    → 32bits일 경우에는 VA의 20bits로 page번호로 계산 

- PT(MM에 있음)참고할때 1번, PA로 가서 메모리 참고할때 1번 → 총 두번 main memory에 접근

</br></br></br>

#### 2. PTE(page table entry)

![](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F7b4fd19a-d06a-4695-9673-6202a3018649%2FUntitled.png?table=block&id=71a1d192-e671-43e8-9462-012031866502&spaceId=4d9d3b27-bb1b-411b-a1a8-7cb1102cd8b0&width=2000&userId=f780b332-6c42-48fa-a9a1-d8836ed7aec7&cache=v2)

- page frame number(PFN) 담고있음
- present/absent(valid) : 쓸수 있고 없고 차이 (absent면 page fault발생)
- modify bit(dirty) : store옵션이 일어났는지
- reference bit : 접근된적이 있는지 여부
- protections bits : 권한 제한 (read, write..)
- 
</br></br></br>

#### 3. Page Fault
- frame으로 mapped되어있지 않은 page에 access할때
- disk에서 가져와야하기때문에 process → blocked
- 가장 안쓰인 page frame을 내쫓고 disk에서 가져온다
