## RIP란 ?

- `Routing Information Protocol`의 약자로, 네트워크 엔지니어가 일일이 패킷의 전송경로를 정하지 않고 알아서 찾아가는 동적 라우팅 방식 중 디스턴스 벡터 라우팅 방식 프로토콜이다.
- 오로지 거리, 방향을 기준으로 패킷정보를 전송한다.

## RIP의 특징

1. AS를 구성하는 내부용 라우팅 프로토콜이다.
2. 경로를 설정하는 기준은 거리 카운터로서 15개까지만 허용된다.
3. 디폴트 라우팅 업데이트 시간 기준은 30초이다. 이때, 라우팅된 정보가 갱신된다.
4. RIP에 설정된 네트워크는 Classful하게 들어간다.
    1. EX) 150.19.125.0 → 150.19.0.0으로 들어간다.
5. RIP은 180초 동안은 상대측으로부터 정보를 받지 못해도 기다린다. (Invalid Time)
    
    하지만 180초가 지나도 정보를 받지 못하면 Hold Down 상태가 된다. (possibly Down 표시)
    
    그 이후 1분동안도 정보를 못 받으면 그 경로가 죽었다고 생각하고 라우팅 테이블에서 이 경로에 대한 정보를 지운다. (Flush Time)
    

## Administrative Distance란 ?

- Distance 값을 Administrative Distance 라고 한다.
- 라우팅 정보에 대한 신뢰성을 뜻한다.
- 이 값은 적으면 적을수록 라우터는 그 경로를 신뢰한다.
    - Static Routing 경로는 1이다.
- 라우터는 DIstance값이 더 작은 경로로 패킷을 보내게 된다.

## Cost 란 ?

- Cost란 Show ip route 명령어를 입력하면 [120/1]이 나온다.
- 여기서 1이 Cost이다. (120은 Distance 값이다.)
- RIP에서는 Cost가 Next Hop이므로 라우터 한개 떨어져서 목적지가 있다는 뜻!

## RIP의 장점

```
장점

    1. 소규모 네트워크 상에서 효율적이다.(자원낭비가 덜함.)
    2. 비교적 구성이 쉬운편이다.
    3. 거의 모든 회사의 라우터에서 지원한다.
    4. cisco라우터의 경우 4개에서 6개의 라우터까지 로드밸런싱을 허용한다.
    4-1. 로드밸런싱 : 패킷을 여러 경로로 나누어서 보낼 수 있음.
    4-2. 로드밸런싱으로 부하 분산 처리를 할 수 있다.

```

## RIP의 단점

```
단점

1. 홉 수가 16개 이상이면 네트워크를 찾지못하여   데이터를 보내지 못하므로 대규모 네트워크 환경에서는 사용하기 부적합하다.

2. 속도나 거리 지연을 고려하지 않아 최적의 경로 선정에 비효율적일 수 있다.

3. 전체 경로를 담은 라우팅테이블들을 브로드캐스트 함에 따라 과도한 트래픽이 부하된다.

4. 모든 라우터들 사이에서 동기화를 해주지 않으면 패킷의 경로가 부적합하게 잡힐 수 도 있다.

5. 30초 간격으로 주기적인 업데이트를 함으로 몇 개만 지나도 수 분이 소모된다.

```

## RIP의 무한루프를 극복하는 방법

```
무한루프를 극복하는법

1. 최대 홉 수를 15로 늘린다.

2. Split-Horizon : 데이터를 광고한곳에서는 광고받지 않는다. 즉, 자신이 보낸 정보는 되돌려 받지 않고 단방향으로 전송된다.

3. Poison-Reverse : 16이라는 홉의 라우팅 값을 받으면 역으로 이 라우터 고장났다고 알려주는 기능이다.

4. Holddown-Timers : 특정 연결 구간에서 라우터가 Fail 신호를 받을 경우 바로 없애지 않고 사실여부를 확인한 후 삭제한다. 이로써 연결 구간에 문제로 네트워크가 불안정할때 잘못된 데이터가 들어와서 전체적인 네트워크가 마비되는 현상을 막아준다.

5. Triggerd-Update : 토폴로지의 변화를 이웃한 라우터에게 알려준다.

```

## RIPv1 vs RIPv2

### RIPv1

```
RIPv1

1 : Classful Routing Protocol

1-1 : A,B,C 처럼 규격화된 IP를 기준으로 라우팅을 한다. 따라서 서브넷의 정보가 붙어있지 않으므로 정보의 크기가 크다.

1-2 : VLSM 지원 안함

? VLSM이란

?: 서브넷의 서브넷. 이미 나누어져 있는 서브넷을 가상의 Prefix로 나누어서 사용한다. 이것이 지원이 되면 /24라는 서브넷의 실제사용하는 서브넷이 2개이면 나머지 것들을 또 나누어서 사용할 수 있어서 절약적이고 지원되지 않는다면 클래스를 통쨰로 나누어야 해서 굉장히 비효율적이다.

2. 인증기관을 지원하지 않음

3. BroadCast를 통해서 광고한다.

4. 자동 축약이 불가능하다.

```

### RIPv2

```
1. Classless Routing Protocol

1-1. 서브넷의 정보와 함께 전송하기 때문에 정보의 크기가 크지않음.

1-2. VLSM을 지원함.

2. Plain Text or MDS 인증을 지원함.

3. Multicast를 통해 광고한다.

4. 자동축약이 가능하다.

```