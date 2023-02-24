# Project
- mlops를 ML 엔지니어가 경험해보기
- [해당 내용](https://mlops-for-mle.github.io/tutorial/docs/intro)을 따라가는 프로젝트
- 2023.02.20 ~ 

# TIL
## 01. Database
- What
    - DB server 생성
    - 데이터 생성
### 진행과정
1. DB 서버 생성
-  `docker run -d --name postgres-server -p 5432:5432 -e POSTGRES_USER=minsoo -e POSTGRES_PASSWORD=1234 -e POSTGRES_DB=mydb postgres:14.0`
2. DB 서버 확인
- psql [설치](https://www.postgresql.org/download/)
- ` PGPASSWORD=1234 psql -h localhost -p 5432 -U minsoo -d mydb`
```
psql (15.2 (Ubuntu 15.2-1.pgdg20.04+1), server 14.0 (Debian 14.0-1.pgdg110+1))
Type "help" for help.

mydb=# \du
                                   List of roles
 Role name |                         Attributes                         | Member of 
-----------+------------------------------------------------------------+-----------
 minsoo    | Superuser, Create role, Create DB, Replication, Bypass RLS | {}

mydb=# 
```
3. 테이블 생성
- `pip install pandas psycopg2-binary scikit-learn`
- `psycopg2`를 이용하여 테이블을 생성해본다.
- [`.py`](./01_database/01_create_table.py)을 실행하여 테이블을 생성한다.
- ` PGPASSWORD=1234 psql -h localhost -p 5432 -U minsoo -d mydb`로 db에 접속하여 만들어졌는지 확인해본다.

4. 데이터 생성 및 테이블에 삽입
- [`.py`](./01_database/02_data_insert.py)를 실행하여 데이터를 테이블에 삽입한다. (3초간격으로 row 하나씩)

5. `docker compose`를 이용하여 container 환경에서 데이터 생성 및 db에 저장
- 데이터 저장용 DB container와 데이터 생성해서 DB에 삽입하는 container 2개가 필요하다.
- 서로 통신이 가능해야하므로 docker compose를 이용한다.
- DB container는 기존의 image를 사용하고 데이터 생성 container는 [`Dockerfile`](./01_database/Dockerfile)을 이용한다.
- [`docker-compose.yaml`](./01_database/docker-compose.yaml)을 만들고 `docker compose up -d` 명령어를 이용해서 container를 띄운다.
    - DB container가 잘 띄워진다음 데이터를 생성해서 보내기 위해 `healthcheck`기능을 이용한다.

## 02. Model Development
## 03. Model Registry
## 04. Model Deployment
## 05. FastAPI
## 06. API Serving
## 07. Kafka
## 08. Stream