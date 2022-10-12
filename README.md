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
1. user ID 입력 (user 이름이 자동으로 적혀있음)
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

## sudo적용

## UFW / 설정하기

## SSH / SSH서버 설정하기

## 비밀번호 정책 설정

## 호스트네임과 파티셔닝

## cron, monitoring.sh