---
layout: post
title: 깃페이지 포스트가 반영이 안될때
date: 2022-02-21 00:00:00+0900
category: Git
published: true
---
로컬서버에서 깃페이지를 확인했을때는 분명히 포스트가 잘 올라가 있는데, 깃허브에 push한 후  
내 깃허브 페이지에 접속하면 포스트가 반영이 안되는 문제가 있었다.  
찾다보니 2가지를 내가 놓치고 있었다.  

<br>
둘다 포스트의 머리말(YAML형식으로 작성한 부분)에서의 문제였다.  

# 1. published항목의 설정값이 이상하게 설정돼있을때.
처음에는 
>
ㅡㅡㅡ  
layout: post  
title: 깃페이지 포스트가 반영이 안될때  
date: 2022-02-11  
category: Git   
ㅡㅡㅡ

이런식으로 머릿말을 작성했는데 published: true를 써주지 않았을때  
어떤 이유인지는 모르겠지만 로컬서버를 열때 bundle exec jekyll serve **--unpblished** 처럼 unpublished옵션이 내가 치지 않았는데도 추가된게 아닌가 하고 의심이 된다.  
(로컬에서는 보이고 서버에서는 비공개인 옵션)

#### 결론1 : 머릿말에 published: true를 추가하자.  
>
ㅡㅡㅡ  
layout: post  
title: 깃페이지 포스트가 반영이 안될때  
date: 2022-02-21  
category: Git   
published: true  
ㅡㅡㅡ 

<br>
<br>  


# 2. timezone 미설정으로 인한 문제
포스트의 머릿말을 쓸 때 나는 date를 
>date:2022-02-21

같은 식으로 썼다.  
그러나 Jekyll은 이 date 값이 미래 시간이면 새로운 포스트로 인식하지 않는 것으로 생각이 된다.  
미래 시간을 판별할 때 Jekyll은 내부적으로 UTC+0000을 기준으로 삼고 있고  
시간대 정보가 없는 date 값은 암묵적으로 UTC+0000 시간대로 판단하는 것으로 추정된다.  
**즉, 나는 한국에서 시간대 정보없이 글을 썼기 때문에 미래 시간으로 인식이 되어, 포스트가 반영이 안됐던 것이다.**  
이를 해결하기 위해 **_config.yml**에서 timezone: Asia/Seoul 을 추가해 준 후  
한국은 표준시간대보다 9시간이 빠른 UTC+0900을 사용하기 때문에 date를 쓸때 00:00:00+0900 를 추가해줘야한다.  

#### 결론2 : _config.yml에서 timezone: Asia/Seoul추가하기 + 머릿말 date에 00:00:00+0900을 추가하자.
>
ㅡㅡㅡ  
layout: post  
title: 깃페이지 포스트가 반영이 안될때  
date: 2022-02-21 00:00:00+0900  
category: Git  
published: true  
ㅡㅡㅡ
+
_config.yml에서 timezone: Asia/Seoul추가하기.