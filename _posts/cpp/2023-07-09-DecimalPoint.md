---
title: "[C++] 소수점 고정해서 출력"
categories: Cpp
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-07-09
last_modified_at: 2023-07-09
---

## 소수점 고정

```c++
cout<<fixed; 
cout.setf(ios::fixed);
```

위 두 코드 둘 중에 아무거나 써도 됨. 

보통 윗 방법으로 많이 쓰는 것 같음. 

그리고 위 코드를 치는 순간 **기본적으로 소숫점 6자리까지 출력이 됨**. (소숫점 7자리에서 반올림함)

 <br>

ex)

```c++
#include<iostream>
using namespace std;

int main()
{
   double r=1.123456789;
   cout<<fixed;
   cout<<r;
}

//출력 결과: 1.123457
```

<br>



## 소수점 자릿수 설정

```c++
cout.precision(7); //소숫점 7자리까지 표현. (소숫점 8자리에서 반올림함)
```

<br>



## 소수점 고정 해제

```c++
cout.unsetf(ios::fixed);
```

