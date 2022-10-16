# Born2beroot

가상머신 설치 및 서버 세팅   
VM: **VirtualBox**   
OS: **Debian(Linux)**

## 가상머신 및 OS 설치 (VirtualBox, Debian)

1. VirtualBox 설치
1. Debian 설치   
https://www.debian.org/releases/stable/debian-installer/   
```netinst CD 이미지 - amd64 다운로드```
1. VirtualBox 실행
1. 상단 new 클릭
1. 가상머신 이름과 경로 및 타입, 버전 설정 후 Continue   
Name: ```eujeong's vm```   
Machine Folder: ```/goinfre/eujeong```   
Type: ```Linux```   
Version: ```Debian(64-bit)```
1. 가상머신에서 사용할 메모리 크기 지정 후 Continue   
```1024MB```
1. 가상 하드디스크 생성 선택 후 Create   
```Create a virtual hard disk now```
1. VDI 선택 후 Continue   
```VDI```(VirtualBox에서만 사용가능한 포맷)
1. Dynamically allocated 선택 후 Continue   
(저장공간이 동적으로 설정되어 공간효율에 좋음, 다만 성능은 떨어짐)
1. 저장공간 한계치 설정 후 Create   
```8.00GB```
1. 가상머신이 생성되었다면 가상머신 선택후 상단에 Start 클릭
1. 다운받았던 Debian 파일을 찾아서 넣은 후 Start
1. Debian 설치화면이 떴다면 install 선택   
창이 작다면 하단바에서 조절 가능
1. 언어는 ```English``` 선택   
(한국어는 글자가 깨지는 이슈가 있음)
1. 나라 선택 ```other```->```asia```->```Korea, Republic of```
1. ```United States``` 선택
1. 키보드는 ```Korean``` 선택
1. 호스트네임 설정   
```eujeong42```
1. 도메인네임은 빈칸으로 넘어감
1. root 비밀번호 입력
1. root 비밀번호 재입력
1. user 이름 입력   
```eujeong```
1. user ID 입력 (user 이름이 자동으로 적혀있음)   
```eujeong```
1. user 비밀번호 입력
1. user 비밀번호 재입력
1. 암호화된 LVM을 선택   
```Guided - use entire disk and set up encrypted LVM```
1. 다음 엔터
1. 파티션 분할 선택   
```Separate /home partition```
1. LVM 구성하시겠습니까? ```Yes```
1. LVM 비밀번호 입력
1. LVM 비밀번호 재입력
1. LVM 분할 할 볼륨 크기 입력 (기존 볼륨크기 그대로 선택함)
1. ```finish ... ``` 선택
1. 디스크 덮어쓰기 전 확인 ```Yes```
1. 더 읽을 파일 있는지 ```No```
1. update, upgrade, 프로그램 추가를 위한 네트워크 미러 사이트 설정   
```Korea, Requblic of```
1. 다음 그냥 엔터
1. 프록시 설정 (그냥 ```Continue```)
1. 통계자료 보내기 ```No```
1. 추가로 설치할 소프트웨어 선택 (그냥 ```Continue```)
1. GRUB 설치 ```Yes``` (```No``` 해도 상관없음)
1. 부트 경로 지정   
```/dev/sda (ata-...)```
1. 설치 완료. ```Continue```
1. 재부팅되었다면 LVM 비밀번호 입력
1. root로 로그인
1. ```lsblk``` 를 입력해보면 파티셔닝된 디바이스 정보 확인 가능

## sudo 설치 및 설정

1. root로 로그인
1. sudo가 설치되어 있는지 확인   
```dpkg -l sudo```
1. 설치되어 있지 않다면 sudo 설치   
```apt update```   
```apt install sudo```
1. ```visudo``` 명령어로 sudoers 파일에 접근하여 아래와 같이 설정해주기
	> sudoers파일은 일반 편집기로 접근하면 많은 제약이 있다.   
	> 직접 /etc/sudoers 파일을 편집하다가 실수가 발생하면, sudo를 사용할 수 없게 된다.   
	>visudo는 문법체크를 해준다.

	secure_path에 ```/snap/bin``` 추가
	```shell
	secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
	```
	>sudo명령 실행 시 현재 계정의 쉘이 아닌 새로운 쉘을 생성하고 그 안에서 명령을 실행하는데, 이 때 명령을 찾을 경로를 나열한 환경변수인 PATH값이 바로 secure_path
	> 
	> 트로이목마 해킹 공격에 대한 일차적인 방어 기능을 제공.(사용자의 부주의로 현재 계정의 PATH에 악의적인 경로가 포함된 경우, 이를 무시함으로써 sudo를 통한 전체 시스템에 해킹되는 경우를 방지

	그 밑에 다른 정책들 추가
	```shell
	Defaults	authfail_message="원하는 에러메세지" #권한 획득 실패 시 출력 (sudo 인증 실패 시)
	Defaults	badpass_message="원하는 에러메세지" #sudo인증에서 비밀번호 틀리면 출력
	Defaults	iolog_dir="/var/log/sudo/" #sudo log 저장 디렉토리 설정
	Defaults	log_input #sudo명령어 실행 시 입력된 명령어 log로 저장
	Defaults	log_output #sudo명령어 실행 시 출력 결과를 log로 저장
	Defaults	requiretty #sudo명령어 실행 시 tty강제
	Defaults	passwd_tries=3 #sudo실행 횟수를 지정. default가 3
	```
	이후 ```ctr + x```를 누른 후 ```y```를 누르고 엔터를 치면 저장하고 나가진다.

1. ```visudo```를 한번 더 해서 제대로 입력되었는지 확인
1. 누가 sudo명령어를 실행 시 ```/var/log/sudo/```에서 log를 확인할 수 있다.

## 그룹 설정

1. user42 그룹 추가   
```groupadd user42```
1. sudo, user42 그룹에 사용자 추가   
```usermod -aG sudo,user42 <사용자ID>```
1. user42 그룹이 기본 그룹이 되도록 한다   
```usermod -g user42 <사용자ID>```
	> ```-g``` : 사용자의 기본 그룹을 변경   
	> ```-G``` : 추가로 다른 그룹에 속하게 할 때 쓰임. G옵션만 붙힌 상태에서 그룹 설정 시, gid그룹(기본그룹)을 제외하고 명령어에 나열된 그룹만 추가가 되며 명령어에 나열되어 있지 않지만 유저가 속해있는 그룹은 전부 탈퇴된다.   
	> ```-a``` : G옵션에서만 함께 쓰일 수 있고, G옵션만 붙었을 때와 달리, 유저가 속해있지만 명령어에 나열되어있지 않는 그룹에 관하여 탈퇴처리 되지 않는다. 

## vim 설치 및 설정

1. root로 로그인
1. vim 설치   
```apt install vim```
1. ```.vimrc``` 파일을 열어 아래와 같이 설정 (간단하게 기본적인 것만 설정)   
```vi ~/.vimrc```
	```shell
	syntax on
	set number
	set mouse=a
	```

## UFW 설치 및 설정

1. root로 로그인
1. UFW 설치   
```apt install ufw```
1. UFW 상태 확인 (디폴트는 inactive)   
```ufw status verbose```
1. 부팅 시 ufw 활성화되게 설정   
```ufw enable```
1. 기본 incoming deny로 설정   
```ufw default deny```
1. ssh 연결 허용   
```ufw allow 4242```
1. ufw 상태 확인 (active로 되어 있어야함)   
```ufw status verbose```

## SSH 설치 및 설정

1. root로 로그인
1. openssh가 설치되어 있는지 확인 (보통 설치되어 있다)   
```apt search openssh-server```   
설치가 안되어 있다면 설치   
```apt install openssh-server```
1. ```/etc/ssh/sshd_config```파일을 열어 아래와 같이 설정   
```vim /etc/ssh/sshd_config```   
```#Port 22```를 ```Port 4242```로 변경 (#을 지워야 함)   
```#PermitRootLogin prohibit-password```를 ```PermitRootLogin no```로 변경   
해당 옵션은 외부에서 root로 로그인하는 것을 막는 것이다.
	> ```/etc/ssh```에는 ```ssh_config```와 ```sshd_config```가 있다. 전자는 client측일 때 설정, 후자는 server측일 때 설정이다.
1. ssh를 재시작하여 설정 적용   
```systemctl restart ssh```
1. ssh 상태 확인 (실행여부와 사용포트 확인)   
```systemctl status ssh```

### 로컬 PC(Client)에서 가상머신(Server)에 접속하는법

1. ```ifconfig``` 명령어를 통해 실제 머신의 ip주소를 확인한다.
1. ```ifconfig``` 혹은 ```hostname -I```를 통해 가상머신의 ip주소를 확인한다.
1. VirtualBox에서 가상머신을 선택 후 상단에 ```Settings```->```Network```->```Adapter1```->```Advanced```->```Port Forwarding```에 들어간다.
1. 우측에 add 버튼을 누른 후 아래와 같이 입력한다.
	| Host IP | Host Port | Guest IP | Guest Port |
	| ------- | --------- | -------- | ---------- |
	| 실제 머신의 ip주소 | 아무숫자 | 가상머신의 ip주소 | 4242 |
	
	ex)
	| Host IP | Host Port | Guest IP | Guest Port |
	| ------- | --------- | -------- | ---------- |
	| 10.28.4.9 | 4242 | 10.0.2.15 | 4242 |
	> ```10.28.4.9:4242``` 에 접속시도를 했을 때 ```10.0.2.15:4242```로 연결시켜준다는 의미
1. 가상머신을 다시 실행시킨 후 클라이언트 측에선 아래 명령어로 가상머신에 접속할 수 있다.
	```shell
	ssh <계정이름>@<서버주소> -p <포트번호>
	#ex) ssh eujeong@10.28.4.9 -P 4242
	```

## 비밀번호 정책 설정

1. root로 로그인
1. ```/etc/login.defs```파일을 열어 아래와 같이 기본 정책 설정   
```vi /etc/login.defs```   
(좀 많이 내려가야 있음)
	```shell
	PASS_MAX_DAYS 30	#패스워드 최대 사용일
	PASS_MIN_DATS 2		#패스워드 최소 사용일
	PASS_WARN_AGE 7		#패스워드 만료 경고일
	```
1. 패스워드 정책 설정을 위한 모듈 설치   
```apt install libpam-pwquality```
1. /etc/pam.d/common-password 파일을 열어 패스워드 강도 정책 설정   
```vi /etc/pam.d/common-password ```   
```pam_pwquality.so retry=3``` 뒤에 이어 아래와 같이 설정하면 된다.
	```shell
	pam_pwquality.so retry=3 minlen=10 ucredit=-1 lcredit=-1 dcredit=-1 maxrepeat=3 reject_username enforce_for_root difok=7
	```
	> ```retry=N```: 암호입력을 N회로 설정   
	> ```minlen=N```: 암호의 최소 길이는 N   
	> ```ucredit=-N```: 대문자 N개 이상   
	> ```lcredit=-N```: 소문자 N개 이상   
	> ```dcredit=-N```: 숫자 N개 이상   
	> ```maxrepeat=N```: 같은 문자가 N번 이상 연속해서 나오는지 검사   
	> ```reject_username```: 사용자의 이름이 그대로 혹은 뒤집혀 패스워드에 있는지 검사   
	> ```enforce_for_root```: root 사용자가 패스워드를 바꾸려 할 때에도 위 조건 적용   
	> ```difok=N```: 기존 패스워드와 달라야하는 문자 수 N
1. 현재 비밀번호가 조건에 않는 경우, 아래 명령어로 바꿀 수 있다.   
```passwd -e <사용자ID>```   
사용자가 다시 로그인을 해보면 비밀번호를 변경하라고 뜬다.
	> ```-e```: 강제적으로 사용자의 암호를 만료시킨다.

## 호스트네임과 파티셔닝

## cron, monitoring.sh