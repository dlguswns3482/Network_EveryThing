# FTP vs TFTP

## FTP

- File Transfer Protocol로 인터넷상에서 컴퓨터 사이의 파일을 전달하는 데 사용되는 프로토콜.
- TCP 기반 프로토콜이다.

## TFTP

- Trivial File Transfer Protocol로 FTP와 마찬가지로 파일을 전송하기 위한 프로토콜이다.
- 하지만 FTP보다 더욱 단순한 방식으로 파일을 전송할 수 있다.
- UDP 기반 프로토콜이다.

| FTP  | TFTP |
| --- | --- |
| TCP 기반 | UDP 기반 |
| 20,21번 Port Number 사용 | 69번 Port Number 사용 |
| 로그인 절차를 거친다.  | 로그인 절차를 거치지 않는다.  |
| 파일 디렉토리를 볼 수 있다. (DIR) | 파일 디렉토리를 볼 수 없다.  |

---

## FTP 프로토콜의 동작 원리

- 호스트간 두 개의 연결 설정이 필요하다.
    - 데이터 전송 연결. 실질적으로 데이터가 지나다니는 포트 (포트 20번)
    - 명령과 응답 등의 제어 연결. FTP를 담당하는 포트 (포트 21번)

### 종류

- 공개 FTP - 누구나 접속해서 다운로드가 가능하다.
- 비공개 FTP - 계정과 비밀번호가 필요하다.
- FTP는 Active Mode와 Passive Mode로 나뉜다.

### Active Mode

![Untitled](https://1.bp.blogspot.com/-WBjojdH1bfw/W5EZEGlXsLI/AAAAAAAAAPY/6NRa-Q-tK9IJe9iNFzaeEy0420x9HpBNACLcBGAs/s400/2.png)
1. Server에는 20번 포트와 21번 포트가 있다. Client에는 1023이 넘는 임시포트 2가지를 사용함. 
    1. 1023이 넘는 이유는 Well-known Port를 사용하면 안되기 때문이다.
    2. 20번 포트는 데이터가 이동하는 포트이고 21번 포트는 명령어를 수행하는 포트이다.
2. Clinet의 임시포트인 1029포트에서 Server의 21포트에 접근한다. 
3. Client는 1029포트에서 21포트로 자신의 Data Channel인 1030포트 번호를 알려준다.
4. 서버에서 21번 포트는 Client에서 포트 번호를 응답 받았다고 ACK 메시지를 보낸다.
5. 그 다음, 서버의 Data Channel을 열어 20번 포트에서 1030으로 데이터를 보낸다. 
6. 1030포트는 Data를 정상적으로 수신했다는 ACK응답을 보낸다. 

### Passive Mode

![Untitled](https://3.bp.blogspot.com/-A_nxbm7dirk/W5EZ4TJVyCI/AAAAAAAAAPg/A65pFFNAr4smHb0DuTW6sJaW4MCwqf_uQCLcBGAs/s400/2.png)
1. Client의 임시 포트인 1029포트에서 Server의 21포트에 수동적으로 접근한다. 
2. Server의 21번 포트는 자신의 임시 포트인 2031포트를 Client에게 알려준다.
3. Client는 Server로부터 알려진 2031포트에 접속을 하고 메시지를 보낸다. 
4. Server에서는 접근 성공과 메시지 전송을 성공하면 ACK 응답 메시지를 보낸다. 

## Active mode와 Passive mode의 차이점

- Active mode는 Server에서 포트를 20번을 사용한다.
- Passive mode는 Server에서 포트를 임의지정해서 사용한다.
- Active mode는 Server에서 Client 포트로 접근한다.
- Passive mode는 Client에서 Server로 접근한다.