---
title: "[C++] 올림,내림,버림,반올림"
categories: Cpp
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-07-05
last_modified_at: 2023-07-05
---

## 헤더파일

```c++
#include<cmath>
```

<br>



## 올림(ceil)

```c++
double ceil (double x);
float ceil (float x);
long double ceil (long double x);
```

<br>

사용 예

```c++
cout<<ceil(2.1); //결과:3
cout<<ceil(-3.2) //결과:-3
```

<br>



## 내림(floor)

```c++
double floor (double x);
float floor (float x);
long double floor (long double x);
```

<br>

사용 예

```c++
cout<<floor(2.1); //결과:2
cout<<floor(-3.5); //결과:-4
```

<br>



## 버림(trunc)

```c++
float trunc(float num);
double trunc(double num);
long double trunc(long double num);
double trunc(T num);
```

<br>

사용 예

```c++
cout<<trunc(2.1) //결과:2
cout<<trunc(-3.5) //결과:-3
```

<span style="color:green">**내림**</span>과 <span style="color:orange">**버림**</span>의 차이:

**음수**일떄

**floor(-3.5)는 -4  //**<span style="color:green">**내림**</span>

**trunc(-3.5)는 -3 //**<span style="color:orange">**버림**</span>

<br>



## 반올림(round)

```c++
double round(double num);
float round(float num);
long double round(long double num);
double round(T x);
```

<br>

사용 예

```c++
cout<<round(2.1);	//결과:2
cout<<round(2.5);	//결과:3
cout<<round(-3.5);	//결과:-4
cout<<round(-3.8);  //결과:-4
cout<<round(-3.2);  //결과:-3
```



