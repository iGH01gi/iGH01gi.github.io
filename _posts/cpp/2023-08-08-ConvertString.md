---
title: "[C++] 숫자<->string 변환"
categories: Cpp
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-08-08
last_modified_at: 2023-08-08
---

<br>

# 🔘숫자를 String으로 변환



## 헤더파일

```c++
#include<string>
```

<br>

## 사용법

```c++
string str=to_string(2.3);

string str=to_string(1);
```

`to_string( )` 을 이용한다.

다양한 숫자타입을 받을수있게 오버라이딩 되어있다.

<br>

<br>

<br>

<br>



# 🔘string을 숫자로 변환

## 헤더파일

```c++
#include<string>
```

<br>

## 사용법

```c++
string intString="1";
int a=stoi(intString);

string longlongString="2";
long long int b=stol(longlongString);

string floatString="1.0";
float c=stof(floatString);

string doubleString="2.0";
double d=stod(doubleString);
```
