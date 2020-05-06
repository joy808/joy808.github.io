---
title: "Openstack Mount Volumes"
categories:
  - DevOps
tags:
  - openstack
---

* 아래는 openstack horizon에서 instance에 volume을 연결한 이후 수행하는 작업
  프로세스 입니다.

# 연결된 disk	확인
```
$ fdisk -l
```

# horizon상에서 연결된 경로로 fdisk실행
```
$ fdisk /dev/vdb
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table.
Created a new DOS disklabel with disk identifier 0xee87d061.
```

# 디스크 상태 확인
```
Command (m for help):F
Unpartitioned space /dev/vdb: 1000 GiB, 1073740775424 bytes, 2097149952 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes

Start        End    Sectors  Size
 2048 2097151999 2097149952 1000G
```

# 파티션 생성
```
Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p):
...
```

# ext4 포맷으로 포맷하기
```
$ mkfs.ext4 /dev/vdb1
```

# 마운트를 위한 UUID 정보 확인
```
$ blkid
```

# 마운트를 위한 fstab 설정
```
$ vi /etc/fstab
UUID=[UUID값] [실제 마운트될 디렉토리] [파티션 포맷] defaults 0 0

e.g. 
UUID=8cc76db2-056b-4456-b54d-5f3fe8361695 /mnt                   ext4    defaults        1 1
```

# 마운트 및 확인
```
$ mount -a
```