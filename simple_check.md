## 간단한 체크

### OS와 버전 확인

```head -n 2 /etc/os-release```

### AppArmor 설치되어 있는지 확인

```aa-status```

### 사용중인 포트 확인

```ss -tunlp```

### UFW 상태 확인

```ufw status```
