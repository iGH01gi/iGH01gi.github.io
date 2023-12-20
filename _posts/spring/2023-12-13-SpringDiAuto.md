---
title: "[Spring] 스프링 핵심 원리(기본편) - 6.의존관계 자동 주입"
categories: Spring
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-12-13
last_modified_at: 2023-12-13
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

# <span style="color: #D6ABFA;">⚪의존 관계 주입 방법</span>

<div class="notice--warning" markdown="1">

**참고**   

**@Autowired** 의 기본 동작은 주입할 대상이 없으면 오류가 발생한다. 

주입할 대상이 없어도 동작하게 하려면 **@Autowired(required = false)** 로 지정하면 된다

</div>

<div class="notice--warning" markdown="1">

**참고**   

의존관계 자동 주입은 스프링 컨테이너가 관리하는 스프링 빈이어야 동작한다.  

스프링 빈이 아닌 Member 같은 클래스에서 **@Autowired** 코드를 적용해도 아무 기능도 동작하지 않는다

</div>

## 🔹생성자 주입

```java
@Component
public class OrderServiceImpl implements OrderService {
    
	private final MemberRepository memberRepository;
	private final DiscountPolicy discountPolicy;
    
 	@Autowired
	public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
 		this.memberRepository = memberRepository;
		this.discountPolicy = discountPolicy;
	}
}
```

- 생성자가 딱 1개만 있으면 @Autowired를 생략해도 자동 주입 됨 (물론 스프링 빈에만 해당)
- 생성자 호출시점에 딱 1번만 호출되는 것이 보장
- **불변, 필수** 의존관계에 사용

## 🔹수정자 주입(setter 주입)

```java
@Component
public class OrderServiceImpl implements OrderService {
    
     private MemberRepository memberRepository;
     private DiscountPolicy discountPolicy;
    
     @Autowired
     public void setMemberRepository(MemberRepository memberRepository) {
     	this.memberRepository = memberRepository;
     }
    
     @Autowired
     public void setDiscountPolicy(DiscountPolicy discountPolicy) {
     	this.discountPolicy = discountPolicy;
     }
}

```

- setter라 불리는 필드의 값을 변경하는 수정자 메서드를 통해서 의존관계를 주입하는 방법
- 특징 
  - **선택, 변경** 가능성이 있는 의존관계에 사용 
  - 자바빈 프로퍼티 규약의 수정자 메서드 방식을 사용하는 방법

## 🔹필드 주입

```java
@Component
public class OrderServiceImpl implements OrderService {
    
     @Autowired
     private MemberRepository memberRepository;
    
     @Autowired
     private DiscountPolicy discountPolicy;
}
```

- DI 프레임워크가 없으면 아무것도 할 수 없다
- 외부에서 변경이 불가능해서 테스트 하기 힘들다는 치명적인 단점
- 사용하지 말자 (테스트코드나 스프링 설정을 목적으로 하는 @Configuration 같은 곳에서만 특별한 용도로 사용)

## 🔹@Bean에서 파라미터

```java
@Bean
OrderService orderService(MemberRepository memberRepoisitory, DiscountPolicy discountPolicy) {
 	return new OrderServiceImpl(memberRepository, discountPolicy);
}
```

- 다음 코드와 같이 @Bean 에서 파라미터에 의존관계는 자동 주입됨

## 🔹일반 메서드 주입

```java
@Component
public class OrderServiceImpl implements OrderService {
    
     private MemberRepository memberRepository;
     private DiscountPolicy discountPolicy;
    
     @Autowired
     public void init(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
         this.memberRepository = memberRepository;
         this.discountPolicy = discountPolicy;
     }
}
```

- 한번에 여러 필드를 주입 받을 수 있다
- 일반적으로 잘 사용하지 않는다

<br>

<br>

<br>

# <span style="color: #D6ABFA;">⚪옵션 처리</span>

주입할 스프링 빈이 없어도 동작해야 할 때,

```@Autowired``` 만 사용하면 ```required``` 옵션의 기본값이 ```true``` 로 되어 있어서 자동 주입 대상이 없으면 오류가 발생한다

<br>

자동 주입 대상을 옵션으로 처리하는 방법은 다음과 같다

- ```@Autowired(required=false)``` : 자동 주입할 대상이 없으면 수정자 메서드 자체가 호출 안됨
- ```org.springframework.lang.@Nullable``` : 자동 주입할 대상이 없으면 null이 입력된다
- ```Optional<>``` : 자동 주입할 대상이 없으면 Optional.empty 가 입력된다

예제)

```java
    @Test
    void ttest(){
        ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfigTest.class);
    }

    @Configuration
    public static class AppConfigTest {

        //호출 안됨
        @Autowired(required = false)
        public void setNoBean1(Member member) {
            System.out.println("setNoBean1 = " + member);
        }
        
        //null 호출
        @Autowired
        public void setNoBean2(@Nullable Member member) {
            System.out.println("setNoBean2 = " + member);
        }
        
        //Optional.empty 호출
        @Autowired(required = false)
        public void setNoBean3(Optional<Member> member) {
            System.out.println("setNoBean3 = " + member);
        }
    }
```

출력)

```
setNoBean2 = null
setNoBean3 = Optional.empty
```

- Member는 스프링 빈이 아님
- ```setNoBean1()``` 은 ```@Autowired(required=false)``` 이므로 호출 자체가 안된다

>**참고**
>
>@Nullable, Optional은 스프링 전반에 걸쳐서 지원된다. 
>
>예를 들어서 생성자 자동 주입에서 특정 필드에만 사용해도 된다.

<br>

<br>

<br>

# <span style="color: #D6ABFA;">⚪생성자 주입을 선택해라!</span>

## 🔹불변

- 대부분의 의존관계 주입은 한번 일어나면 애플리케이션 종료시점까지 의존관계를 변경할 일이 없다. 오히려 대부 분의 의존관계는 애플리케이션 종료 전까지 변하면 안된다.(불변해야 한다.)
- 수정자 주입을 사용하면, setXxx 메서드를 public으로 열어두어야 한다
- 누군가 실수로 변경할 수 도 있고, 변경하면 안되는 메서드를 열어두는 것은 좋은 설계 방법이 아니다
- 생성자 주입은 객체를 생성할 때 딱 1번만 호출되므로 이후에 호출되는 일이 없다. 따라서 **불변**하게 설계할 수 있 다

## 🔹누락

