# 데이터베이스 시스템

## 개요

1. **데이터베이스**: 조직체의 응용 시스템들이 공유해서 사용하는 운영 데이터들이 구조적으로 통합된 모임
    - 모든 데이터가 중복을 최소화하면서 통합됨
    - 데이터에 관한 설명(스키마 또는 메타데이터)까지 포함
    - 프로그램과 데이터 간의 독립성 제공
    - 시스템 카탈로그(또는 데이터 사전)와 저장된 데이터베이스로 구분

    > 시스템 카탈로그는 저장된 데이터베이스의 스키마 정보를 유지하며 스키마 정보가 바뀌면 시스템 카탈로그에 반영됨

2. **데이터베이스 관리 시스템(DBMS; Database Management System)**: 데이터베이스를 정의하고 질의어를 지원하고 리포트를 생성하는 등의 작업을 수행하는 소프트웨어

    데이터베이스 언어라고 부르는 특별한 프로그래밍 언어를 한 개 이상 제공

    > SQL은 여러 DBMS에서 제송되는 사실상의 표준 데이터베이스 언어

    ![시스템 카탈로그와 저장된 데이터베이스](./images/시스템%20카탈로그와%20저장된%20데이터베이스.png)

3. **스키마**: 전체적인 데이터베이스 구조를 뜻하며 자주 변경되지는 않음 = **내포**(intension)
4. **상태**: 특점 시점의 데이터베이스의 내용을 의미하며, 시간에 따라 계속 바뀜 = **외연**(extension)

    ![데이터베이스 스키마와 데이터베이스 상태](./images/데이터베이스%20스키마와%20상태.png)

## 데이터 모델

### 구성

1. **구조**: 정적 성질, 객체 타입과 이들간의 관계를 명세함
2. **연산**: 구조 위에서 동작하는 연산자들로 객체 인스턴스를 처리하는 작업에 대한 명세(데이터 조작 기법)
3. **제약조건**: 데이터의 논리적인 제약으로 데이터 조작의 한계를 표현하는 규정

### 종류

![DBMS의 발전과정](./images/DBMS의%20발전과정.png)

1. **계층 데이터 모델**
    - 트리 구조를 기반으로 하는 계층 데이터 모델
    - 네트워크 데이터 모델의 특별한 사례
    - 장점: 어떤 유형의 응용에 대해서는 빠른 속도와 높은 효율성 제공
    - 단점
        - 어떻게 데이터를 접근하는가를 미리 응용 프로그램에 정의해야 함
        - 데이터베이스가 생성될 때 각각의 관계를 명시적으로 정의해야 함
        - 레코드들이 링크로 연결되어 있으므로 레코드 구조를 변경하기 어려움

    ![계층 데이터베이스의 예](./images/계층%20데이터베이스의%20예.png)

2. **네트워크 데이터 모델**
    - 레코드들이 노드로, 레코드들 사이의 관계가 간선으로 표현되는 그래프를 기반으로 하는 데이터 모델
    - 레코드들이 링크로 연결되어 레코드 구조를 변경하기 어려움

    ![네트워크 데이터베이스의 예](./images/네트워크%20데이터베이스의%20예.png)

3. **관계 데이터 모델**
    - **구조**: 릴레이션(또는 테이블)
    - **연산**: 관계대수
    - **제약조건**: 무결성 제약조건
    - 간단하여 이해하기 쉬움
    - 사용자는 자신이 원하는것만 명시하고 데이터가 어디에 있는지 어떻게 접근해야 하는지는 DBMS가 결정
4. **객체지향 데이터 모델**
    - 객체 지향 프로그래밍 패러다임을 기반으로 하는 데이터 모델
    - 데이터와 프로그램을 그룹화하고 복잡한 객체들을 이해하기 쉬우며, 유지와 변경이 용이함
5. **객체 관계 데이터 모델**
    - 관계 데이터 모델에 객체지향 개념을 통합한 데이터 모델