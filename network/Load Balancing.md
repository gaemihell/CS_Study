# 로드 밸런싱(Load Balancing)

사용자 수가 많아지면 아무리 성능이 뛰어난 서버라고 해도 모든 트래픽을 감당할 수 없다. -> 서버를 추가로 구비하고 여러 대의 서버에 동일한 데이터를 저장해 효과적으로 트래픽을 분산시킨다. -> 이 때 트래픽을 여러 대의 서버로 분산해주는 기술이 필요하다. -> 이 기술이 로드 밸런싱이다.

<p align="center">
  <img src="./img/load-balancer-arc.jpg">
  <br />
  로드밸런서의 아키텍처
</p>

## Scale-up 그리고 Scale-out

<p align="center">
  <img src="./img/loadbalancing-scale.jpg">
  <br />
  Scale-up과 Scale-out
</p>

증가한 트래픽에 대처할 수 있는 방법은 `Scale-up` 과 `Scale-out` 두 가지가 있다.

- `Scale-up` : 서버 자체의 성능을 확장하는 것. 비유하자면 i3 CPU를 갖고 있는 컴퓨터를 i7 CPU로 업그레이드 하는 것이다.
- `Scale-out` : 기존 서버와 동일하거나 낮은 성능의 서버를 두 대 이상 증설하여 운영하는 것. 그러니까 서버 컴퓨터의 개수를 늘리는 것이다.

`Scale-out` 방식으로 서버를 증설하려면 트래픽을 여러 컴퓨터로 분산 시켜줘야 한다 -> **로드 밸런싱이 반드시 필요하다.**

## 로드 밸런서가 서버를 선택하는 알고리즘

- Round Robin : 서버에 들어온 요청을 순서대로 돌아가며 배정하는 방식. 클라이언트의 요청을 순서대로 분배하기 때문에 여러 대의 서버가 동일한 스펙을 갖고 있고, 서버와의 연결(세션)이 오래 지속되지 않는 경우에 활용하기 적합하다.

- Weighted Round Robin(가중 라운드 로빈) : 서버마다 가중치를 매기고 가중치가 높은 서버에 클라이언트의 요청을 우선적으로 배분한다. 주로 서버 트래픽 처리 능력이 상이한 경우 사용하는 분산 방식이다.

- IP Hash : 클라이언트 IP 주소를 특정 서버로 매핑하여 요청을 처리하는 방식. 클라이언트 IP를 해싱하기 때문에 사용자가 항상 동일한 서버로 연결되는 것을 보장한다.

- Least Connection (최소 연결 방식) : 요청이 들어온 시점에 가장 적은 연결상태를 보이는 서버에 우선적으로 트래픽을 배분한다. 자주 세션이 길어지거나 서버에 분배된 트래픽들이 일정하지 않은 경우에 사용하기 좋다.

- Least Response Time(최소 리스폰타임) : 서버의 현재 연결 상태와 응답시간을 모두 고려하여 트래픽을 배분한다. 가장 적은 연결 상태와 가장 짧은 응답시간을 보이는 서버에 우선적으로 로드를 배분하는 방식이다.

## 로드 밸런서의 종류

L4, L7은 내일

### 참고 링크

[가비아 포스트](https://m.post.naver.com/viewer/postView.nhn?volumeNo=27046347&memberNo=2521903)
[DevlopersIO](https://dev.classmethod.jp/articles/load-balancing-types-and-algorithm/)