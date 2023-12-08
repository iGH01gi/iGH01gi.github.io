---
title: "[Spring] 스프링 입문 - 6-5.스프링 데이터 JPA"
categories: Spring
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-12-06
last_modified_at: 2023-12-06
---

<a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8" target="_blank">
  <img src="./../../assets/images/2023-11-23-VLSM/325630-eng.png" alt="325630-eng" style="zoom: 50%;" />
</a>

```
본 시리즈는 인프런 김영한님의
'스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC,DB 접근 기술'
을 보고 공부용으로 작성한 것입니다.
```

<br>

<br>

<br>



# <span style="color: #D6ABFA;">⚪스프링 데이터 JPA</span>

스프링 부트와 JPA만 사용해도 개발 생산성이 정말 많이 증가하고, 개발해야할 코드도 확연히 줄어들게 됨

여기에 스프 링 데이터 JPA를 사용하면, 리포지토리에 구현 클래스 없이 인터페이스 만으로 개 발을 완료할 수 있음

그리고 반복 개발해온 기본 CRUD 기능도 스프링 데이터 JPA가 모두 제공함

실무에서 관계형 데이터베이스를 사용한다면 스프링 데이터 JPA는 이제 선택이 아니라 필수

> **주의** : 
>
> 스프링 데이터 JPA는 JPA를 편리하게 사용하도록 도와주는 기술입니다. 
>
> 따라서 JPA를 먼저 학습한 후에 스프링 데이터 JPA를 학습해야 합니다.

<br>

<br>

<br>

# <span style="color: #D6ABFA;">⚪환경 설정</span>

JPA 환경설정과 동일

## 🔹build.gradle  설정

build.gradle 파일에 JPA, h2 데이터베이스 관련 라이브러리 추가

```java
dependencies {
	implementation("org.springframework.boot:spring-boot-starter-thymeleaf")
	implementation("org.springframework.boot:spring-boot-starter-web")
	testImplementation("org.springframework.boot:spring-boot-starter-test")

	//implementation ("org.springframework.boot:spring-boot-starter-jdbc")
	implementation ("org.springframework.boot:spring-boot-starter-data-jpa") //이걸 추가
	runtimeOnly ("com.h2database:h2")
}
```

- spring-boot-starter-data-jpa 는 내부에 jdbc 관련 라이브러리를 포함한다. 따라서 jdbc는 제거해도 된다

## 🔹application.properties 설정

```properties
spring.datasource.url=jdbc:h2:tcp://localhost/~/test
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa


//아래 두개가 추가된 부분
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=none
```

> **주의**!
>
> 스프링부트 2.4부터는 spring.datasource.username=sa 를 꼭 추가해주어야 한다. 그렇지 않으면 오류가 발생한다

- **show-sql** : JPA가 생성하는 SQL을 출력한다
- **ddl-auto** : JPA는 테이블을 자동으로 생성하는 기능을 제공하는데 none 를 사용하면 해당 기능을 끈다
  - create 를 사용하면 엔티티 정보를 바탕으로 테이블도 직접 생성해준다

<br>

<br>

<br>

# <span style="color: #D6ABFA;">⚪스프링 데이터 JPA 회원 리포지토리</span>

```java
package hello.hellospring.repository;

import hello.hellospring.domain.Member;
import org.springframework.data.jpa.repository.JpaRepository;

import java.util.Optional;

public interface SpringDataJpaMemberRepository extends JpaRepository<Member, Long>, MemberRepository {
    
    @Override
    Optional<Member> findByName(String name);
}
```

- 리포지토리인데 interface임
- JpaRepository(인터페이스임)를 extends해야함
- JpaRepository를 extends 하면 스프링에서 해당 인터페이스의 **구현체를 자동으로 만들어주고, 스프링 빈에 자동으로 등록**함

<br>

findByName은 JpaRepository에 있는 공통 인터페이스가 아니기때문에 자동으로 구현을 해줄수 있는 부분이 아님.

따라서 @Override해서 따로 써줘야 함

그런데 이 **메소드 이름에도 규칙**이 존재해서

```java
    @Override
    Optional<Member> findByName(String name);
```

이렇게 써주는 순간

```sql
select m from Member m where m.name = ?
```

과 같은 JPQL을 짜주는 메소드로 구현을 해줌

즉, 실제 구현체를 직접 안만들고도 이름만보고도 구현을 해준다는 뜻임

<br>

<br>

<br>

# <span style="color: #D6ABFA;">⚪스프링 설정 변경</span>

스프링 데이터 JPA 회원 리포지토리를 사용하도록 스프링 설정 변경

```java
package hello.hellospring;

import hello.hellospring.repository.*;
import hello.hellospring.service.MemberService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;


@Configuration
public class SpringConfig {
    private final MemberRepository memberRepository;

    @Autowired
    public SpringConfig(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    @Bean
    public MemberService memberService() {
        return new MemberService(memberRepository);
    }
}
```

MemberRepository 스프링 빈을

```java
interface SpringDataJpaMemberRepository extends JpaRepository<Member, Long>, MemberRepository
```

이 과정에서 자동으로 구현체를 스프링에서 생성해주고 스프링빈에 등록해주었기 때문에 위와같은 코딩이 가능해짐

