---
title: "[C++] 배열,container의 누적 합"
categories: Cpp
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-08-09
last_modified_at: 2023-08-09
---

<br>

## 헤더파일

```c++
#include<numeric>
```

<br>

## 사용법

```c++
accumulate(시작 iterator, 끝 iterator, 초기값)

accumulate(시작 iterator, 끝 iterator, 초기값, 커스텀함수)
```

보통 단순한 누적합을 구하기 위해서는 첫번째 방식을 사용함.  

아래방식은 커스텀함수를 사용하는 방법인데, 예를들면 단순히 더하는 것이 아닌 2배를 해서 더하던가 빼던가 등의 구현이 가능해짐.

<br>

## 누적 합 예시 코드

```c++
#include<iostream>
#include<vector>
#include<numeric>

using namespace std;

int main()
{
	vector<int> v = { 1,2,3 };
	int result = accumulate(v.begin(), v.end(), 0);
	cout << result;
	//6 출력됨.
}
```

<br>

## 커스텀함수 예시 코드

```c++
// 1. 람다 함수 이용
vector<int> v = { 1,2,3 };
int result = accumulate(v.begin(), v.end(), 0, [](int x, int y) { return x - y; });
cout << result; //0-1-2-3 = -6출력됨


//2. 일반 함수 이용
int CustomFunc(int x, int y)
{
    return x-y;
}
vector<int> v = { 1,2,3 };
int result = accumulate(v.begin(), v.end(), 0, CustomFunc);
cout << result; //0-1-2-3 = -6출력됨
```

<br>

## `#include<functional>` 이용하기

funcional헤더는 c++의 여러 연산 정보를 담고있음. 

따라서 커스텀함수의 기능이 여기에 이미 정의되어있다면 굳이 커스텀으로 만들필요없이 갖다 쓰면 됨. 

사용하기 위해서는 반드시 `#include<functional>`을 해줘야 함.

```c++
//minus<int>()
vector<int> v = { 1,2,3 };
int result = accumulate(v.begin(), v.end(), 0, minus<int>());
cout << result; //0-1-2-3 = -6출력됨


//multiplies<int>()   
vector<int> v = { 1,2,3 };
int result = accumulate(v.begin(), v.end(), 1, multiplies<int>());
cout << result; //1*1*2*3 = 6출력됨
```

