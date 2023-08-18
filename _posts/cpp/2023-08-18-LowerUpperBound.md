---
title: "[C++] lower_bound와 upper_bound와 equal_range"
categories: Cpp
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-08-18
last_modified_at: 2023-08-18
---

## 헤더파일

```c++
#include<algorithm>
```

<br>



## ❗주의점

lower_bound, upper_bound, equal_range는 모두 사용하기전에 **<u>정렬</u>**이 필요함.

 **<u>이진탐색</u>**을 기반으로 하기 때문.

<br>



## lower_bound 사용법

범위 `[first, last)` 안에서 **<u>value 이상</u>**인 첫 번째 반복자를 return함.

없다면 last에 해당하는 반복자를 리턴함.

이때 last는 `)` 범위이기 때문에, 찾으려는 범위의 바로 다음부분을 가리켜야함.

```c++
lower_bound(반복자 시작, 반복자 끝, value)
lower_bound(반복사 시작, 반복자 끝, value, comp함수)
///////////////////////////////////////////////////////////////////////
    
    
	vector<int> v{ 1,3,5 }; //정렬된 상태여야함

	auto itr = lower_bound(v.begin(), v.end(), 2);
	cout << *itr; //3출력됨

	itr = lower_bound(v.begin(), v.end(), 3);
	cout << *itr; //3출력됨
```

<br>



```c++
bool comp(const Type1 &a, const Type2 &b);
```

이때 `비교를 위한 이항함수인 comp함수`는 위와 같은 형식을 갖어야 함. 

파라미터가 `const &`  일 필요는 없지만 전달받은 원소를 수정하면 안되기 때문에 위처럼 썼음.

<br>



## upper_bound 사용법

범위 `[first, last)` 안에서 **<u>value 보다 큰</u>** 첫 번째 반복자를 return함.

없다면 last에 해당하 는 반복자를 리턴함.

이때 last는 `)` 범위이기 때문에, 찾으려는 범위의 바로 다음부분을 가리켜야함.

```c++
upper_bound(반복자 시작, 반복자 끝, value)
upper_bound(반복사 시작, 반복자 끝, value, comp함수)
///////////////////////////////////////////////////////////////////////
    
    
	vector<int> v{ 1,3,5 }; //정렬된 상태여야함

	auto itr = upper_bound(v.begin(), v.end(), 2);
	cout << *itr; //3출력됨

	itr = upper_bound(v.begin(), v.end(), 3);
	cout << *itr; //5출력됨
```

<br>



## equal_range 사용법

lower_bound와 upper_bound를 같이 묶어서 `std::pair` 로 리턴해줌.

(lower_bound가 first, upper_bound가 second)

```c++
vector<int> v{ 1,3,5 };

pair<vector<int>::iterator, vector<int>::iterator> itr = equal_range(v.begin(), v.end(), 3);
cout << "lower_bound는" << *(itr.first) << " upper_bound는" << *(itr.second);
//출력:  lower_bound는3 upper_bound는5
```

