---
title: "[C++] 문자열 자르는 방법"
categories: Cpp
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-07-16
last_modified_at: 2023-07-16
---

# <span style="color: #D6ABFA;">substr</span>

## 헤더파일

```c++
#include<string>
```

<br>

## 사용법

```c++

스트링변수.substr(pos , count);

-스트링변수의 pos번째부터(인덱스) count 길이 만큼 자른 string을 return함.
-count자리에 값을 전달안하거나 string::npos를 전달하면 pos번째부터 끝까지 자른 string을 return함.
-pos가 문자열을 벗어나면 std::out_of_range 예외 발생.

---------------------------------------------------------------------------
string str="0123456";
string result=str.substr(2,3);
cout<<result; //출력:234
    
```

<br>

<br>

<br>

<br>

# <span style="color: #D6ABFA;">substr과 find 동시 사용</span>

## 헤더파일

```c++
#include<string>
```

<br>

## 사용법

- `find( separator , index )` 는 인자로 전달된 Index부터 탐색을 시작하여 처음으로 발견된 separator를 찾고 그곳의 index를 리턴함.

- 만약, separator를 찾지 못했다면 string::npos를 리턴함.

```c++
#include<iostream>
#include<string>
using namespace std;

int main()
{
	string str = "Hello,World,C++";
	string separator = ",";

	int cur_position = 0;
	int separator_position;

	while ((separator_position = str.find(separator, cur_position)) != string::npos)
	{
		int len = separator_position - cur_position;

		string result = str.substr(cur_position, len);
		cout << result << endl;

		cur_position = separator_position + 1;
	}

	cout << str.substr(cur_position);//마지막 부분 출력용
}

//출력 결과:
Hello
World
C++
```

<br>

<br>

<br>

<br>

# <span style="color: #D6ABFA;">getline과 istringstream 동시 사용</span>

## 헤더파일

```c++
#include<string>
#include<sstream> 
```

<br>

## 사용법

문자열을 `istringstream`으로 변환하고

`getline( )` 을 통해서 구분자를 기준으로 `istringstream` 으로부터 문자열을 읽어옴.

```c++
#include<iostream>
#include<string>
#include<sstream>

int main() 
{

	std::string str = "Hello,World,C++";
	char separator = ',';
	std::istringstream iss(str);
	std::string str_buf;
	while (getline(iss, str_buf, separator)) 
	{
		std::cout << str_buf << std::endl;
	}

}

//출력 결과:
Hello
World
C++
```

