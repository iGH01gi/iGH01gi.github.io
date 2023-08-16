---
title: "[C++] 이진 탐색 함수(binary_search)"
categories: Cpp
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-08-16
last_modified_at: 2023-08-16
---

<br>

c++에서는 탐색을 위한 `find( )` 함수를 제공하지만, 

**정렬된 상태**에서의 탐색속도는 `이진탐색(binary_search( ))`가 일반적으로 빠름. 

`find( )`함수는 만약에 찾았다면 해당하는 iterator를 return해주지만, 

`이진탐색(binary_search( ))` 의 경우에는 값이 존재한다or안한다에 해당하는 bool값을 return해줌.

<br>

따라서 배열의 경우에는 한번 정렬해놓고, 지속적으로 값의 존재여부를 파악하고싶을때 binary_search를 사용하면 유용함.

그러나 map같은 경우는 binary search tree이기 때문에 그냥 find( )를 사용하면 됨.

## 헤더파일

```c++
#include<algorithm>
```

<br>

## 사용법

```c++
vector<int> v={50,80,10,30};
sort(v.begin(),v.end()); //반드시 정렬이 필요함!

if (binary_search(v.begin(), v.end(), 10))
{
	cout<<"10이 존재합니다";
}
```

