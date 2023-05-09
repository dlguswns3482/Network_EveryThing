# **TCP Selective Acknowledgments (SACK)**

## **일반적인 TCP를 통한 Data 전송 Flow**

- Client 에서 Server로 request를 보내고, 이에 대한 답으로 Server에서는 4개로 나누어진 TCP segments를 Client로 되돌려 준다.
- 하지만 두번째 packet이 drop된 상황이다.

1.  Segment #2가 손실되었다.
2.  Client는 Segment #3을 받았다. 하지만 Segment #2가 누락된 것을 알게되고 Server에 Segment #1의 ACK를 2번 보내어 Segment #2의 손실을 Server쪽에 알린다.
3.  아직 Server쪽에서는 Client로 부터 중복된 Segment #1의 ACK를 못받은 상태인지라 계속 다음 Segment인 Segment #4를 전송한다. 하지만 Client는 아직 Segment #2를 못받았으므로 다시 Segment #1의 ACK를 전송한다.
4. Server가 Client로 부터 중복된 Segment #1의 ACK를 받았다.이에 Segment #2부터 이후 #3,#4에 대해 다시 재전송한다. 두번째로 전달된 중복된 Segment #1의 ACK는 무시된다.
5. Client가 나머지 Segment를 전송받고, ACK도 정상적으로 전송한다.

- 2번이 손실되었는데 3,4번도 재전송되는 불필요한 전송이 일어난다.

---

## **Selective ACK이 적용된 TCP를 통한 Data 전송 Flow**

1. Segment #2가 손실되었다.
2. Client는 segment #1과 #3사이가 누락되었음을 확인하고, segment #1에 대한 duplicated ack을 전송한다.
    
    (단, 이전과 다르게 해당 duplicated ack에 segment #3은 전송받았다고 SACK option을 통해 표시한다.)
    
3. Server가 아직 duplicated ACK을 받기 전이라 segment 4를 Client로 전송하게 되는데

Client는 segment #3을 받았을 때와 마찬가지로 segment #1에 대한 duplicated ack을 보낼 때 segment #3, #4를 받았다고 표시하고 ack을 전송한다.

1.  이후 server는 segment #1에 대한 duplicated ACK을 전달받고, segment #3이 포함된 SACK를 받게 되는데 이를 통해 segment #2가 누락된 것을 확인하고 segment #2를 재전송하게 된다.
    
    이후 한번 더 전송받은 segment #1에 대한 dupplicated ACK(SACK #3, #4) 는 내용상 더 전송할게 없으므로 추가 동작은 없다.
    
2. Client는 segment #2를 전송받게 되고, 모든 segment 를 전송받았다는 의미로 segment #4에 대한 ACK를 server로 전송한다.