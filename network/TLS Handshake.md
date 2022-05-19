# TLS Handshake

넷보 시험을 복습도 할겸 중요한 것중 하나인 TLS HandShake에 대해서 알아보겠습니다.

## TLS(Transport Layer Secret)

TLS는 개인 정보 보호 및 안전한 전송을 위해 암호화하는 프로토콜이다. TCP와 UDP와 같은 일반적인 인터넷 통신에 안전한 계층을 추가하는 방식이고, 이 기술을 구현하기 위해 웹 서버에 설치하는 것이 SSL/TLS 인증서다.

<p align="center">
  <img src="./img/ssl.jpeg">
  SSL/TLS가 적용되는 구조
  <br />
</p>

그림에서와 같이 SSL/TSL 인증서는 Transport Layer에서 적용되는 보안 프로토콜이다. TCP 위에 존재하며, 이 프로토콜은 CA와 PKI를 이용한다.

### TLS를 사용하는 이유

우리가 통신을 할때, 대칭 키를 이용하여 암호화를 하는데, 이 대칭키를 나눌 때 비대칭 키 암호화를 사용해서 나눈다. 그렇다면 어떻게 비대칭 키 암호화를 사용하여 안전하게 나눌 수 있을까? 이 생각에서 시작된 프로토콜이다.

즉, 어떻게 비대칭키를 안전하게 나누어서 사용할지 정의하는 프로토콜이다. CIA를 만족하기 위한 프로토콜.

#### 깨알 복습

- 대칭 키, 비대칭 키를 섞어서 사용하는 이유? : 비대칭 키는 주고받는게 정말 안전하지만, 매번 사용하기에는 정말 느리다. 대칭키는 빠르지만 주고 받는 것이 안전하지 못하다. 그래서 이 장점을 섞기 위해 대칭키를 안전하게 나누기 위해 비대칭 키를 이용하는 것이다.

## TLS 메커니즘

TLS는 이 3가지 메커니즘을 기반으로 하고 있다. 이 3가지 프로토콜이 TLS의 가장 기본적인 동작이다.

1. Cipher Suite Negotiation

   - Cipher Suite란, 암호화 Fucntions and Techinques의 모음이다.
   - Cipher Suite에 들어 있는 정보들 : 키 교환 알고리즘(DH), 인증 알고리즘(RSA), 데이터 암호화 알고리즘(DES, 3DES, AES), 데이터 무결성 알고리즘(SHA 시리즈)

<p align="center">
  <img src="./img/ciphersuite2.png">
  <br  />
  Cipher Suite의 구성
</p>

2. Authentication

   - 인증서로, 두 가지 방식의 서명에 기반을 하고 있다.
   - 올바른 개인키를 사용하여 올바른 pre-master secret을 사용할 수 있게끔 보장하기 위한 것이다.
   - RSA : 소인수분해의 어려움을 기반으로 하고 있는 공개 키 시스템
   - ECDSA : 타원곡선 기반으로 만든 디지털 서명

3. Key Exchange

   - RSA 교환과, DH Key교환을 사용하고 있었으나, TLS 1.3부터는 DH Key 교환만 사용하고 있다.
   - 안전하게 pre-master secret만 전달되면, 그 다음부터는 서버와 클라이언트가 동일한 키로 통신할 수 있게 된다.
   - Finished : K값을 구했으니, K값으로 해싱해서 보낸다는 것을 확인시켜주는 것

## HandShake 과정

<p align="center">
  <img src="./img/tls.jpeg">
  <br  />
  TLS HandShake 1
</p>

이 과정을 조금 더 직관적으로 나타내면 아래 그림과 같다.

<p align="center">
  <img src="./img/tlshandshake.webp">
  <br  />
  TLS HandShake 2
</p>

TLS HandShake는 그림에서와 같이 TCP 3 Way HandShake(파란색)를 통해 TCP 연결이 열린 후에 발생한다.

1. 클라이언트가 서버에 패킷을 전송하면서 HandShake를 시작합니다. 클라이언트가 사용 가능한 Cipher Suite 목록, Session ID, SSL Protocol Version, Random Byte 등을 전달합니다. 아래 사진을 보면 Client가 사용 가능한 Cipher Suite를 Server에 제공하는 것을 볼 수 있습니다.

<p align="center">
  <img src="./img/ciphersuite.jpeg">
  <br  />
  Clienthello Packet
</p>

2. Clinet가 보내온 패킷에서 Cipher Suite 중 하나를 선택한 뒤에, Client에게 이를 알리는 Server Hello Packet을 보냅니다.또한 자신의 SSL Protocl Version 및 인증서도 같이 보냅니다. 아래 사진을 보면 아까는 여러개 였던 Cipher Suite가 하나로 선택된 것을 볼 수 있습니다.

<p align="center">
  <img src="./img/serverhello.png">
  <br  />
  Serverhello Packet
</p>

3. Server가 보낸 SSL 인증서를 Client가 검증합니다. 인증서 내부에는 Server가 발행한 공개키가 들어 있습니다. 따라서 Client는 Server가 보낸 SSL 인증서를 CA 공개키를 사용하여 복호화 합니다.(서버의 인증서는 당연히 CA 개인키로 암호화 되어있을 것입니다.) 복호화 함으로써 인증서를 검증하게 되는 것입니다.

<p align="center">
  <img src="./img/certificatepacket.png">
  <br  />
  Certificate Packet
</p>

4. 클라이언트는 `예비 마스터 암호(Pre-master Secret)` 이라고 하는 무작위 바이트 문자열을 전송합니다. 아까 받은 서버 인증서의 공개키로 암호화하여 전송합니다. 서버와 클라이언트는 클라이언트 무작위 바이트, 서버 무작위 바이트, 그리고 예비 마스터 암호를 이용해 세션 키를 생성합니다. 모두 같은 결과가 나와야 합니다.

5. 클라이언트는 암호 사양 변경 알림을 서버에 보내 클아이언트가 메세지를 암호화하는데 새로운 세션 키 사용을 시작함을 나타내고, 클라이언트 완료 메세지를 보냅니다.

6. 서버는 암호 사양 변경을 수신하여 세션 키를 사용하기 시작하며 대칭 키 암호화로 전환합니다. 서버는 클라이언트에 서버 완료 메세지를 보냅니다.

이러면 TLS HandShake가 완료되어, 설정한 보안 채널을 통해 데이터를 암호화하여 안전하게 교환할 수 있게 됩니다.

# Reference

홍익대학교 이윤규 교수님의 네트워크 보안 강의 및 PDF

https://www.cloudflare.com/ko-kr/learning/ssl/what-happens-in-a-tls-handshake/

https://www.itworld.co.kr/news/113007

https://aws-hyoh.tistory.com/entry/HTTPS-통신과정-쉽게-이해하기-3SSL-Handshake

https://tlseminar.github.io/first-few-milliseconds/
