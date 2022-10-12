# ****DBMS ~ 외래키, 정규화****

목차

DBMS
DB를 사용하는 이유
DBMS 종류
- HDBMS
- NDBMS
- RDBMS
- NoSQL
테이블 구조
키
- 슈퍼키
- 후보키
- 기본키
- 대체키
- 외래키

정규화
- 배경
- 제 1정규화
- 제 2정규화
- 제 3정규화

## ****DBMS****

- 데이터베이스 관리 시스템(DataBase Management System)
- 데이터베이스의 데이터에 접근하여 사용할 수 있도록 해주는 SW
- 정의, 조작, 제어 기능 수행
    - 정의 : DB 구조 정의(테이블, 속성)
    - 조작 : DB 연산 처리(수정, 삭제, 검색)
    - 제어 : 데이터 무결성 및 일관성 유지, 접근 권한 부여, 동시성 제어

<BR>
<BR>

## DB를 사용하는 이유

- DB 이전 ~  `파일 시스템` 사용
    - OS 종속적
    - 데이터 중복, 비일관성, 검색 등의 문제 존재
- 확장성이 좋음
- 중복 최소화, 보안성, 계속적 변화에 대한 적응
- 데이터 관리 기능을 통해 데이터를 편하게 관리 할 수 있음

<BR>
<BR>

## DBMS 종류

### 계층형 DBMS(HDBMS, Hierarchical DBMS)

- 처음 등장한 DBMS 개념으로 1960년대 시작됨.
- 트리 형태를 갖음.
- 처음 구성 완료 후 이를 변경하기 까다로움. → 현재는 사용하지 않음.

![계층형 DBMS](https://hongong.hanbit.co.kr/wp-content/uploads/2021/11/계층형DBMS.png)

<BR>

### 망형 DBMS (NDBMS, Network DBMS)

- 계층형 DBMS의 문제점 개선을 위해 1970년대 등장
- 하위 구성원들끼리도 관계를 갖는 유연한 구조로, 네트워크상의 노드로 데이터 구조를 표현하여 각각 노드가 서로 대등한 관계로 구성됨.

> **👆 여기서 잠깐**
여기서 노드란 시스템이 아니라 자료를 의미.
> 
- 구성과 설계가 복잡하고 궁극적으로 데이터 종속성의 문제를 해결하지 못했다.

> **👆 데이터 종속성 문제란? (Data Dependency)**
프로그램의 구조가 데이터 구조에 영향을 받는 것을 의미.
> 

![망형DBMS](https://hongong.hanbit.co.kr/wp-content/uploads/2021/11/망형DBMS.png)

<BR>

### 관계형 DBMS (RDBMS, Relational DBMS)

- `테이블` 이라는 최소단위로 구성되며, `열`과 `행`으로 이루어져 있다.
- SQL을 이용해 `속성(열)에 맞는 자료형`으로 데이터 삽입

> **👆 SQL(Structured Query Language)**
RDBMS에서 사용되는 언어로 특정 회사에서 만드는게 아니라 `국제표준화기구`에서 SQL에 대한 표준을 정해서 발표하고 있음. 이를 `표준SQL` 이라고 함.
> 
- ACID

> 👆 **ACID?
데이터베이스의 트랜잭션이 안전한 수행을보장하기 위해 가지는 4가지 특성을 말함.
- 트랜잭션(Transaction) :** 다수 사용자가 데이터베이스를 동시에 접근하도록 허용하면서 데이터 베이스가 일관성을 유지하게 하는 기술
- **Atomicity(원자성)** : 트랜잭션의 처리가 완전히 끝나지 않았을 경우에는 전혀 이루어지지 않은 것과 같아야 한다(all or nothing).
- **Consistency(일관성)** : 트랜잭션의 실행이 성공적으로 완료되면 데이터베이스는 모순 없이 일관성이 보존된 상태여야 한다.
- **Isolation(격리성)** : 현재 수행중인 트랜잭션이 완료될 때 까지 트랜잭션이 생성한 중간 연산 결과에 다른 트랜잭션들이 접근할 수 없다.
- **Durability(지속성)** : 트랜잭션이 성공적으로 완료된 후 데이터베이스에 반영한 수행 결과는 어떠한 경우에도 손실되지 않고 영구적이어야 한다.
> 
- 데이터 무결성 보장, 데이터를 중복 없이 저장
- 기존의 스키마 수정이 어려움, 데이터가 자주 변경되거나 명확한 스키마가 있는 경우 사용

![RDBMS](https://hongong.hanbit.co.kr/wp-content/uploads/2021/11/sql_table.png)

<BR>

### 비관계형 DBMS (NoSQL)

- 스키마가 없거나 느슨한 스키로 데이터 저장
- 데이터 질의 API 다양함
- 유연하고 확장성이 좋음
- 데이터를 자주 변경하지 않고 정확한 데이터 구조를 알 수 없는 경우 사용함
- 키-값 : `Redis` , 문서형(JSON, XML) : `MongoDB`

<BR>
<BR>

## 테이블 구조

![테이블구조](https://github.com/workhardslave/cs-study/raw/main/Database/img/dbms1.png)

- 테이블
    - 행과 열로 이루어진 데이터 집합
    - 릴레이션 스키마와 인스턴스로 구성
- 스키마
    - 테이블의 이름과 속성들의 나열, 테이블의 첫 행 헤더
    - 데이터 구조와 구성을 설명
- 행
    - 테이블을 구성하는 데이터 셋. `튜플` 이나 `레코드`라고 불림
    - 한 객체에 대한 정보를 가짐
- 열
    - 테이블을 구성하는 데이터 셋으로 `속성`이라고 불림.
    - 개체의 특성
- 도메인
    - 속상 하나가 취할 수 있는 같은 타입의 원자값들의 집합

<BR>
<BR>

## 키(Key)

![키](https://user-images.githubusercontent.com/38900338/139516864-ce72fa77-10dc-465c-9e6d-959db391f61d.png)

검색, 정렬 시 튜블을 **구별하는 기준이 되는 속성**

> **👆 여기서 용어정리**
**유일성** : 키로 튜플을 유일하게 식별할 수 있음
**최소성** : 튜블을 구분하는데 꼭 필요한 속성들로만 구성
> 

![테이블예시](https://github.com/workhardslave/cs-study/raw/main/Database/img/dbms3.png)

<BR>

### 슈퍼키

- `유일성`을 만족, 최소성은 만족하지 않는 속성의 집합
- (위의 테이블 참조)학번, 주민번호, 이름+나이

<BR>

### 후보키

- `유일성`과 `최소성`을 만족하는 속성의 집합
- 기본키로 사용할 수 있는 속성들
- 모든 테이블은 하나 이상의 후보키를 가짐
- (위의 테이블 참조) 학번, 주민번호

<BR>

### 기본키

- 후보키 중에서 선택한 주 키(Main Key)
- `유일성`과 `최소성` 만족
- 중복 값과 NULL값 불가(`개체 무결성`)
- (위의 테이블 참조) 학번

<BR>

### 대체키(보조키)

- 후보 키가 두 개 이상일 때 기본 키를 제외한 나머지 후보키
- (위의 테이블 참조) 주민번호

<BR>

### 외래키

- 한 테이블의 키 중에서 다른 테이블의 튜플을 식별할 수 있는 키
- 참조되는 릴레이션의 `기본키`와 대응되어 릴레이션 간에 `참조 관계`를 표현 하는 키
- 사용하는 이유 : 테이블 연결, 중복 방지, 무결성 유지

<BR>
<BR>

## 정규화

### 배경

- 데이터의 중복 발생과 무결성 저하.
- 이상현상(Anomaly) 발생
    - 삽입 이상 : 튜플 삽입 시 특정 속성에 해당하는 값이 없어 null을 입력해야 하는 현상
    - 수정 이상 : 튜플 수정 시 중복된 데이터의 일부만 수정되어 일어나는 데이터 불일치
    - 삭제 이상 : 튜플 삭제 시 같이 저장된 다른 정보까지 연쇄적으로 삭제되는 현상
- 이러한 문제 해결을 위해 정규화 과정 진행

<BR>

### 특징

- 이상현상이 있는 릴레이션을 분해하여 이상현상을 없애는 과정
- 여러 개의 릴레이션을 생서하게 됨
- 단계별로 구분되며 정규형이 높아질수록 이상현상은 줄어듬.
- 장점
    - 이상 현상 제거
- 단점
    - JOIN 연산 증가. 릴레이션의 분해로 릴레이션 간의 JOIN 연산이 많아짐
    - 질의에 대한 응답시간이 늘여질**수도** 있음.
    - 조인이 많아 성능 저하가 나타나면 반정규화를 적용할 수도 있음.

<BR>

### 제 1정규형(1NF)

- 규칙
    - 테이블 칼럼이 분해되지 않는 `원자값`을 가져야함.
    
    ![1NF](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcWnN4H%2FbtrkvINLOvN%2FWCeNK8l2Kdixwf9SKa5o80%2Fimg.png)
    
<BR>

### 제 2정규형(2NF)

- 규칙
    - 제 1정규형 만족
    - 모든 칼럼이 부분적 종속이 없어져야 함. = 모든 칼럼이 완전 함수 종족을 만족해야 함.
    
    > 👆**완전 함수 종속?** 
    어떤 속성이 기본키에 대해 완전히 종속일 때
    👆**부분 함수 종속?**
    어떤 속성이 기본키가 아닌 다른 속성에 종속되거나, 기본키가 여러 속성으로 구성되어 있을 때 기본키를 구성하는 속성 중 일부만 종속될 때.
    > 

![2NF](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkAt80%2FbtrkuJl1lkz%2FbF2qmwfoOsXMFYFpt9i0H0%2Fimg.png)

<BR>

### 제 3정규형(3NF)

- 규칙
    - 제 2정규형 만족
    - 기본키를 제외한 속성들 간에 이행 종속성이 없어야 함.
    
    > 👆**이행 종속성?**
    > 
    > 
    > A → B , B → C 인 경우 A → C 가 성립될 때.
    > 
    > 즉, A를 알면 B를 알고 그를 통해 C를 알 수 있는 경우를 의미
    > 

![3NF](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbHpEsK%2Fbtrkz43gDik%2FWwjuPIBtTdnsAsNLfeG86K%2Fimg.png)

참고자료

- [https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=utis&logNo=220472055509](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=utis&logNo=220472055509)
- [https://victorydntmd.tistory.com/129](https://victorydntmd.tistory.com/129)
- [https://hongong.hanbit.co.kr/데이터베이스-이해하기-databasedb-dbms-sql의-개념/](https://hongong.hanbit.co.kr/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-databasedb-dbms-sql%EC%9D%98-%EA%B0%9C%EB%85%90/)
- [https://code-lab1.tistory.com/48](https://code-lab1.tistory.com/48)
- [https://newehblog.tistory.com/38](https://newehblog.tistory.com/38)
- [https://developer-talk.tistory.com/256](https://developer-talk.tistory.com/256)
