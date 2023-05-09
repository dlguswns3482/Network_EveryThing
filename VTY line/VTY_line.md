# VTY line

# VTY line이 무엇인가요❓

- VTY Line은 원격으로 접속하는 가상 터미널 라인을 의미한다.

### VTY line이 하는일이 무엇인가요❓

- VTY Line은 네트워크 장비(라우터,스위치)에 대한 원격 접속을 가능하게 한다.
- VTY Line은 일반적으로 Telnet, SSH 등의 프로토콜을 사용하여 원격으로 접속한다.
- VTY Line을 통해 관리자는 네트워크 장비에 대한 설정, 모니터링 등을 원격으로 수행한다.

### VTY line 설정 방법

```markdown
Router# conf t

Router(config)# line vty 0 4

Router(config-line)# password [ password ]

Router(config-line)# login 

Router(config-line)# exit
```

- 이 설정을 하게 되면 vty line으로 원격접속을 할 때 Password설정이 가능하다.