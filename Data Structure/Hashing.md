Heshing
=======

### 해싱(Hashing)
- 해시 테이블을 이용한 탐색 방법
- 배열을 사용하여 데이터를 저장하기에 검색 속도가 빠르다
- 탐색키의 비교가 아닌 탐색키에 수식을 적용시켜서 바로 탐색 키가 저장된 위치를 얻는다.

### 해시 테이블(Hash tables / Hash map)
- (Key, Value)로 데이터를 저장하는 자료구조
- 대량의 정보를 저장하고 특정 요소를 효율적으로 검색할 수 있다.
- key 저장 시 데모리 공간을 더 사용하도록, 다양한 길이를 가진 key를 일정한 길이의 hash로 바꾸어 저장소 사용이 효율적이다.
- 각각의 키값에 해시 함수를 적용해 해시를 생성한다.
- 생성된 해시를 활용해 값을 저장하거나 검색한다.
- 배열이 저장되는 곳은 저장소(bucket, slot)이다.
- 
  - 키 Key : 다양한 길이의 고유한 값, 해시 함수의 input
  - 해시 함수 Hash Function : key를 hash로 바꿔주는 함수
  - 해시 Hash : hash function의 결과물, bucket, slot에 value와 매칭되어 저장
  - 값 Value : bucket, slot에 최종적으로 저장되는 값으로 키와 매칭되어 저장, 삭제, 검색, 접근이 가능

#### Key는 Hash Function을 통해 Hash로 변경되고, Hash는 Value와 매칭되어 저장소(Bucket, Slot)에 저장된다.



