---
title: "[Spring] 스프링 핵심 원리(기본편) - 1.객체 지향 설계와 스프링"
categories: Spring
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-12-08
last_modified_at: 2023-12-08
---

<a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8" target="_blank">
  <img src="./../../assets/images/2023-12-08-SpringCoreOop/cr.png" alt="325630-eng" style="zoom: 50%;" />
</a>

```
본 시리즈는 인프런 김영한님의
'스프링 핵심 원리 - 기본편'
을 보고 공부용으로 작성한 것입니다.
```

<br>

<br>

<br>

# <span style="color: #D6ABFA;">⚪객체 지향 특징</span>

## 🔹추상화

- 어떤 대상/집단의 공통적이고 본질적인 특징을 추출하여 정의한 것
- abstract class와 interface 등이 그 예시

## 🔹캡슐화

- 클래스 내의 속성이나 함수를 캡슐로 묶어 외부로부터 접근을 최소화 함
- 필요한 요소만 노출하고 상세 동작은 은닉
- 객체 간 결합도를 감소시켜 응집도를 강화해줌 (유지보수 good)

## 🔹상속

- 기존에 구현한 클래스등을 이어 받아서 확장 가능
- 코드 재사용성을 높임

## 🔹다형성

- 객체 지향의 핵심
- 객체 그 자체, 속성, 기능이 상황에 따라 여러 형태로 변할 수 있는 것
- 상위 객체의 타입으로 하위 객체를 참조 (ex. 인터페이스로 구현체 참조)
- 메소드 오버라이딩/오버 로딩

<br>

<br>

<br>

# <span style="color: #D6ABFA;">⚪SOLID 원칙</span>

## 🔹SRP

- 단일 책임 원칙(Single Responsibility principle)
- 한 클래스는 하나의 책임만 가져아 함
- 중요한 기준은 변경. 변경이 있을때 파급 효과가 적으면 잘 지킨 것
- ex) UI 변경, 객체의 생성과 사용을 분리

## 🔹OCP

- 개방-폐쇄 원칙(Open/Closed principle)
- 확장에는 열려 있으나 변경에는 닫혀있어야 함
- 다형성을 활용하면 가능!
- 인터페이스를 구현한 새로운 클래스를 하나 만들어서 새로운 기능을 구현

## 🔹LSP

- 리스코프 치환 원칙(Liskov Substitution Principle)
- 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다
- 다형성에서 하위 클래스는 인터페이스 규약을 다 지켜야 한다는 것, 다형성을 지원하기 위 한 원칙, 인터페이스를 구현한 구현체는 믿고 사용하려면, 이 원칙이 필요하다
- 단순히 컴파일에 성공하는 것을 넘어서는 이야기
-  예) 자동차 인터페이스의 엑셀은 앞으로 가라는 기능, 뒤로 가게 구현하면 LSP 위반, 느리 더라도 앞으로 가야함

## 🔹ISP

- 인터페이스 분리 원칙(Interface Segregation Principle)
- 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다
- ex) 자동차 인터페이스 -> 운전 인터페이스, 정비 인터페이스로 분리
- 인터페이스가 명확해지고, 대체 가능성이 높아진다.

## 🔹DIP

- 의존관계 역전 원칙(Dependency Inversion Principle)
- 추상화에 의존해야지, 구체화에 의존하면 안된다 (의존성 주입(DI)은 이 원칙 을 따르는 방법 중 하나)
- 쉽게 이야기해서 구현 클래스에 의존하지 말고, 인터페이스에 의존하라는 뜻

<br>

<br>

<br>

# <span style="color: #D6ABFA;">⚪객체 지향 설계와 스프링</span>

- 스프링은 다음 기술로 다형성 + OCP, DIP를 가능하게 지원 
  - DI(Dependency Injection): 의존관계, 의존성 주입
  - DI 컨테이너 제공
- 클라이언트 코드의 변경 없이 기능 확장
- 쉽게 부품을 교체하듯이 개발

```java
//DIP, OCP 위반
//MemberRepository는 인터페이스
//MemoryMemberRepository는 인터페이스의 구현체
public class MemberService {
    
    private MemberRepository memberRepository = new MemoryMemberRepository();
    
}
```

만약에 위처럼 스프링의 DI 기능(스프링 빈, 컨테이너)을 사용하지 않는다면 

MemberService는 MemberRepository라는 추상화(인터페이스)에도 의존하지만 구체화(MemoryMemberRepository)에도 의존하게 된다

즉 DIP와 OCP(구현 객체를 변경하였을때 MemberService내의 코드도 바꿔줘야 해서)를 위반하게 됨