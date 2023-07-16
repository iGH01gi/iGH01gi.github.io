---
title: "[C++] 배열을 매개변수로 받는 다양한 방법"
categories: Cpp
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-07-09
last_modified_at: 2023-07-09
---

C++ 사용자라면, 매개변수를 받을때 참조(&)로 받는 것이 효율적이고 자주 사용한다는 것을 알 것임.

근데 배열은 어떤식으로 받아야 효율적일까? 

그 방법들을 소개하고자 함.

<br>





## 불가능한 방법

일단 이런 형식을 생각해 볼 수 있음. (받는 것이 10칸짜리 배열이라 가정)

```c++
void func(int &arr[10])
{
}
```

그냥 다른 참조 쓰듯이 똑같이 int &arr[10] 이런식으로 매개변수를 받을 수 있을까?

정답은 **불가능** 임. 

c++에서 위와같은 문법은 금지되어 있음.

```
[ ]의 연산 우선순위가 &보다 높기 때문에 괄호가 없다면 int &(ref[3]) 과 같이 선언되기 때문이라고 생각합니다.
```

<br>





## 포인터로 배열 받기

```c++
void func(int* arr)
{
}
```

위 방법은 가능. 

흔한 포인터를 사용한 방법. 

대신 배열의 범위를 벗어나지 않도록 주의해야함.

<br>

```c++
void func(int arr[100])  //int *arr 과 똑같다!!!!!
{
}
```

여기서 위와같이, 난 100칸의 배열을 인자로 받을테야!!

하고, int arr[100]을 매개변수자리에 쓸 수 도 있지만 

사실 **int\* arr과 똑같은 처리**임.

즉, **실은 포인터로 처리하고** 있기때문에, 배열의 범위를 마찬가지로 신경써줘야 함.

(범위기반 for문도 쓰지 못함! 단순 포인터로 처리하기 때문에)

<br>

```c++
void func(int arr[])  //int *arr 과 똑같다!!!!!
{
}
```

그렇기 때문에 위처럼 [ ] 안의 숫자를 생략해도 됨. (마찬가지로 포인터와 같은 취급)

<br>





## 배열 참조

위에서 불가능한 경우에서 살짝만 신경써주면 가능함.

```c++
void func(int (&arr)[100])  
{
}
```

아마, 연산자 우선순위로 인한 문제같은데 (&arr)을 묶어줌으로서 해결해줌.

**포인터와의 차이점**은 **배열 참조의 경우 원소의 갯수도 타입으로 인정한다는 것임.**

아래 코드 참고.

```c++
void func(int (&arr)[100])  
{
}
int main()
{
    int arr[6]={1,2,3,4,5,6};
    func(arr); //ERROR!!!!!!!!!!!!!!!!!!!
    
    int arr2[100];
    func(arr2); //OK
}
```

배열 원소 갯수도 타입으로 포함시켜서 처리하는 것을 알 수 있음.

이런 부분에서, 참조와 포인터의 차이가 나는 것 같음.

<br>





## 배열 참조(+템플릿 사용)

흠..여기서 더 유동적으로, 자유롭게 사용하고 싶은 생각이 들게 됨.

C++은 그래서 우리에게 템플릿을 주었음!

```cpp
template<typename T,size_t size>
void func(T (&arr)[size])  
{
}
```

이런식으로 해준다면, **인자로 받을 배열의 타입과, 사이즈까지 알아서 처리가 됨!!!**

 

**ex)**

```cpp
template<typename T,size_t size>
void func(T (&arr)[size])  
{
    cout<<arr[3];
}
int main()
{
    int arr[6]={1,2,3,4,5,6};
    func(arr); //4출력됨
}
```

위와 같은 사용이 가능해짐.

<br>





## std::array를 파라미터로 받는법

```c++
void func(std::array<int,2>& t)
{
    cout << t[0];
}


//템플릿 사용 버전
template<typename T, size_t size>
void func(std::array<T,size>& t)
{
    cout << t[0];
}

```

참조형을 사용할수 있다면 사용하자!