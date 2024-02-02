---
layout: default
title: 개발환경 세팅하기 - 2
nav_order: 2
---

> 작성일: 2024-01-31

> Devdalus 프로젝트의 개발환경 세팅 소개문서입니다

## 목표 
1편에서 완료한 MySQL - JPA - SpringBoot 연동에 더해  
경량 관계형 데이터베이스인 H2데이터베이스를 연동하고,  
in-memory 모드를 사용해 테스트 코드를 작성합니다.

---

## H2 의존성 추가

H2 의존성을 `build.gradle` 파일에 추가합니다.

```
testImplementation 'com.h2database:h2'
```

{: .note}
테스트 용도로만 사용할 예정이기 때문에 testImplementation으로 설정하였습니다.

## application.yml 수정

당연하게도 application.yml에 h2 관련 접속정보를 추가하면 될 것 같지만..  
무작정 추가하게되면 스프링부트에서는 어떤 데이터베이스를 사용해야할지 모르게 됩니다.
<br>
이처럼 개발 / 배포 / 테스트에 대해서 환경변수들을 각각 따로 관리하고 싶을 때 사용하는것이 profile입니다.  
