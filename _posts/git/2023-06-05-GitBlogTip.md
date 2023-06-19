---
title: 마크다운 문법

categories: Git

toc: true
toc_sticky: true

//author_profile: false 왼쪽에 따라다니는거 키고끄기

layout: single

show_Date: true
date: 2023-06-05
last_modified_at: 2023-06-19
---

<br>

## 줄바꿈

1️⃣ 스페이스바 두번+ Enter (Typora를 사용중일땐 shfit+Enter)

```
줄바꿈(스페이스 스페이스+엔터)
테스트
```

줄바꿈  
테스트 

2️⃣  \<br> 줄바꿈 HTML태그 사용

```html	
줄바꿈<br> 테스트
```

줄바꿈<br>테스트 

<br>



## 문단 나누기

- 문장 사이에 한 줄 공백 (Typora를 사용중일땐 Enter 한번만)

```
한줄 공백

테스트
```

한줄 공백

테스트

<br>



## 리스트

### 🔹unordered list

- '-' + '공백' (구조가 중첩될때마다 '-'앞 스페이스바 2번씩 추가해줘야함.)  
  (Typora를 사용줄일때는 스페이스바를 신경쓰기보단 자동정렬 기능이 있기때문에 상관X)

```
- 중첩(스페이스바 0번)
  - 중첩(스페이스바 2번)
    - 중첩(스페이스바 4번)
```

- 중첩(스페이스바 0번)
  - 중첩(스페이스바 2번)
    - 중첩(스페이스바 4번)  

<br>

### 🔹ordered list

- `1.` `2.` ... `. 뒤에 한칸 스페이스바 하기`

```
1. 순서
2. 있는
  1. 있는1
  2. 있는2
```

1. 순서

2. 있는

   1. 있는1

   2. 있는2

<br>

### 🔹check list

- `- [ ]` 와 `- [X]`

```
- [ ] 체크 안됨
- [X] 체크 됨
```

- [ ] 체크 안됨
- [X] 체크 됨





## 마크다운 문법 그대로 표시

- `\`붙여주기 

```
\<u>예시</u>
```

\<u>예시</u>  

만약에 `\`를 붙이지 않았다면  
<u>예시</u>  
위처럼 밑줄이 쳐지게 됨.

<br>



## Header

- `#`를 통해서 제목 크기 조절. (TOC에서도 # 개수에 따라서 정렬됨)

```
# h1
## h2
### h3
#### h4
##### h5
###### h6
```

<br>



## 텍스트 효과

### 🔹굵은  텍스트

- `**`

```
**굵은 텍스트**
```

**굵은 텍스트**

<br>

### 🔹기울여진  텍스트  

- `*`

```
*기울여진 텍스트*
```

*기울여진 텍스트*

<br>

### 🔹굵고 기울여진  텍스트   

- `***`

```
***굵고 기울여진 텍스트***
```

***굵고 기울여진 텍스트***

<br>

### 🔹취소선  

- `~~`

```
~~취소선 텍스트~~
```

~~취소선 텍스트~~

<br>

### 🔹밑줄

- `<u>`

```
<u>밑줄 텍스트</u>
```

<u>밑줄 텍스트</u>

<br>

### 🔹텍스트  색상

```
<span style="color:yellow">노란 텍스트</span>
```

<span style="color:yellow">노란 텍스트</span>

<br>



## 코드 블록

- \``` + `언어이름`

````
```c++ 
#include <iostream>
using namespace std;

int main()
{
	cout<<"hello world";
}
```
````

```c++ 
#include <iostream>
using namespace std;

int main()
{
	cout<<"hello world";
}
```

<br>



## 링크

### 🔹주소 그대로 링크

- `<링크 주소>`

```
<https://www.google.com>
```

<https://www.google.com>

<br>

### 🔹대체 텍스트 링크

- `[대체 텍스트](링크 주소)` 

```
[구글링크](https://www.google.com)
```

[구글링크](https://www.google.com)

<br>

### 🔹동일 문서 내에서 특정 문단(헤더)으로 이동 링크

- `[대체 텍스트](#문단의 주소)` 

```
<문단 주소란?>
1. 헤더 제목 문자열을 복사하고 (문단의 주소)에 복사한다.
2. 특수 문자를 제거한다.
3. 공백을 -로 변경한다.
4. 대문자는 소문자로 변경한다. 예시) “#Markdown! 장점” > “#markdown-장점”

[코드 블록으로 이동하는 링크](#코드-블록)
```

[코드 블록으로 이동하는 링크](#코드-블록)

<br>

### 🔹그림 링크 삽입(온라인,로컬 둘다 적용)

- `![사진 설명 텍스트](이미지 주소)`

```
![image](./../../assets/images/2023-06-05-GitBlogTip/ighRabbit.png)
```

![ighRabbit](./../../assets/images/2023-06-05-GitBlogTip/ighRabbit.png)

- html의 img태그 사용 (이미지 크기 조절 가능)

```
<img src="이미지 URL">
<img src="이미지 URL" width="가로 사이즈" height="세로 사이즈">

<img src="./../../assets/images/2023-06-05-GitBlogTip/ighRabbit.png" width="100">
```

<img src="./../../assets/images/2023-06-05-GitBlogTip/ighRabbit.png" width="100">

<br>

### 🔹그림 자체에 링크 걸기

- `[대체텍스트](이미지주소)](이동하려는 링크 주소)`

```
[![image](https://cdn-icons-png.flaticon.com/512/5968/5968866.png)](https://github.com/iGH01gi)
```

[![image](https://cdn-icons-png.flaticon.com/512/5968/5968866.png)](https://github.com/iGH01gi)

<br>



## 인용문

- `>`로 표현. `>>` 이렇게 두개 쓰면 중첩된 인용문. 중첩할땐 앞에 스페이스바 2번

```
>인용문
  >>중첩된인용문
```

>인용문
>>중첩된인용문

<br>



## 구분선

- `---` 또는 `***`

```
---
***
```

---
***

<br>



## 테이블

- `|` 와 `-(3개 이상)`의 조합으로 테이블 생성

```
<정렬>
왼쪽 정렬 |:—|
오른쪽 정렬 |—:|
가운데 정렬 |:—:|

|제목|레이팅|감상평|
|:---:|---:|---|
|탑건|⭐⭐⭐⭐⭐|돌비최고|
|슬램덩크|⭐⭐⭐⭐⭐|뚫어!|
|배트맨|⭐⭐⭐⭐⭐|필요악|
```

|   제목   | 레이팅 | 감상평   |
| :------: | -----: | -------- |
|   탑건   |  ⭐⭐⭐⭐⭐ | 돌비최고 |
| 슬램덩크 |  ⭐⭐⭐⭐⭐ | 뚫어!    |
|  배트맨  |  ⭐⭐⭐⭐⭐ | 필요악   |

<br>



## 토글(접기,펼치기)

- HTML의 details 태그 사용

```
div markdown=”1” 은 jekyll에서 html사이에 markdown을 인식 하기 위한 코드임.

<details>
<summary>여기를 눌러주세요</summary>
<div markdown="1">       

🐣속 내용🐣

</div>
</details>
```

<details>
<summary>여기를 눌러주세요</summary>
<div markdown="1">       

🐣속 내용🐣

</div>
</details>

<br>



## 버튼

- html 태그 사용

```
링크부분에 #을 넣어주면 페이지 맨 위로 이동함

<a href="#" class="btn--success">맨위로</a>

[Default Button](#){: .btn .btn--primary }
```

<a href="#" class="btn--success">맨위로(성공)</a>

[Default Button](#){: .btn .btn--primary }
