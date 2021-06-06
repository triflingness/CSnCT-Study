# TCL

> Transaction Control Language는 트랜잭션을 제어하는 명령어

## COMMIT

- INSERT, UPDATE, DELETE 문으로 **변경한 데이터를 데이터베이스에 반영**
- 변경 전 이전 데이터는 잃어버림
- 다른 모든 데이터베이스 사용자는 변경된 데이터를 볼 수 있음
- COMMIT이 완료되면 데이터베이스 변경으로 인한 LOCK이 해제(UNLOCK)
- COMMIT이 완료되면 다른 모든 데이터베이스 사용자는 변경된 데이터 조작 가능
- COMMIT을 실행하면 하나의 트랜잭션 과정 종료

## ROLLBACK

- ROLLBACK을 실행하면 데이터에 대한 변경 사항을 모두 취소하고 트랜잭션을 종료
- INSERT, UPDATE, DELETE 문의 작업을 **모두 취소함**
- 단, **이전에 COMMIT한 곳까지만 복구**
- ROLLBACK을 실행하면 **LOCK이 해제**되고 다른 사용자도 데이터베이스 행을 조작할 수 있음

## SAVEPOINT

- 트랜잭션을 작게 분할하여 관리하는 것
- 지정된 위치 이후의 트랜잭션만 ROLLBACK 가능
- SAVEPOINT 지정은 `SAVEPOINT <SAVEPOINT명>`을 실행
- 지정된 SAVEPOINT까지만 데이터 변경을 취소하고 싶은 경우는 `ROLLBACK TO <SAVEPOINT명>`을 실행
- `ROLLBACK`을 실행하면 **SAVEPOINT와 관계없이** 데이터의 모든 변경사항을 저장하지 않음
