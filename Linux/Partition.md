# 파티션(Partition)

하나의 물리적 디스크를 여러 개의 논리적인 디스크로 분할하는 것

### 다중 파티션의 장점

- 파티션마다 독립적인 파일 시스템이 운영되기 때문에 파일점검 시간이 줄어들어 **부팅 시간을 단축**시킬 수 있다.
- 특정 파티션의 파일 시스템이 손상되더라도 다른 파티션에 영향을 주지 않기 때문에 **높은 안정성을 보장**한다.
- 필요한 파티션만 포맷할 수 있기 때문에 **백업과 업그레이드가 편리**하다.
- 파티션 상태 정보를 확인할 수 있는 파일은 **/proc/partitions**이다.

### 파티션의 구분

- 주 파티션(Primary Partition)
    - 부팅이 가능한 기본 파티션
    - 하나의 하드디스크에 최대 4개의 주 파티션 분할 가능
    - 하드디스크를 4개 이상의 파티션으로 사용해야 할 때 하나의 확장 파티션을 설정하여 확장 파티션 안에 여러 개의 논리 파티션을 분할하여 데이터 저장
- 확장 파티션(Extended Partition)
    - 주 파티션 내에 생성, 하나의 물리적 디스트에 1개만 생성
    - 파티션 번호는 1~4번이 할당
    - 데이터 저장 영영을 위한 것이 아니라 논리 파티션을 생성
- 논리 파티션(Logical Partition)
    - 확장 파티션 안에 생성되는 파티션
    - 논리 파티션은 12개 이상 생성하지 않는 것을 권고하며 5번 이후의 번호가 붙여짐
- 스왑 파티션(Swap Partition)
    - 하드디스크의 일부를 메모리처럼 사용하는 영역
    - 주 파티션 또는 논리 파티션에 생성
    - 프로그램 실행 시 부족한 메모리 용량을 하드디스크로 대신함
    - 리죽스 설치 시에 반드시 설치되어야 하는 영역
    - 스왑(Swap) 영역의 크기는 메모리의 2배를 설정하도록 권고

### 디스크와 장치명

- 분할된 파티션은 디스크의 장치 파일명 뒤에 숫자를 붙인다.
- 하드디스크 유형 지정
- 파티션 번호
    - 1~4번:  primary 또는 extended 파티션
    - 5번: logical 파티션
    

### 파일 시스템

- 파일 시스템은 운영체제가 파일을 시스템의 디스크 파티션상에 구성하는 방식이다.
- 일정한 규칙을 가지고 파일을 저장하도록 규칙 방식을 제시한다.
- 파티션에 파일 시스템이 없으면, 파일 시스템 생성을 거쳐야 사용이 가능하다.
- 리눅스는 고유의 파일 시스템 뿐만 아니라 다양한 파일 시스템을 지원하고 있다.
    - 리눅스 전용 파일 시스템 : ext, ext2, ext3, ext4
    - 저널링 파일 시스템: JFS, XFS, ReiserFS
    - 네트워크 파일 시스템: SMB, CIFS, NFS
    - 클러스터링 파일 시스템: 레드햇 GFS, SGI cXFS, IBM GPFS, IBM SanFS, EMS highroad, Compaq CFS, Veritas CFS, 오라클 OCFS2
    - 시스템 파일 시스템: ISO9660, UDF
    - 타 운영체제 지원 파일 시스템: FAT, VFAT, FAT32, NTFS, HPFS, SysV

### LVM (Logical Volume Manager)

- 여러 개의 하드디스크를 합쳐서 사용하는 기술로 한 개의 파일 시스템을 사용한다.
- 작은 용량의 하드디스크 여러 개를 큰 용량의 하드디스크 한 개처럼 사용한다.
- 서버를 운영하면서 대용량의 별도 저장 공간이 필요할 때 활용한다.
- 다수의 디스크를 묶어서 사용함으로써 파티션의 크기를 줄이거나 늘릴 수 있다.
    - 물리 볼륨(Physical Volume): 여러 개의 물리적 하드디스크
    - 볼륨 그룹(Volume Group): 물리 볼륨을 합쳐서 하나의 물리적 그룹으로 만드는 것
    - 논리 볼륨(Logical Volume): 볼륨 그룹을 다시 나눠서 다수의 논리 그룹으로 나눔

### RAID

- 복수 배열 독립 디스크(Redundant Array of Independent Disks)의 약자
- 여러 개의 물리적 디스크를 하나의 논리적 디스크로 인식하여 작동하게 하는 기술
- 여러 개의 하드디스크에 일부 중복된 데이터를 나눠서 저장하는 기술
    - 하드웨어 RAID: 하드웨어 제조업체에서 여러 개의 하드디스크를 장비로 만들어 그 자체를 공급, 안정된 시스템일수록 고가
    - 소프트웨어 RAID: 고가의 하드웨어 RAIK의 대안, 운영체제에서 지원하는 방식, 저렴한 비용으로 안전한 데이터 저장이 가능
- 레벨 : 데이터를 저장하는 방법
    - 레벨에 따라 저장 장치의 신뢰성을 높이거나 전체적인 성능을 향상시키는 등 다양한 목적을 만족시킨다.
    - RAID 0
        - **스트라이핑 저장 방식**: 연속된 데이터를 여러 디스크에 나눠 저장
        - 최소 2개의 하드디스크가 필요
        - 입출력 작업이 모든 디스크에 동시에 진행: 저장과 읽기 속도가 가장 빠르지만 하나의 디스크라도 고장나면 전체 시스템 사용 불가
        - 고장 대비 능력이 없으므로 주요 데이터 저장은 부적합
    - RAID 1
        - **미러링 저장 방식**: 하나의 디스크에 데이터를 저장하면 다른 디스크에 동일한 내용이 백업되어 저장
        - 데이터 저장 시 두 배의 용량이 필요
        - 결함 허용을 제공하지만 공간 효율성은 떨어짐
        - 주요한 데이터를 저장하기에 적절함
    - RAID 2
        - 스트라이핑 저장 방식
        - 기록용 디스크와 데이터 복구용 디스크를 별도로 제공: 오류 제어 기능이 없는 디스크를 위해 해밍 코드 사용
        - 디스크의 사용 효율성이 낮음
        - 모든 SCSI 디스크에 ECC(에러 검출 기능)를 탑재하고 있기 때문에 실제 사용되지 않음
    - RAID 3
        - 스트라이핑 저장 방식
        - 오류 검출을 위해 패리티 방식을 이용
        - 패리티 정보를 저장하기 위해 전용 디스크를 사용하기 때문에 최소 3개 이상의 하드디스크가 필요
        - 데이터 복구는 패리티 저장 디스크에 기록된 정보의 XOR를 계산하여 수행
        - 대형 레코드가 사용되는 단일 사용자 시스템에 적합
    - RAID 4
        - RAID 3과 유사한 방식 : 2개 이상의 데이터 디스크와 전용 패리티 디스크 사용
        - RAID 3은 Byte 단위로 데이터를 저장하는 반면 RAID 4는 Block(섹터) 단위로 저장
    - RAID 5
        - 스트라이핑 저장 방식
        - 디스크마다 패리티 정보를 갖고 있어 패리티 디스크의 병목 현상을 줄이는 것이 가능해 실무에서 많이 사용
        - 디스크 섹터 단위로 저장
        - 쓰기 작업이 많지 않은 다중 사용자 시스템에 적합
    - RAID 6
        - 기본적으로 RAID 5를 확장한 것
        - 제 2partiy를 두는  dual parity를 사용함으로써 더 나은 무정지성을 갖게 함
        - 최소 4개의 드라이브가 필요
    - RAID 0+1
        - RAID 0(스트라이핑 방식)과 RAID 1(미러링)을 조합
        - 디스크 2개씩 RAID 0으로 구성 후 RAID 0으로 구성된 하드디스크들을 RAID 1로 구성
        - 미러링 전 스트라이핑을 진행
        - 속도는 빠르나 데이터 복구 시간이 오래 걸림
    - RAID 1+0
        - RAID 0+1의 반대 구성
        - 디스크 2개씩 RAID 1로 구성 후 RAID 1로 구성된 하드디스크들을 RAID 0으로 구성
        - 미러링 후 스트라이핑을 진행하여 손실된 데이터만 빠른 복원이 가능하므로 RAID 0+1보다 운영 상 유리

### 파티션 분할

🔸 fdisk 

- 파티션 테이블을 관리하는 명령어
- 리눅스의 디스크 파티션을 생성, 수정, 삭제할 수 있던 일종의 유틸리티
