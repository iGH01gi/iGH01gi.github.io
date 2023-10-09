---
title: "[DB] SQL 테이블 생성"
categories: Db
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-10-09
last_modified_at: 2023-10-09

---

> MariaDB를 기준으로 함

# ⚪<span style="color: #D6ABFA;">생성법</span>

```sql
CREATE TABLE table_name
(
    'col이름1' VARCHAR(10) NULL COMMENT '주석' COLLATE 'utf8mb4_general_ci',
    'col이름2' INT NOT NULL DEFAULT NULL  COMMENT '주석',
    'col이름3' DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP(),
    PRIMARY KEY('col이름1')
)
COLLATE='utf8mb4_general_ci'
ENGINE=InnoDB
comment '주석';
```

- **CREATE TABLE** : SQL명령
- **table_name** : 생성하려는 테이블 이름
- **'col이름1'** : 열 이름
- **VARCHAR(10)** : 데이터 유형 및 길이 ([참고](https://igh01gi.github.io/db/MariaDbDataTypes/))
- **NULL** : null 허용
- **DEFAULT NULL** : 값을 입력안했을때 해당 열의 기본값을 NULL로 설정. NULL말고도 다른것도 가능(예. DEFAUILT CURRENT_TIMESTAMP())
- **COMMENT '주석'** : 해당 열에 대한 설명. 
- **PRIMARY KEY('col이름1')** : 기본키 제약사항 설정
- **COLLATE='utf8mb4_general_ci'** : 테이블의 문자 셋 설정 (MariaDB 설치할 때 "Use UTF8 as default server's character set" 옵션 선택으로 MariaDB전체에서 기본값으로 적용되는 문자 셋)
- **ENGINE=InnoDB** : MariaDB에서 제공하는 여러 데이터베이스 엔진 중 InnoDB사용

<br>

<br>

<br>



# ⚪<span style="color: #D6ABFA;">외래키 설정</span>

```sql
CREATE TABLE table_name
(
    ...
    foreign key(열 이름) references 다른테이블명(다른테이블의 열 이름)
)
```

- **foreign key(열 이름) references 다른테이블명(다른테이블의 열 이름)** 

<br>

<br>

<br>



