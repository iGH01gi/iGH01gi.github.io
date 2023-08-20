---
title: "[C++] Iterator 조작"
categories: Cpp
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-08-21
last_modified_at: 2023-08-21
---

## next 사용법

`std::next(반복자 , n)` 

반복자로부터 n만큼 다음에 위치한 반복자를 return함.

(단, n이 음수면 |n|만큼 이전에 위치한 반복자를 return)

```c++
vector<int> v = { 0,1,2 };
auto itr=v.begin();

itr=next(itr,2);
cout<<*itr; //1출력됨
```

<br>





## prev 사용법

`std::prev(반복자 , n)`

반복자로부터 n만큼 이전에 위치한 반복자를 return함.

(단, n이 음수면 |n|만큼 다음에 위치한 반복자를 return)

```c++
vector<int> v = { 0,1,2 };
auto itr=v.end();

itr=prev(itr,2);
cout<<*itr; //0출력됨
```

<br>





## advance 사용법

`std::advance(반복자 , n)`

반복자로부터 

- **n이 양수일 경우**=> n 만큼 다음에 위치한 반복자를,

- **n이 음수일 경우**=> n 만큼 이전에 위치한 반복자를

첫번째 인자로 넣어준 반복자변수에 저장함.

```c++
vector<int> v = { 0,1,2 };
auto itr=v.begin();
itr++;

advance(itr,-1);
cout<<*itr; //0출력됨

advance(itr,2);
cout<<*itr; //2출력됨

```

