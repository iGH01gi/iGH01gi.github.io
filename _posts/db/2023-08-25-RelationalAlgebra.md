---
title: "[DB] 관계대수(Relational Algebra)"
categories: Db
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-08-25
last_modified_at: 2023-08-25
---

> 이미지는 [Database System Concepts](https://db-book.com/) 7판의 이미지를 사용함.

## 관계대수란?

- 데이터베이스 이론에서 관계 대수는 대수 구조를 사용하여 데이터를 모델링하고 그에 대한 쿼리를 잘 정립된 의미론으로 정의하는 이론
- 관계 대수의 주요 응용은 주로 관계형 데이터베이스, 특히 SQL과 같은 쿼리 언어를 위한 이론적 기반을 제공하는 데 사용됨
- relation은 set이기 때문에 그 결과는 **중복이 없음**.

<br>





## 사용되는 연산자들

- select : **σ**
- project: **π**
- cartesian product: **X** 
- theta join: **⨝**<sub>**AθB**
- natural join: **⨝**
- union operation: **∪**
- set-intersection: **∩**
- set-difference: **-**
- assignment: **←**
- rename: **ρ**
- division: **÷**

> 이중에서 기본 연산자는 select(**σ**), project(**π**), cartesian product(**X**), union operation(**∪**), set-difference(**-**), rename(**ρ**) 이렇게 총 6개임
>
> 위 6개의 연산자로 모든 관계를 서술 할 수 있음.
>
> 다른 연산자들은 편의상 만들어짐

<br>





## select: σ

조건문

- `=` ,  `≠` , `>` , `≥` , `<` , `≤` 를 select문에서 사용 가능
- ∧(**and**), ∨(**or**), ¬ (**not**) 를 select문에서 사용 가능![image-20230825222416070](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230825222416070.png)
- 중복되는 rows가 없음. (중복을 제거함. 하나만 남게)

<br>

ex) instructor테이블에서 dept_name이 Physics인 것들을 가져옴

![image-20230825221154766](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230825221154766.png)

<br>





## project: π

- 인자로 받은 릴레이션에서 특정 속성들만을 가져오기위해 사용
- unary operation 임
- 아래 그림에서 A1~Ak는 속성의 이름이고 r은 릴레이션의 이름  
  ![image-20230825222655668](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230825222655668.png)
- 중복되는 rows가 없음. (중복을 제거함. 하나만 남게)
- SQL에서 SELECT DISTINCT문에 해당됨

<br>

ex)

![image-20230825222601588](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230825222601588.png)

<br>

select문과 섞어서 쓰는것도 가능

![image-20230825223704695](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230825223704695.png)

<br>





## cartesian product: X

가능한 경우를 모두 조합함. 

위 예시의 경우 instructor와 teaches 테이블에 동일한 이름의 ID 속성이 존재하기때문에 instructor.ID와 teaches.ID를 통해서 구분해줬음.

<br>

ex)

![image-20230825235513988](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230825235513988.png)

<br>





## theta join: **⨝** <sub>AθB

![image-20230826033126031](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230826033126031.png)

- θ는 비교연산자( `=` ,  `≠` , `>` , `≥` , `<` , `≤` )를 사용한 식이 옴.

<br>

ex) 

![image-20230826035610508](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230826035610508.png)이거랑

 ![image-20230826035623508](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230826035623508.png) 이것은 같은 뜻임.

위 예시의 연산의 결과는

![image-20230826035746959](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230826035746959.png)





## natural join:  ⨝

- theta join에서 θ가 `=` 인 경우. 자주 쓰여서 따로 용어가 있음.

- 두 릴레이션에서 **컬럼명이 같은 모든 컬럼간의 equi-join**을 수행하는 것임.

<br>

ex) 

릴레이션 r의 속성을 ( A, B, C )

릴레이션 s의 속성을 ( A, D )라고 가정했을때

![image-20230826072513123](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230826072513123.png)

<br>





## union :  ∪

2개의 릴레이션을 섞는 합치는 용도

r ∪ s 연산을 하기 위해서 필요한 조건은 (r과 s 는 릴레이션임)

- r, s는 동일한 개수의 속성을 지녀야 함 (same arity)
- r, s의 각 속성은 서로 compatible 해야함. 

<br>

ex)

![image-20230826063758399](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230826063758399.png)

<br>





## set-intersection: ∩

2개의 릴레이션에서 공통부분을 얻는 용도

r ∩ s 연산을 하기 위해서 필요한 조건은 (r과 s 는 릴레이션임)

- r, s는 동일한 개수의 속성을 지녀야 함 (same arity)
- r, s의 각 속성은 서로 compatible 해야함. 

<br>

ex)

![image-20230826064421700](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230826064421700.png)

<br>





## set-difference: -

2개의 릴레이션에서 하나의 릴레이션을 기준으로 다른 릴레이션에는 들어있지 않은 부분만 얻는 용도

r - s 연산을 하기 위해서 필요한 조건은 (r과 s 는 릴레이션임)

- r, s는 동일한 개수의 속성을 지녀야 함 (same arity)
- r, s의 각 속성은 서로 compatible 해야함. 

<br>

ex)

![image-20230826064819128](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230826064819128.png)

<br>





## assignment: ←

- 관계 대수식을 작성할 때, 일부를 임시 관계 변수에 할당하여 표현하기위해 사용. (편의성,가시성)
- 코딩할때 변수를 할당하는 이유와 비슷

<br>

ex)

![image-20230826065518263](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230826065518263.png)

<br>





## rename: ρ

- 릴레이션의 이름, 릴레이션의 이름+속성의이름을 변경하기 위해 사용

<br>

ex) 릴레이션 E 의 이름만 x로 변경할 때

![image-20230826071039838](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230826071039838.png)

ex) 릴레이션 E의 이름을 x로 변경하고 각 속성의 이름을 A1~An으로 변경할 때

![image-20230826071114580](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230826071114580.png)

<br>





## division: ÷

예시를 보고 이해하는것이 빠름

![image-20230826073020574](./../../assets/images/2023-08-25-RelationalAlgebra/image-20230826073020574.png)
