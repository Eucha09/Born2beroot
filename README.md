# Born2beroot

가상머신 설치 및 서버 세팅   
VM: **VirtualBox**   
OS: **Debian**

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

## sudo적용

## UFW / 설정하기

## SSH / SSH서버 설정하기

## 비밀번호 정책 설정

## 호스트네임과 파티셔닝

## cron, monitoring.sh