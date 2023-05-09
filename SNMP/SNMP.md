# SNMP

## SNMP - Simple Network Management Protocol란❓

```markdown
SNMP는 IP 네트워크 상의 네트워크로부터 정보를 수집 및 관리하며, 장치의 동작을 변경하는데 사용되고 정보를 모니터링 하게 도와주는 인터넷 표준 프로토콜이다. 
```

- EX) Router, Switch, Server, Workstation, Printer 등이 SNMP를 지원한다.
- SNMP는 네트워크 장비의 성능과 핵심 기능의 상태/기능 정보를 저장하고 관리할 수 있는 프로토콜이다.
- 또한 SNMP를 사용하여 장비의 설정을 수정할 수도 있다.

```markdown
SNMP Port : 161번
```

## SNMP가 하는일

![Untitled](https://snmpsimulator.files.wordpress.com/2017/01/snmp.png)
- SNMP를 지원하는 컴퓨터 혹은 장비라면 SNMP를 이용해 모니터링 할 수 있다.
- SNMP에서는 주로 Manager / Agent로 나뉜다.

### Manager

- 장비의 정보를 수집하는 하드웨어/소프트웨어를 의미한다.
- Manager는 실제 장비의 정보를 수집하는 하드웨어/소프트웨어 이므로 NMS라고도 불린다.
- NMS :SNMP를 활용하여 네트워크 장비의 정보를 상시 수집하여 장애 발생시 사용자에게 알림.

### Agent

- 정보를 제공하는 주체인 네트워크 장비를 의미한다.

---

# SNMP Version

- 딱히 많이 차이가 나지는 않고 보안성을 기르기 위해 업데이트를 한것이다.
- 여기서 보안은 Community String(커뮤니티 값)의 보안 취약성이다.

# Community String

- Manager(NMS)와 네트워크 장치 간 인증을 위한 값이다.
- NMS는 해당 장비를 관제하려면 장비에 설정된 커뮤니티 값을 평문(String)으로 보낸다. (Password와 같은 개념)
- 만약 이 장치에 있는 커뮤니티 값과 다르면 관제를 거부한다.

---

# SNMP Version (2)

### SNMPv1

- SNMP 최초 버전.
- 커뮤니티 값을 이용해 NMS와 Agent 간 인증을 수행한다.
    - 하지만, 커뮤니티 값은 평문(String)으로 전달되므로 보안에 취약하다.
    - 장비 정보 값 수집도 대량 수집 요청이 불가능하다.
    - 요즘에는 전혀 사용되지 않는 버전이다.

### SNMPv2 / SNMPv2c

- SNMPv1에서 보안 취약점과 장비 정보 값 대량 수집 요청 기능을 추가한 버전이다.
- SNMPv2에서는 커뮤니티 값을 암호화하여 전송하도록 변경하였다.
- 하지만 사용하기 너무복잡하다는 문제점에 도달한 후, 다시 평문으로 전달하는것으로 돌아감.
    - 이것이 SNMPv2c라고 불린다.

### SNMPv3

- SNMPv2의 특징에서 보안 기능을 추가로 강화한 버전이다.
- Username(계정) + Password(비밀번호, 커뮤니티값에 해당)을 제공해야 한다.
- 비밀번호는 인증 값과 암호 값으로 구성된다.
    - 인증 값 : 해쉬 알고리즘으로 위변조 여부를 확인함 (MD5,SHA알고리즘 사용)
    - 암호 값 : 암호화 알고리즘(AES,3-DES)를 사용하여 암호화되는 비밀번호.