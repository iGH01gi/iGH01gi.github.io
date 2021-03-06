---
layout: post
title: CSS 여백을 조절하는 속성
date: 2022-03-03 00:00:00+0900
category: Web
published: true
---
# 요소 주변의 여백을 설정하는 margin 속성 
마진을 이용하면 요소와 요소 사이의 간격을 조절할 수 있다.  
마진도 박스 모델의 4개 방향에 똑같이 지정할 수도 있고, margin 다음에 하이픈(-)을 넣고 위치를 나타내는 예약어 top,right,bottom,left를 사용해서 특정 방향에만 지정할 수도 있다.  
```css
margin: <크기> | <백분율> | auto
```
- ```<크기>``` 에는 너빗값이나 높잇값을 px나 em같은 단위와 함께 수치로 지정함.  
- ```<백분율>```에는 박스 모델을 포함한 부모 요소를 기준으로 너빗값이나 높잇값을 퍼센트(%)로 지정함.  
- auto는 display 속성에서 지정한 값에 맞게 적절한 값을 자동으로 지정함.  


값이 1개라면 마진값을 4개 방향 모두 독같이 지정하지만, 값이 여러 개라면 top->right->bottom->left순(시계 방향)으로 적용됨.   

# margin 속성을 사용하여 웹 문서를 가운데 정렬하기  
웹 문서에서 텍스트 요소를 배치할 때는 text-align 속성을 사용해서 정렬했었음.  
하지만 웹 문서 전체를 중앙에 배치할때는 이 margin 속성을 사용하면 할 수 있음.  
margin 속성을 사용해 웹 문서의 내용을 화면 중앙에 배치하려면 우선적으로 배치할 요소의 너빗값이 정해져 있어야 한다.  
그리고 margin-left와 margin-right의 속성값을 auto로 지정함. 이렇게 지정하면 CSS는 웹 브라우저 화면의 너비에서 요소 너빗값을 뺀 나머지 영역을 좌우 마진으로 자동 계산함.  

# 마진 중첩 이해하기 
요소를 세로로 배치할 경우에 각 요소의 마진과 마진이 서로 만나면 마진값이 큰 쪽으로 겹쳐지는 문제.  
이런 현상을 마진 중첩(margin overlap)또는 마진 상쇄(margin collapse)라고 함.  
이렇게 된 이유는 여러 요소를 세로로 배치할 때 맨 위의 마진과 맨 아래 마진에 비해 중간에 있는 마진이 지나치게 커지는 것을 방지하기 위한 것.  
따라서 **위 아래 마진**이 서로 만날 때 큰 마진값으로 합쳐지는 것이고, **오른쪽 왼쪽 마진**이 만날 경우에는 중첩되지 않는다.  

# 콘텐츠와 테두리 사이의 여백을 설정하는 padding 속성  
패딩이란 콘텐츠 영역과 테두리 사이의 여백을 말함.  
다시 말해 테두리 안쪽의 여백이라고 생각하면 됨.  
padding속성으로 4개 방향의 마진을 한꺼번에 지정할 수도 있고, padding 다음에 하이픈(-)을 넣고 위치를 나타내는 예약어 top,right,bottom,left를 사용해서 특정 방향에만 지정할 수도 있다.  