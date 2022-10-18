## SSH

### SSH 상태 확인

```systemctl status ssh```

### SSH 설정 확인

```vi /etc/ssh/sshd_config```

### Client에서 SSH를 통해 Server(가상머신) 접속

```shell
ssh <계정이름>@<서버주소> -p <포트번호>
#ex) ssh eujeong@10.28.4.9 -P 4242
```