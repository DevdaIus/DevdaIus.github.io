---
layout: default
title: 개발환경 세팅하기 - 1
parent: DevOps
nav_order: 2
has_children: false
---

> 작성일: 2024-01-29  
> Written By: [ClayCat](https://github.com/claycat)

> Devdalus 프로젝트의 개발환경 세팅 소개문서입니다

## 목표
SpringBoot로 생성된 웹서버와 도커 컨테이너로 실행된 MySQL 클라이언트를 연동합니다.

## 가정
SpringBoot를 통해서 프로젝트를 생성하였고, Docker 및   docker-compose가  
설치되었다는것을 가정합니다.

---

### **Docker-compose 파일 작성하기**

먼저 docker-compose 파일을 작성합니다.   
개발환경을 위한 compose 파일이기 때문에 docker-compose.dev.yml 이라는 파일명으로 생성합니다.

```yaml
## 최상단 디렉토리에 docker-compose.dev.yml 생성

services:
  mysql:
    image: mysql:8.0.33
    ports:
      - 43306:3306
    volumes:
      - ./db/mysql/data:/var/lib/mysql
      - ./db/mysql/init:/docker-entrypoint-initdb.d
    command:
      - '--character-set-server=utf8mb4'
      - '--collation-server=utf8mb4_unicode_ci'
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: devdalus
```

### **Container Test**

정상적으로 docker compose 파일이 작성되었는지 확인합니다.   
-f 옵션은 파일명을 특정하기 위해서, -d 는 백그라운드 실행을 위해 추가합니다.

```yaml
docker-compose -f docker-compose.dev.yml -d
## 잠시 기다린 뒤
docker ps ## 컨테이너 목록이 나타나면 성공입니다
```
### **MySQL Test**
해당 컨테이너에 접속하여 MySQL이 정상적으로 동작하는지 확인합니다
```yaml
docker ps ## 컨테이너 id 가 나오면 복사해둡니다
docker exec -it container_id bash
mysql -u root -p -h localhost -P 43306(또는 지정한 포트)

## 아래 프롬프트가 나오면 성공입니다
mysql>
```

---

## **SpringBoot Settings**

### **build.gradle**

`build.gradle`` 파일에 의존성을 추가합니다
(maven 관련 취약점으로 인해 8.2.0으로 넣었습니다)

```
dependencies {
	...
	runtimeOnly 'com.mysql:mysql-connector-j:8.2.0'
}
```

{: .note}
여기서 **implementation이** 아닌 **runtimeOnly로** 지정했습니다.  
implementation의 경우, compile time(compileClassPath)에 해당 의존성을 요구하고,  
runTimeOnly의 경우, 런타임(runtimeClassPath)에 요구합니다.   
코드 변경이 일어나도 재컴파일이 필요하지 않기 때문에 **rutimeOnly로** 설정하였습니다.

### **applications.yml**

`/src/main/resources` 안에 `application.yml` 파일을 생성합니다.
(`application.properties`가 기본 설정이라면  지우고 대체합니다)

```yaml
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:43306/devdalus?useSSL=false&serverTimezone=UTC

    username: root
    password: password
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    database-platform: org.hibernate.dialect.MySQL8Dialect
```

도커 컨테이너의 외부 포트인 43306번으로 연결해주었습니다.  
정상적으로 애플리케이션이 실행된다면 완성입니다.