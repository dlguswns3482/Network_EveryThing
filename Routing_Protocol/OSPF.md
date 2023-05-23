## OSPF란❓

- Link-State 라우팅 프로토콜
- 최적의 경로를 계산할 때 SPF(Shortest path First) 또는 다익스트라(dijkstra) 알고리즘을 이용하여 각 목적지 까지의 최적 경로를 계산
- Metric은 Cost를 사용
- Multicast를 사용하여 정보를 전달한다.
    - 224.0.0.5 (DR이 DROTHER에게 전송할 때 사용)
    - 224.0.0.6 (DROTHER가 DR에게 전송할 때 사용)
- AD값은 110을 사용한다.

## OSPF의 장점

1. OSPF는 area 단위로 구성되어 대규모 네트워크를 안정되게 운영할 수 있음
    1. 특정 area에서 발생하는 상세한 라우팅 정보가 다른 area로 전송되지 않아 큰 규모에서 안정되게 운영할 수 있다. (재분배를 통해서 다른 area로 전송 가능)
2. Stub 이라는 강력한 축약기능 지원
    1. 기존 라우팅 프로토콜과는 달리 IP주소가 연속되지 않아도 Routing Table의 크기를 줄일 수있음.
3. 표준 라우팅 프로토콜
4. Convergence Time이 전반적으로 빠른 편이다.
    1. 네트워크의 상태를 수렴하고 이러한 변화가 반영된 라우팅 테이블을 만드는데 걸리는 시간

## OSPF의 네트워크 분류

- 각각 동작 방식 및 설정이 다르다.
- 밑에는 없지만 Point-to-Access 네트워크가 하나 더 있다.


### 1. BroadCast Multi Access

- 하나의 Broadcast 패킷을 전송할 경우 동일 네트워크 상의 모든 네트워크 장비에게 전달되는 네트워크. → BroadCast 네트워크
- 하나의 인터페이스를 통해 다수의 장비와 연결된 네트워크 → Multi Access 네트워크
- Broadcast나 Multi Access를 사용해서 하나의 Paceket만 전송해도 모든 장비에게 전달됨



### 2. Non Broadcast Multi Access (NBMA)

- Broadcast가 지원되지 않는 Multi Access 네트워크를 의미한다.
- 대부분 내부에 Virtual Circuit(가상회로) 방식을 사용한다.
- NBMA 에서는 Broadcast로 Packet을 전송할 경우에는 가상회로 하나당 하나씩 보내야함.



### 3. Point-to-Point

- 하나의 인터페이스에 연결된 장비가 하나뿐인 네트워크
    - ex) HDLC, PPP, Point-to-Point 등등



## OSPF의 동작과정

### 1. DR/BDR 선출

1. OSPF Priority가 가장 높은 라우터가 DR로 선출된다 (그 다음 높은게 BDR 선출)
2. OSPF Priority가 같은 경우 Router-ID가 높은것이 DR이 된다.
3. DR, BDR이 선출된 후에 더 높은 순위의 라우터가 추가되어도 DR, BDR이 변경되지 않는다. 
    - (단, 재부팅하거나 clear ip ospf process 명령어 사용 시 변경됨)
4. DR이 다운될 경우 BDR이 DR이 되고 다시 BDR을 선출함 
    - (DR과 BDR이 아닌 라우터를 DROTHER라고 함)
    
   