# Backend
📌실습 링크
[![Naver Blog Badge](https://img.shields.io/badge/Naver%20Blog-03C75A?style=flat&logo=Naver&logoColor=white)](https://blog.naver.com/genie290/223342482060)
[![Naver Blog Badge](https://img.shields.io/badge/Naver%20Blog-03C75A?style=flat&logo=Naver&logoColor=white)](https://blog.naver.com/genie290/223492077252)
---
## 1. JDK Version
- jDK 11 이상

### Modify with your MySQL info 
`path` : src/main/resources/config/application.properties
```
spring.datasource.url=jdbc:mysql://YOUR_MYSQL_URL/employee?serverTimezone=UTC&useSSL=false&allowPublicKeyRetrieval=true
spring.datasource.username=
spring.datasource.password=
spring.jpa.hibernate.ddl-auto=update
```

### docker mysql insatll
```
docker pull mysql:8.0.22 --platform linux/amd64
docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=12345 --name mysql-db mysql:8.0.22

docker exec -it mysql-db bash

## (optional) 
# apt-get update 
# apt-get install -y vim
# vi /etc/mysql/my.cnf
```
## 2. MySQL DB
- Create DB Name : employee
- (생성할 필요 없음) Create Table : employee
- (생성할 필요 없음) Columns : id, email_address, first_name, last_name

```
create database employee;
show databases;
GRANT ALL PRIVILEGES ON employee.* TO root@localhost;
flush privileges;
```

### maven build
```
mvn clean
mvn package
```

### java 
```
java -jar employee-management-backend-0.0.1-SNAPSHOT.jar
```

### docker build and running

```
docker build -t backend .

## Mac m1 실행의 경우
docker buildx build --platform linux/amd64 -t bakcend .

docker run --net="host" -p 8080:8080 app:0.1 
## 해당 도커 컨테이너에는 MySQL이 포함되어 있지 않으므로, 호스트 네트워크를 사용하도록 설정하고 DB URL 설정을 변경해야 한다.
```
