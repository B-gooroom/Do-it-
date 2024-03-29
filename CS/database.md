### Database
---
- 관계형 데이터 = 엑셀과 같이 표의 형태로 데이터를 관리함 (차이점이라면 ui 버튼을 활용 or `DB의 언어로 실행`)
  - 필터기능 > 보고 싶은 값만 걸러서 볼 수 있음
  - 소트기능 > 보고 싶은 순서로 소팅해서 볼 수 있음
- 데이터를 여러가지 경로로 활용이 가능
- 표(table) 그룹핑해서 관리
- Database > database schema > table > column
---
#### Database CRUD
- Database 조회 (schema)
  ```shell
  show database;
  ```
  - 현재 내 local에 가지고 있는 database schema 확인 </br>
&nbsp;<img width="220" alt="스크린샷 2023-02-20 오전 10 29 48" src="https://user-images.githubusercontent.com/79742210/219989423-8cb38e38-14f4-4b4b-af5a-94391291b9af.png">
- Database 생성 (schema)
  ```shell
  create database 이름(ex.bases);
  ```
  - 새로운 database 생성 </br>
&nbsp;<img width="220" alt="스크린샷 2023-02-20 오전 11 01 37" src="https://user-images.githubusercontent.com/79742210/219992154-4996b70c-5ea3-4da0-a686-34f24b0c31a1.png"> </br>
↓ </br>
&nbsp;<img width="220" alt="스크린샷 2023-02-20 오전 11 04 00" src="https://user-images.githubusercontent.com/79742210/219992366-7fa6f244-d4e7-4a08-ab0f-5945f85911b0.png">
- Database 삭제 (schema)
  ```shell
  drop database 이름(ex.bases);
  ```
  - database 삭제 </br>
&nbsp;<img width="220" alt="스크린샷 2023-02-20 오전 11 09 06" src="https://user-images.githubusercontent.com/79742210/219993040-a7ae8912-777c-4a0e-b4ec-dbc4db5d33db.png"> </br>
↓ </br>
&nbsp;<img width="220" alt="스크린샷 2023-02-20 오전 11 10 06" src="https://user-images.githubusercontent.com/79742210/219993164-8bae7d87-b83c-4fd1-8dea-1a949aa42981.png">

- 생성한 database로 접근하기(이동)

  ```shell
  use 이름(ex.bases);
  ```
  - <img width="220" alt="스크린샷 2023-02-20 오전 11 20 26" src="https://user-images.githubusercontent.com/79742210/219994881-48b6af78-2395-4b63-945d-17a07706b83b.png">
---
#### Table
- Table의 구조
  - 행 (row - 1, 2, 3 행) >> data 단에서 1개의 data를 의미
  - 열 (column - a, b, c 열) >> data의 type을 의미
- Table 생성
  - column의 type을 지정해야 함 >> int(), varchar() 등
  - column 중에 필수값을 지정할 수 있음 >> not null(필수) & null(선택)
  - primary key 설정
  - row 추가될 때마다 일정하게 증가하는 값 설정 >> auto_increment
  ```shell
  create table 이름(
    record_no int(20)[type] not null[필수] auto_increment[+1증가],
    user_id varchar(20)[type] not null[필수],
    record_time datetime not null[필수],
    contents varchar(100) null[선택],
    PRIMARY KEY(record_no)[메인 키 설정]
    );
  ```
- <img width="325" alt="스크린샷 2023-02-20 오전 11 45 29" src="https://user-images.githubusercontent.com/79742210/219997736-0c111527-ac7d-485c-a6d7-6f66b2235715.png">

