## Hostname and partitions

### Hostname 확인

```hostnamectl```

### Hostname 변경

```sudo hostnamectl set-hostname [hostname]```   
재부팅하면 바뀌어져 있다.

### partitions 확인

```lsblk```

>주 파티션은 최대 4개만 만들 수 있다. 이러한 한계를 벗어나기위해 확장 파티션과 논리 파티션이 만들어졌다. 주 파티션 하나를 확장 파티션으로 두면 그 파티션을 여러개의 논리 파티션으로 나눌 수 있다. 확장 파티션은 디스크 하나에 하나만 만들 수 있다. 

>리눅스는 파티션을 SCSI 디스크의 경우 최대 255개(주 파티션 3개, 논리 파티션 252개), IDE 디스크의 경우 최대 63개(주 파티션 3개, 논리 파티션 60개)까지 쓸 수 있다.

>첫번째 발견한 하드디스크의 이름은 /dev/sda이다. 두번째 발견한 하드디스크의 이름은 /dev/sdb이고, 그 이후는 마찬가지다.

>드라이브의 파티션 이름은 디스크 이름 뒤에 숫자를 붙인다. sda1와 sda2는 각각 첫번째 디스크의 첫번째와 두번째 파티션을 말한다.

>리눅스에서 주 파티션은 드라이브 이름 뒤에 숫자 1에서 4까지가 붙인다. 예를 들어 첫번째 드라이브의 첫번째 파티션은 /dev/sda1이다. 논리파티션은 5번부터 시작하므로, 이 드라이브의 첫번째 논리파티션은 /dev/sda5이다. 확장 파티션은 논리파티션이 들어있는 주 파티션으로, 직접 쓸 수 없다.

### LVM이란?

[LVM이란](https://mamu2830.blogspot.com/2019/12/lvmpv-vg-lv-pe-lvm.html)

