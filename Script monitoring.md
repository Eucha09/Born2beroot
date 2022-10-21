## Script monitoring

일정한 시간마다 모든 터미널에 아래 정보를 표시하는 스크립트를 작성

### 운영체제 및 커널 버전의 아키텍처 출력

```sh
printf "#Architecture: "
uname -a
```

```uname``` : 시스템 및 커널 정보 출력
- ```-a``` : 시스템의 전체 정보 출력

참고 : [uname 명령어에 대한 설명](https://udpark.tistory.com/99)

### 물리적 프로세서의 수 출력

```sh
printf "#CPU physical: "
nproc --all
```

```nproc``` : 사용할 수 있는 프로세서 수
- ```--all``` : 전체 프로세서 수

참고 : [Linux nproc 명령 자습서](https://ciksiti.com/ko/chapters/1418-linux-nproc-command-tutorial--linux-hint)

### 가상 프로세서 개수 출력

```sh
printf "#vCPU :"
cat /proc/cpuinfo | grep "processor" | wc -l
```

```cat /proc/cpuinfo``` : cpu 정보가 담겨있다.
- ```| grep "processor" | wc -l``` : cpu(vCPU) 수 확인

참고 : [How to Display the Number of Processors (vCPU) on Linux VPS](https://webhostinggeeks.com/howto/how-to-display-the-number-of-processors-vcpu-on-linux-vps/)

### 서버에서 현재 사용 가능한 RAM용량 및 사용률(백분율) 출력

```sh
printf "#Memory Usage: "
free -m | grep "Mem" | awk '{printf "%d/%dMB (%.2f%%)", $3, $2, $3 / $2 * 100}'
printf "\n"
```

```free``` : 메모리 정보 출력
- ```-m``` : 메가바이트 단위로 출력

참고 : [리눅스 free 명령어로 메모리 상태 확인하기](https://www.whatap.io/ko/blog/37/)   
[리눅스 awk 명령어 사용법](https://recipes4dev.tistory.com/171)


### 서버에서 사용 가능한 현재 디스크공간 및 사용률(백분율) 출력

```sh
printf "#Disk Usage: "
df -P | grep -v ^Filesystem | awk '{sum += $3} {sum2 += $2} END {printf "%d/%dGB (%d%%)", sum/1024, sum2/1024/1024, sum/sum2*100 }'
printf  "\n"
```

```df``` : 파일 시스템의 공간에 대한 정보를 출력
- ```-P``` : 파일 시스템에 대한 정보를 POSIX와 호환되는 형식으로 표시합니다.
	>df 명령어를 그대로 쓸 경우 파일시스템 이름이 길 경우 다음 줄로 넘겨서 출력하기 때문에 -P 옵션을 준다

```grep -v ^Filesystem``` : Filesystem으로 시작하는 줄을 제외하고 출력

참고 : [리눅스 전체 디스크 사용량 확인](https://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_%EC%A0%84%EC%B2%B4_%EB%94%94%EC%8A%A4%ED%81%AC_%EC%82%AC%EC%9A%A9%EB%9F%89_%ED%99%95%EC%9D%B8)

### 프로세서(CPU)의 현재 사용률(백분율) 출력

```sh
printf "#CPU load: "
top -b -n 1 | grep -Po '[0-9.]+ id' | awk '{print 100 - $1}'
```

```top``` : 유닉스계열 시스템에서 프로세스 목록을 CPU 사용률이 높은 것부터 보여주는 소프트웨어. 3초 간격으로 업데이트를 하여 출력해준다.
- ```-b``` : 배치모드로 정보를 출력   
	> 실시간 모드에서는 한 페이지만 보여줄 수 있지만, 배치 모드에서는 모든 프로세스를 다 표시할 수 있다.
- ```-n num``` : 지정한 num 만큼 업데이트 정보를 출력

```grep``` : 특정 문자열을 찾는 명령어
- ```-P``` : PATTERN을 Perl 정규 표현식(Perl RegEx)으로 해석
- ```-o``` : 매치되는 문자열만 표시

참고 : [TOP 명령어](https://yjshin.tistory.com/entry/Linux-%EB%A6%AC%EB%88%85%EC%8A%A4-CPU-%EC%82%AC%EC%9A%A9%EB%A5%A0-%ED%99%95%EC%9D%B8%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95-TOP-%EB%AA%85%EB%A0%B9%EC%96%B4)   
[리눅스 grep 명령어 사용법](https://recipes4dev.tistory.com/157)   
[Perl](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=new27kr&logNo=221002842931)

### 마지막으로 부팅한 날짜 및 시간 출력

```sh
printf "#Last boot: "
who -b | sed 's/system boot//g' | sed 's/^ *//g'
```

```who``` : 호스트에 로그인한 사용자의 정보 출력
- ```-b``` : 마지막 시스템 부팅 시간 출력

```sed 's/system boot//g'``` : "systemp boot" 부분 삭제   
```sed 's/^ *//g'``` : 앞 공백 삭제

참고 : [[리눅스 명령어] who](https://shaeod.tistory.com/623)   

### LVM의 사용 여부 출력

```sh
printf "#LVM use: "
if [ "$(cat /etc/fstab | grep '/dev/mapper/' | wc -l)" -gt 0 ];
 then
  echo 'yes'
 else
  echo 'no'
fi
```

```cat /etc/fstab``` : 파일 시스템 정보가 담겨 있다.
- ```/dev/mapper/```이 있으면 LVM을 사용하고 있다는 의미이다.

참고 : [How do I check whether I am using LVM?](https://askubuntu.com/questions/202613/how-do-i-check-whether-i-am-using-lvm)

### 활성화된 연결 수 출력

```sh
connections=$(ss -t | grep -i ESTAB | wc -l)
printf "#Connexions TCP: $connections ESTABLISHED\n"
```

```ss``` : 시스템 소켓 상태를 출력
- ```-t``` : TCP 소켓만 출력
- ```ESTAB```의 의미 : Established, 서버와 클라이언트 간에 세션 연결이 성립되어 통신이 이루어지고 있는 상태

### 서버를 사용하는 사용자 수 출력

```sh
printf "#User log: "
who | wc -l
```

```who``` : 호스트에 로그인한 사용자의 정보 출력


### 서버의 IPv4 주소와 해당 MAC 주소 출력

```sh
ip=$(hostname -I)
mac=$(ip addr | grep "ether " |  sed "s/.*ether //g" | sed "s/ brd.*//g")

printf "#Network: IP $ip ($mac)\n"
```

```ether``` 뒤에 오는게 MAC 주소

### sudo 프로그램으로 실행된 명령 수 출력

```sh
printf "#Sudo: "
sudo grep "sudo: " /var/log/auth.log | grep "COMMAND=" | wc -l | tr -d '\n'
```

```/var/log/auth.log``` : 사용자 로그인이나 사용된 인증방법같은 시스템 인증 정보가 기록되어 있다.

### cron

- 특정 시간에 프로그램을 실행시키기 위해 사용
- 윈도우에서는 스케줄러와 비슷
- crontab에 설정해놓으면 cron이 실행시켜준다.
- 멈추기   
```/etc/init.d/cron stop```
- 시작   
```/etc/init.d/cron start```
- reboot시 cron자동실행 중단   
```sudo systemctl disable cron```
- reboot시 cron자동실행   
```sudo systemctl enable cron```
- 30초마다 실행   
```sudo crontab -e```   
```* * * * * sleep 30; /home/yurlee/monitoring.sh;```

참고 : [리눅스 크론탭 시간 설정](https://danmilife.tistory.com/4)