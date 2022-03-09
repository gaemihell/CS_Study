<!-- @format -->

# Reliable Data Transfer

데이터 전송에서 reliable 하다는 것은

1. packet error X
2. packet loss X
3. sequence error X

를 의미한다.

즉 reliable한 채널에선 **_데이터 손상 및 손실 X_**, **_데이터는 전송된 순서대로 전달됨_** 을 보장하는 것이다.

<p align="center">
    <img src="./img/unreliable-channel-below.png" width="300px">
</p>

하지만 이러한 작업들은, reliable transfer protocol의 하위 계층이 신뢰적이지 않으므로 구현하기가 어렵다.

어떻게 하위 계층에서 받은 데이터가 reliable 하다고 보장할 수 있을까?

# Reliable Data Transfer 원리

### rdt 1.0

하위 채널이 reliable 하다고 가정하였다.

하위 채널이 reliable 하므로 각각 send, recv를 기다리면 되고 피드백도 제공할 필요가 없다!

### rdt 2.0

하위 채널에서 packet error가 발생한다고 가정하였다.

packet loss와 sequence error는 발생하지 않는다고 가정한다.

packet error를 다루기 위해선 다음 3가지 부가 프로토콜 기능이 필요하다.

- **Error Detection**  
   Error Detection의 경우 receiver가 검출할 수 있게 checksum bits를 추가하여 구현한다.
- **Feedback**  
  sender가 error 발생 여부를 알 수 있게 하기 위해 Feedback이 필요하다.
  ACK(ACKnowledgements) 와 NAK(Negative AcKnowledgements) 응답을 이용하여 구현한다.

  데이터가 손상되었다면 NAK 응답을 받을 것이고, 잘 도착했다면 ACK응답을 받을 것이다.

- **Retransmission**  
  만약 packet error가 발생했다면, NAK응답을 받을 것이고, NAK응답을 받게 되면 재전송해주는 과정이 필요하다.

위에 기술된 부가 프로토콜들을 적용하게 되면, packet error 처리는 꽉잡아놓는 느낌이 든다.

하지만, ACK, NAK packet도 error가 발생할 수 있다.

receiver가 ACK를 응답으로 보냈는데, error가 발생하여 sender에게 NAK으로 도착하게 된다면 재전송이 이루어 질 것이고, 잘못된 데이터들이 receiver에 도착하게 될 것이다.

이를 어떻게 하면 방지할 수 있을까?

### rdt 2.1

rdt 2.1에선 ACK, NAK packet error가 발생하여 이미 전달된 데이터가 다시 전달이 되어도 새로운 데이터인지 이미 받았던 데이터인지를 구분할 수 있게 sequence number를 추가하여 rdt 2.0의 문제를 해결하였다.

이제 packet error가 발생하여도 잘 처리할 수 있고 ACK, NAK에 에러가 발생하여 잘못 전달 되어도 잘 처리할 수 있다.

지금까지는 packet loss가 없다고 가정하여서 문제를 해결하였다.
ACK packet이 아예 손실되어 오지 않는다면 어떻게 해야할까?
rdt 2.1 프로토콜로는 해결할 수 없다.

### rdt 2.2

ACK, NAK 둘다 쓸 필요 없고, 잘 받은 packet에 대해서만 ACK를 주는 식으로 변경

### rdt 3.0

rdt 3.0에선 packet loss 를 해결하기 위해 timer를 사용하여 일정 시간이 지났음에도 ACK가 오지 않으면 손실되었다고 판단, 재전송하기로 하였다.

<p align="center">
    <img src="./img/rdt3-packet-loss.png" width="300">
    <br />
    packet loss
</p>
<p align="center">
    <img src="./img/rdt3-ack-loss.png" width="300">
    <br />
    ack loss
</p>

#### 정리

- packet error -> ACK packet으로 해결
- ACK error -> sequence number로 해결
- packet loss -> timer로 해결

# pipelined reliable data transfer protocol

추가 예정

# Go-Back-N

추가 예정

# Selective Repeat

추가 예정
