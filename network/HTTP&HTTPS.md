# HTTP & HTTPS

HTTP와 HTTPS 가 무엇이고 차이가 무엇인지 알아봅시다.

<p align="center">
  <img src="./img/HTTP&HTTPS.png">
  <br  />
  HTTP와 HTTPS
</p>

## HTTP(Hyper Text Transfer Protocal)

- 웹 서버와 클라이언트 간의 문서를 교환하기 위한 통신 규약
- 웹에서만 사용하는 프로토콜이다.
- 텍스트 교환이므로, 누군가 네트워크에서 신호를 가로채면 내용이 노출될 수 있다.
- TCP/IP 기반으로 서버와 클라이언트 간의 요청과 응답을 전송한다.
- 사용자의 요청 하나가 들어오면 하나의 응답을 하는 방식이다. -> 서버가 먼저 응답하지 않는다.
- 비연결 지향적이다.(사용자의 요청으로 서버와 접속하여 요청에 대한 응답 데이터를 전송 후, 연결을 종료한다.)
  - 간단하고 자원이 적게든다.
  - 연결이 지속적이지 않기 때문에 연결 종료 후 추가적인 요청시 어떤 사용자의 요청인지 모른다.
  - 여러 사용자가 요청할 시 요청을 구분할 수 없어서 제대로 된 응답 데이터를 전송할 수 없다.
  - 해결 방법 : `Cookie`, `Session`, `Hidden Form Field` 등

## HTTPS(Hyper Text Transfer Protocal Secure)

- 이름에서 알 수 있듯이 HTTP + Secure
- 인터넷 상에서 정보를 암호화하는 TLS/SSL 프로토콜을 사용해 클라이언트와 서버가 자원을 주고 받을 때 사용하는 통신 규약.
- HTTPS는 데이터를 암호화해서 전송하기 때문에, 누군가 신호를 가로채도 해독할 수 없다.

### 대칭 키, 비대칭 키 암호화

**대칭 키 암호화 방식**

- 암호화와 복호화에 같은 키를 사용한다.(공유키)
- 발송자-수신자가 대화를 하려면 둘 다 공유키를 갖고 있어야 한다.
- 그렇다면 공유키를 언젠가 전달 해야함 -> 전달하는 과정에서 키가 유출될 위험이 있다.

**비대칭 키 암호화 방식**

- 공개 키와 비공개 키가 존재 한다. 비공개 키로 암호화를 하면 공개 키로 복호화할 수 있고(거의 사용하지 않는다.), 공개 키로 암호화하면 비공개 키로 복호화 할 수 있다.
- 대표적인 암호화 방식은 RSA
- 처리 알고리즘이 대칭키 보다 느린 단점이 있다.

### 그렇다면 HTTPS의 암호화 방식은 어떻게 될까?

<p align="center">
  <img src="./img/https.png">
  <br  />
  HTTPS 암호화 방식 
</p>

데이터의 암호화에는 대칭 키 암호화 방식을 사용한다.
공유키 교환에는 비대칭 키 암호화를 사용하여 처리 속도가 느린 문제를 해결하고 있다.

1. 서버는 서버가 제공한 공개 키와 증명서에 부합하는 요청을 클라이언트가 보냈는지를 확인합니다. 클라이언트가 공통 키를 서버가 제공한 공개 키로 암호화해 서버에게 보낸 첫 번째 요청을 복호화 하는 과정을 `Handshake` 라고 한다. 이 과정이 끝나면 실제 요청과 정보를 교환하는 과정이 이어진다.
2. 서버가 제공하는 비대칭 키 공개 키를 사용하여 클라이언트는 서버에게 보낼 공통 키를 암호화한다.
3. 서버는 클라이언트가 보낸 암호화된 요청을 비대칭 키 개인 키를 사용하여 복호화한다.
4. 결론 : 클라이언트-서버는 서버가 제공한 비대칭 키를 통해 암호화된 공통 키로 통신한다.

## SSL 디지털 인증서

- SSL(Secure Socket Layer)와 TLS(Transport Layer Security)는 같은 것이라고 볼 수 있다.
- SSL은 TCP/IP 암호화 통신에 사용되는 규약으로써 넷스케이프에서 만들었다. SSL 3.0 버전부터 IETF에서 표준으로 정해서 TLS 1.0이 되었다. 하지만 보통 SSL로 많이 불린다.

### 인증서의 장점

- 클라이언트가 접속하려는 서버가 신뢰할 수 있는 서버인지 확인 가능하다.
- SSL 통신에 사용할 공개키를 클라이언트에게 제공한다.
- 통신 내용이 노출, 변경되는 것을 방지한다.

### 참고자료

[HTTP, 그리고 HTTPS의 이해](https://blog.wishket.com/http-그리고-https의-이해/)

[HTTPS가 동작하는 방식](https://dailyscat.gitbook.io/twis/network/https)