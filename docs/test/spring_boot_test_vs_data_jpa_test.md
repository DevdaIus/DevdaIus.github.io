---
layout: default
title: '@SpringBootTest vs @DataJpaTest'
parent: Test
has_children: false
---

> 작성일: 2024-02-15
> Written By: [Punkryn](https://github.com/punkryn)

# 정의
각 annotation의 용도와 쓰임에 대한 정의
## @SpringBootTest
공식문서에서는 Spring `ApplicationContext`를 생성해서 테스트 하고 `@ContextConfiguration`대신 사용되는 annotation이라고 한다.
그렇다면 `ApplicationContext`와 `@ContextConfiguration`은 무엇일까?

`ApplicationContext`는 스프링 컨테이너이다. BeanFactory의 하위 인터페이스로 BeanFactory에 기능을 추가한 인터페이스이다.
스프링 컨테이너라 함은 IoC 컨테이너를 의미하고 Spring Bean을 관리한다.

`@ContextConfiguration`은 공식 문서에 아래와 같이 적혀있다. 

{: .note}
@ContextConfiguration은 통합 테스트를 위해 ApplicationContext를 어떻게 로드하고 구성할지 결정하기 위해 사용되는 클래스 수준의 메타데이터를 정의합니다.

즉, `@SpringBootTest`는 ApplicationContext를 자동으로 구성하여 로드할 수 있도록 해주는 **통합테스트**를 위한 annotation이라 결론을 내릴 수 있다.

Controller를 test할 수 있는 것은 @SpringBootTest 덕분이다. 서버를 띄우지 않고 web `ApplicationContext`와 web environment를 제공해주기 때문에 테스트가 가능하다. 

참고로 `@Transactional`을 사용하면 매 테스트마다 롤백된다.

{: .note}
If your test is @Transactional, it rolls back the transaction at the end of each test method by default.

## @DataJpaTest
공식 문서에 의하면 JPA component를 위한 annotation이라고 한다. 
JPA component에 대한 설명이 나오지 않아서 @Repositoy나 @Entity 정도로 추정된다.

이 annotation을 사용하면 auto-configuration을 비활성화하고 JPA test와 관련된 configuration만 적용된다.


{: .note}
auto-configuration이란 Spring에서는 수동으로 해주어야 하는 설정들을 Spring Boot가 자동으로 해주는 것들을 의미함.

기본적으로 `@Transactional`에 의해 테스트마다 롤백이 되고 내장된 in-memory db를 사용한다. 
이러한 설정은 `@AutoConfigureTestDatabase`로 재정의 가능하다.

# 어떤 것을 사용해야할까?
`@SpringBootTest` + `@AutoConfigureTestDatabase` + `@Transactional`을 조합해서 사용하면 `@DataJpaTest`와 동일하게 동작하게 할 수 있다.

그렇다면 어떤 기준으로 전자를 선택할지 후자를 선택할지 결정해야 할까? \
`@DataJpaTest`을 사용하는 경우는 ApplicationContext가 필요없는 경우가 될 것이다. 즉, Repository Test와 같은 Unit 테스트에 알맞은 annotation이라 할 수 있다.

이와 다르게 ApplicationContext가 필요한 경우는 위의 조합으로 사용하는 것을 추천하고 있다.

{: .note}
If you are looking to load your full application configuration, but use an embedded database, you should consider @SpringBootTest combined with @AutoConfigureTestDatabase rather than this annotation.


# Reference
---
- [@SpringBootTest 공식 문서](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.testing)
- [@ContextConfiguration 공식 문서](https://docs.spring.io/spring-framework/reference/testing/annotations/integration-spring/annotation-contextconfiguration.html)
- [Spring ApplicationContext](https://www.baeldung.com/spring-application-context)
- [@SpringBootTest / @DataJpaTest 차이점 과 JPA 영속성 컨텍스트](https://cobbybb.tistory.com/23)
- [DataJpaTest](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/autoconfigure/orm/jpa/DataJpaTest.html)