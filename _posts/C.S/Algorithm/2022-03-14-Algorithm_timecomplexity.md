---
layout: post
title: 시간 복잡도(학교)
date: 2022-03-14 00:00:00+0900
category: Algorithm
published: true
---
- 실행 시간은 input size에 따라 변한다.  
- 보통 최악의 경우를 생각해서 알고리즘을 고른다.  

# 시간 복잡도 
n만큼의 인풋이 들어왔을때의 number of operations을 표현하는 방식.  
(실제 실행시간이 아님)  
![시간복잡도](\images\Algorithm\timecomplexity.png)  
![실행시간](\images\Algorithm\executiontime.png)
![그래프](\images\Algorithm\graph.png)

# 공간 복잡도  
알고리즘이 요구하는 메모리의 양을 표현.  
ex)  
Scalar:O(1)  
Vector:O(n)  
Matrix:O(n^2)

# 주로 다룰것은 시간 복잡도!(Time Complexity)
시간 복잡도는 알고리즘의 정확한 연산 횟수를 나타내기 위해서 사용하는 것이 아님.  
n이 커질때 연산횟수가 얼마나 늘어나느냐 하는 그 추이를 표현하고, 그것을 통해 어느 알고리즘이 더욱 효율적인지를 판단하기 위해 사용하는 것이다.  
그렇기 때문에 상수나 최고차항이 아닌 n값등은 무시를 하게 된다.(n이 매우 커질때 영향을 주는 것에 집중해야 하기 때문에 상대적으로 미미한 영향을 주는 것들은 무시됨.) 

<br>  
시간복잡도 표기법으로는 다음과 같은 것이 있다.  
![표기법](\images\Algorithm\notation.png)  

<br>  

--- 

### [ Big-O 표기법 ]  
일반적으로 시간복잡도를 표기한다 하면 이 **Big-O**표기법을 사용함.  
**최악의 경우**를 생각한 표기법임. 그렇기때문에 가장 흔히 사용됨.  
![빅오](\images\Algorithm\bigO.png)  
f(x) is big-oh of g(x)라고 읽는다.   
절댓값 기호는 결과값의 크기를 뜻하기 위해 쓴것이라고 한다.  
상수C와 k는 witnesses라고도 불린다.  
만약 한쌍의 witnesses가 존재한다면 무한히 많은 쌍의 witnesses가 존재하게된다.  
![](\images\Algorithm\infi.png)    

Big-O표기법 공부중에 알아낸것:  f(n)=n^2+n+1 이라했을때  
f(n)=O(n^2)도 되고 O(n^3)도 되고 등등...이 가능해진다. 그러나 일반적으로 그 중 가장 점근적으로 가까운 표시값을 사용한다. 따라서 O(n^2)로 표현하게됨.  

---

### [ Big-Omega 표기법 ] 
Big-O와는 반대로 **최선의 경우**를 생각한 표기법.  
그러므로 주로 사용하지는 않는다.  
![빅오메가](\images\Algorithm\bigOmega.png)  
f(x) is big-Omega of g(x) 라고 읽는다.   
마찬가지로 f(n)=n^2+n+1이라고 했을때  
f(n)=Ω(n^2)도 가능하고 Ω(n)도 가능하고 Ω(logn)도가능하고 Ω(1)...도 가능하다  
하지만 Big-O와 마찬가지로 일반적으로 그 중 가장 점근적으로 가까운 표시값을 사용한다. 따라서 이 경우엔 Ω(n^2)을 사용하게 된다.  

---

### [ Big-Theta 표기법 ]
f(x) is O(g(x)) 이면서 f(x) is Ω(g(x))를 동시에 만족하는 g(x)가 존재할 경우  
f(x)=θ(g(x))라고 표현할 수 있다.  f(x) is big-theta of g(x)라고 읽는다.  


---

# 성질
![프로퍼티](\images\Algorithm\properties.png)


<br>
- 빅오 표기법의 특징  

계수 법칙: 상수 k>0인 경우 f(n)이 O(g(n))이면 kf(n)은 O(g(n))이다.  
합의 법칙: f(n)이 O(h(n))이고 g(n)이 O(p(n))이라면 f(n) + g(n)은 O(h(n)+p(n))이다.  
곱의 법칙: f(n)이 O(h(n))이고 g(n)이 O(p(n))이면 f(n)g(n)은 O(h(n)p(n))이다.  
전이 법칙: f(n)이 O(g(n))이고 g(n)이 O(h(n))이면 f(n)은 O(h(n))이다.  
다항법칙: f(n)이 3(k)차 다항식이면 f(n)은 O(n³(k))이다.  
상수항 무시: 빅오 표기법은 데이터 입력값(n)이 충분히 크다고 가정하고 있고, 알고리즘의 효율성 또한 데이터 입력값(n)의 크기에 따라 영향 받기 때문에 상수항 같은 사소한 부분은 무시한다.  
*영향력 없는 항 무시: 빅오 표기법은 데이터 입력값(n)의 크기에 따라 영향을 받기 때문에 가장 영향력이 큰 항에 이외에 영향력이 없는 항들은 무시한다.  
그래프에 나와 있는 시간 복잡도의 성능을 비교하면 다음과 같다.  

[빅오메가 빅세타 차이](https://www.freecodecamp.org/news/big-theta-and-asymptotic-notation-explained/)
https://cs.stackexchange.com/questions/10763/why-is-theta-notation-suitable-to-insertion-sort-to-describe-its-worst-case-r