## Protocol(프로토콜)

</br></br>

### 1. 프로토콜의 의미 : 컴퓨터나 원거리 통신장비 사이에 **메세지를 주고받는 양식과 규칙**의 체계

</br>
</br>
</br>

### 2. 기본요소 

-   구문(Syntax) : 전송하고자 하는 데이터의 형식, 부호화, 신호 레벨등을 규정
-   의미(Semantics) : 효율적이고 정확ㅎㄴ 정보 전송을 위한 협조 상항과 오류 관리를 위한 제어정보 규정
-   순서(Timing) : 통신속도, 메세지의 순서제어 등을 규정 

</br></br></br></br>

### 3. 계층
: 프로토콜은 7개의 계층구조를 가지고 있으며 각 계층의 역할이 구분되어있습니다. 이렇게 계층을 나눈 이유는 단계별로 통신을 파악할 수 있으며 특정 단계에서 문제가 발생해도 다른 부분과 독립적으로 해결해주면 되기 때문입니다. 

![](/network/img/7layers.png)

</br></br>

#### 특징
    - 순서 : 송신은 layer 7 -> layer 1, 수신은 layer 1 -> layer 7
    - 독립 : 계층끼리 서로 영향을 미치지 않는다
    - 위계 : 기본적으로 하위계층은 상위계층을 위해 기능, 상위계층은 하위 계층에 관여하지 않음 

</br></br>

#### 각 레이어 설명
  - 물리계층(physical Layer)
    -   사용되는 통신 단위는 비트
    -   데이터를 전기적 신호로 변환하여 주고받는 역할만(에러신경x)
    -   장비로는 통신케이블, 허브 등이있음
  
  - 데이터 링크계층(DataLink Layer) 
    - 물리계층을 통해 주고받는 데이터의 오류와 흐름 관리
    - 오류탐색과 재전송기능
    - MAC주소로 통신 
    - 데이터 전송 단위는 frame
    - 장비로는 스위치가 있음
  
  - 네트워크계층(Network Layer)
    - 데이터를 목적지 까지 빠르게 전달(라우팅)
    - 노드를 거칠 때 마다 경로선택, 주소정해서 경로를 따라 패킷전달
    - 장비로는 라우터가있음
    - 라우팅, 흐름제어, 세그멘테이션, 오류제어, 
    - IP(논리적 주소)할당

  - 전송 계층(Transport Layer)
    - 통신을 활성화하기위한 계층 
    - 보통은 TCP프로토콜, 포트를 열어서 응용프로그램들이 전송할 수 있도록 
    - 아래서 올라온 데이터는 하나로 합쳐서 위로 올려줌
    - 양 끝단의 사용자(End to End)들이 신뢰성있게 데이터를 주고받을 수 있도록
    - sequence number기반의 오류제어방식(순서 역전 방지, 중복 패킷 방지..)
    - 포트(port)번호로 응용프로그램 구분 

  - 세션 계층(Session Layer)

  - 표현 계층(Presentation Layer) 

  - 응용 계층(Application Layer)
    - HTTP, FTP, SMTP, POP3, IMAP, Telnet 등과 같은 프로토콜이 있음
    - 통신패킷들은 해당 프로토콜에 의해 처리 
    - 우리가 사용하는 응용프로그램(브라우저, 메일..)은 위의 프로토콜을 쉽게 사용하게 해주는 것



</br></br></br>

### 4. 프로토콜의 기능 
- 단편화(Fragmentation)와 재합성(Assembly)
- 캡슐화(Encapsulation)
- 연결 제어(Connection Control)
- 흐름 제어(Flow Control)
- 오류 제어(Error Control)
- 순서 결정(Seuencing)
- 주소 설정(Addressing
- 다중화(Multiplexing)
- 전송 서비스(Transmission Service)
  




</br></br></br></br></br>

참고
- https://velog.io/@dbwlgns98/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-CS%EC%A0%95%EB%A6%AC-1%ED%83%84
- https://computer-science-student.tistory.com/377

