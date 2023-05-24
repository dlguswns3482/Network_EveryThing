# EIGRP 동적 라우팅 프로토콜이란 ?

- Distance Vector + Link-State 하이브리드 동적 라우팅 프로토콜
- Cisco에서 제작한 Cisco 전용 프로토콜
- DUAL(Diffusing Update Algorithm) 알고리즘 사용하여 최적경로와 후속경로 선출
- Router 정보 전송을 위해 IP 프로토콜 88번 사용
- AD 값은 내부 90, 외부 170이다.
    - 목적지가 같은 경로가 있을 때 사용되는 우선순위
- AS(Autonomous System) 단위로 구성
    - AS = 독립적인 네트워크
- Classless Routing Protocol

## EIGRP의 장점😁

- Fast Convergence  - 빠른 수렴
- Unequal Cost - 부하분산 (RR) 지원
- OSPF에 비해 설정이 간단하다

## EIGRP의 단점😅

- Cisco 전용 장비이므로 Cisco 장비에서만 동작한다.
- 대규모 네트워크에서 사용하기 좀 그렇다 ㅠ (SIA 현상 발생할 수 도 있음)
    - SIA 현상이 무엇인가요 ❓
    - **네트워크 장애 등으로 인하여 이웃 라우터에게 Query 패킷을 전송한 후 답장 패킷을 장기간 수신받지 못하는 상태**


1. Hello Message
    1. 일정 시간동안 답장이 없으면 장애 포트라고 생각하고 연결을 끊음.
2. Update Message
    1. 자신의 라우팅 정보를 넘겨준다.
3. Ack 응답
    1. 라우팅 정보 잘 받았다고 답장함.
4. Topology Table
    1. 받은 라우팅 정보를 토폴로지 테이블에 저장함
5. Update Message
    1. 자신의 라우팅 정보를 넘겨준다.
6. Topology Table
    1. 자신의 토폴로지 테이블에 라우팅 정보를 저장한다.
7. Ack 응답
    1. 라우팅 정보 잘 받았다고 답장한다.
    

## 라우팅 경로 계산하는 방식 🛣️

1. Hello Packet을 인접 Router에게 뿌리고 Neighbor를 맺은 후 Neighbor 테이블을 생성한다.
2. Update Packet을 통해 라우팅 정보를 교환해서 Topology Table을 생성한다.
3. Topology Table 정보를 종합하여 라우팅 경로를 계산하고 Best Path를 라우팅 테이블에 저장.

## DUAL(Diffusing Update Algorithm)이란❓

- EIGRP가 최적의 경로를 계산할 때 사용하는 알고리즘.

1. FD (Feasible Distance) - 출발지 라우터 에서 목적지 네트워크까지 계산한 EIGRP Metric 값       (최적 Metric)
2. AD (Advertised Distance) - 출발지 Next-hop 라우터에서 목적지 네트워크까지 계산한 EIGRP Metric 값 (RD라고도 한다.)
3. Succesor - FD값이 가장 낮은 경로상의 Next-hop 라우터 (즉, 최적 경로상의 Next-hop 라우터가 됨)
4. Fesable Succesor - 최적 경로(Successor)가 동작하지 못할 때 Query 또는 계산 없이 바로 Routing table에 등록되는 경로 (후속 경로상의 next-hop 라우터)

- 목적지 네트워크까지 FD값이 가장 낮은 경로가 Successor (최적경로)로 선출되고 남아있는 경로 중 AD값이 FD값보다 작은 경우 Feasible Successor (후속경로)로 선출 된다.