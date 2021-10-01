# 파일 시스템

물리 저장장치는 논리적인 파티션으로 나눠지며 각 파티션은 고유의 파일 시스템을 생성한다.

파일 시스템은 파티션별로 생성된다.

<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/b0c56668b7fd50834cea6d700333f086a0e67e80/Linux/imgs/file%20system.png" width="700">
</p>

```
📌 <파일시스템 생성하기>

1) 물리 디스크 장착하기

2) 파티션 나누기 → fdisk

3) 파티션에 파일시스템 생성하기(포맷) → mkfs

4) 디스크 mount하기 → mount /dev/sdb1 /mnt/hdd1 (해제: umount /mnt/hdd1)
```

### 파일시스템 구성

✔️ Boot block 

- 맨 앞에 위치하며 운영체제 초기화 또는 부팅시 필요한 bootstrap 코드를 가지고 있는 블럭

✔️ Super block

- 해당 **파일 시스템을 관리**하기 위한 정보를 담고 있는 블럭

✔️ i-node list

- **파일에 대한 속성 정보를 관리**하기 위한 블럭
    
    <p>
      <img src="https://github.com/triflingness/CSnCT-Study/blob/b0c56668b7fd50834cea6d700333f086a0e67e80/Linux/imgs/i-node%20list%20property.png" width="700">
    </p>

✔️ Data blocks

- 실제 파일의 데이터가 들어있는 블럭

# 링크 파일

> link : 파일에 접근할 수 있는 또 다른 포인터를 생성하는 기능

윈도우 바로가기처럼 **원본 파일을 참조할 수 있는 파일**이 링크 파일이다.

링크파일은 `하드 링크(Hard link)`와 `심볼릭 링크(Symbolic link)`로 구분된다.

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/c96a302ac66b4bf85b2a41ba695f8b675dc86ed6/Linux/imgs/cmd_ln.png" width="700">
</p>

## 하드 링크(hard link)

원본 파일과 같은 i-node를 가지는 파일

- 동일한 파일 시스템에서만 링크가 가능하다.
- 하드 링크의 i-node는 원본의 i-node와 같아 자신의 i-node를 통해 접근한다.
- directory는 하드 링크가 불가능하다.
- 하드 링크 파일 생성시, link count가 1 증가한다.
- 원본파일 삭제 시, link count를 참고하여 참조하는 파일이 있으면 삭제되지 않는다.

## 심볼릭 링크(Symbolic link)

원본 파일에 대한 파일 경로를 파일 내용으로 가지는 파일

- 원본 파일에 대한 경로를 저장하여 다른 파일시스템의 파일 또는 디렉터리의 링크도 가능하다.
- 원본 파일이 삭제 또는 이동하면 심볼릭 링크는 링크가 끊어지게 된다.

<p align="center">
  <img src="https://github.com/triflingness/CSnCT-Study/blob/b0c56668b7fd50834cea6d700333f086a0e67e80/Linux/imgs/unix%20link.png" width="700">
</p>

----
[https://sksstar.tistory.com/10](https://sksstar.tistory.com/10)
