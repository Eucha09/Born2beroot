## 간단한 체크

### OS와 버전 확인

```head -n 2 /etc/os-release```

### AppArmor 설치되어 있는지 확인

```aa-status```

### Listening중인 포트 확인

> 클라이언트의 접속 요청을 기다리고 있는 포트

```ss -tunlp```

### UFW 상태 확인

```ufw status```
