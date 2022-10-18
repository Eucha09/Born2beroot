## UFW

### FireWall(방화벽)

- 미리 정의된 보안 규칙에 기반, 들어오고 나가는 네트워크 트래픽을 모니터링하고 제어하는 보안 시스템

### IPTables

- 리눅스에서 많이 쓰이는 방화벽
- 설정과 관리가 너무 복잡함

### UFW

- Uncomplicated FireWall
- 데비안 계열 및 다양한 리눅스 환경에서 IPTables 방화벽 구성을 좀 더 쉽게 설정할 수 있게 해주는 프로그램
- 사용자 친화적이고 사용하기 쉬운 인터페이스를 제공

### UFW 상태 및 규칙 확인

```sudo ufw status verbose```   
- ufw 규칙들에 넘버링하여 볼 경우   
```sudo ufw status numbered```

### UFW 규칙 추가

- 포트 허용   
```sudo ufw allow 8080```   
- 포트 거부   
```sudo ufw deny 8080```

### UFW 규칙 삭제

```sudo delete <규칙번호>```

### 그 외 설정하는 법

[UFW 설정](https://webdir.tistory.com/m/206)