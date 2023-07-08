---
title: "[C++]  순열 구하기 (std::next_permutation, std::prev_permutation)"
categories: Cpp
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2023-07-08
last_modified_at: 2023-07-08
---

## 헤더파일

```c++
#include<algorithm>
```

<br>



## 사용법

- 벡터의 경우

  ```c++
  next_permutation(v.begin(), v.end())
  prev_permutation(v.begin(), v.end())
  ```

<br>

- 배열의 경우

  ```c++
  int arr[n];
  next_permutation(arr,arr+n);
  prev_permutation(arr,arr+n);
  ```

<br>

- do-while문을 활용한 응용법(알고리즘 문제에서 자주 사용)

  ```c++
  #include<algorithm>
  
  int main()
  {
      vector <char> v1 = { 'A','B','C' }; 
      vector <char> v2 = { 'B','C','A' };
      vector <int> v3 =  { 1,2,3 }; 
      vector <char> v4 = { 'B','C','A' };
      
      
      
      do 
      {
          for (auto x : v1)cout << x; 
          cout << "\n"; 
      } while (next_permutation(v1.begin(), v1.end()));//계속해서 정렬 
      /* 출력값
      	ABC
  	ACB
  	BAC
  	BCA
  	CAB
  	CBA
      */
      
      
      
      
      do 
      {
          for (auto x : v2)cout << x;
          cout << "\n";
      } while (next_permutation(v2.begin(), v2.end()));//계속해서 정렬
      /* 출력값
      	BCA
  	CAB
  	CBA
      */
      
      
      
      
       do 
       {
          for (auto x : v3)cout << x;
          cout << "\n";
       } while (next_permutation(v3.begin(), v3.end()));//계속해서 정렬
  	/* 출력값
      	123
      	132
      	213
      	231
      	312
      	321
      */
      
      
      
      
      do 
      {
          for (auto x : v4)cout << x;
          cout << "\n";
      } while (prev_permutation(v4.begin(), v4.end()));//계속해서 정렬
  	/* 출력값
      	BCA
  	BAC
      	ACB
     	ABC
      */
  }
  ```

  <br>

  

## 주의할 점

주어진 배열 또는 벡터등의 **처음 값을 기준**으로,

std::next_permutation은 사전순으로 정렬

std::prev_permutation은 역사전순으로 정렬 

합니다. 

 

즉 **초기값을 A,B,C**를 주었다면 **std::next_permutation을 썼다는 가정** 하에

*ABC*  
*ACB*  
*BAC*  
*BCA*  
*CAB*  
*CBA*  

이렇게 생각한 순서대로 해당 함수를 쓸때마다 정렬값이 바뀌지만

 

**초기값 C,A,B**를 주었다면 

*CAB*  
*CBA*  

이렇게 나옵니다. 

 

std::prev_permutation은 똑같은 상황이지만 역순으로 정렬인것만 알면 되겠습니다.

(B,C,A를 prev_permutation하면 BCA, BAC, ACB, ABC 순으로 결과를 뱉습니다.)
