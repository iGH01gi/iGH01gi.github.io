---
title: "[C++] 구분자를 이용한 문자열 입력받기"
categories: Cpp
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-07-14
last_modified_at: 2023-07-14
---

기본적으로 cin을 이용한 입력을 받지만, "Hello World" 처럼 띄어쓰기가 포함된 문장이라면 Hello까지만 읽게됨.

cin의 >> 연산자에서 공백문자를 구분자로 하여 입력을 끊기 때문에 그런것인데, 이를 해결하기 위한 방법을 소개함.

<br>





# <span style="color: #D6ABFA;">getline</span>

## 헤더파일

```c++
#include<string>
```

<br>





## 사용법

```c++
getline(입력스트림 오브젝트, 문자열을 저장할 string 객체, 구분자)
    //구분자를 입력 안하면 자동으로 '\n'를 구분자로 사용.

string str;
getline(cin, str, '-');
```

<br>





## 주의점

```c++
int n;
string str;
cin >> n;
getline(cin, str);
```

위처럼 사용하면, n을 입력받은 후, 버퍼에 눌렀던 엔터('\n')가 그대로 남아있어서 getline()에 들어가기 때문에 getline부분이 의도된대로 실행되지 않음. 

따라서 str에는 아무것도 들어가지 않게됨. 

<br>

**해결법**

```c++
int n;
string str;
cin >> n;
cin.ignore();
getline(cin, str);
```

`cin.ignore()` 를 사용해서 입력 버퍼의 모든 내용을 제거해주면 정상적으로 작동함.

<br>

<br>

<br>

<br>

# <span style="color: #D6ABFA;">cin.getline</span>

## 헤더파일

```c++
#include<istream> //iostream에 포함되어있음
```

<br>





## 사용법

```c++
cin.getline(변수 주소, 최대 입력 가능 문자수, 종결 문자);
//종결문자를 안적으면 '\n'로 자동설정

cin.getline(char* str, streamsize n);
cin.getline(char* str, streamsize n, char dlim);
```

- 문자 배열이며 마지막 글자가 '\0'인 c-string을 입력받는 용.
- 종결문자 전까지 읽어서 저장함.
- n-1 개의 문자 개수만큼 읽어와 str에 저장 (n번째 문자는 NULL('\0')로 바꿈)



## 주의점

```c++
char str[3];
int n;
cin >> n;
cin.getline(str, 3,'-');
cout << str;
```

위 처럼 n을 cin으로 입력받으면, 버퍼에 '\n'이 남아있기 때문에, 위 경우에서는 str의 첫부분에 \n이 들어가게 됨. 

<br>

**해결법**

```c++
char str[3];
int n;
cin >> n;
cin.ignore();
cin.getline(str, 3,'-');
cout << str;
```

따라서 이를 막기 위해서는 `cin.ignore( )`로 버퍼를 비워주면 됨.

<br>

<br>

<br>

<br>



# <span style="color: #D6ABFA;">cin.get</span>

## 헤더파일

```c++
#include<istream> //iostream에 포함되어있음
```

<br>





## 사용법

```c++
char ch1, ch2;
ch1 = cin.get();
ch2 = cin.get();
```

- 표준 입력 버퍼에서 문자를 하나만 가져옴.
- 문자 하나만 입력이 가능하며 공백, 개행도 입력으로 인식함.
