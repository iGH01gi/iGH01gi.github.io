---
title: "[DB] Size Estimation"
categories: Db
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2024-06-04
last_modified_at: 2024-06-04
---

# ⚪<span style="color: #D6ABFA;">Statistical Information for Cost Estimation</span>

- **n<sub>r</sub>** : 릴레이션 r의 튜플의 수
- **b<sub>r</sub>** : 릴레이션 r의 블록의 개수
- **I<sub>r</sub>** : 릴레이션 r의 튜플의 사이즈
- **f<sub>r</sub>** : 릴레이션 r의 blocking factor (블록 1개에 r의 튜플이 몇개 들어가는지)
- **V(A,r)** : 속성A에 대하여 나타나는 distinct한 value의 수 (예를들어서 학년 속성에 1,2,3,4학년이 있다면 4가 나옴)
- 만약 r의 튜플들이 파일로 저장된다면 **b<sub>r</sub> = ⌈n<sub>r</sub>/f<sub>r</sub>⌉**

<br>

<br>

<br>

# ⚪<span style="color: #D6ABFA;">Selection Size Estimation</span>

- **σ<sub>A=v</sub>(r)**
  - n<sub>r</sub> / V(A,r) : 이 selection을 만족하는 레코드 수는 이 식으로 추정함 (균등분포라고 가정하고 있음)
  - 만약 key 속성에 대한 selection이었다면 size estimate는 1임
- **σ<sub>A<=v</sub>(r)** (σ<sub>A>=v</sub>(r)인 경우는 생략)
  - c를 조건을 만족하는 튜플의 추정개수 라고 정의하자
  - min(A,r)과 max(A,r)의 값이 db 카탈로그에 정보가 있을때,
    - c = 0 if v < min(A,r)
    - c = n<sub>r</sub> * { (v-min(A,r)) / (max(A,r) - min(A,r)) }   ==>비율로 추정하는 방식 (균등분포라고 가정하고 있음)
  - 만약 통계치 정보가 없을때는 c = n<sub>r</sub>/2 로 러프하게 추정함

![image-20240610181439243](../../assets/images/2024-06-04-SizeEstimation/image-20240610181439243.png){: width="50%"}

만약 histograms이 있다면  더 정교한 추정치를 얻을 수 있음

## 🔹selectivity

selectivity(선택도)는 조건 θ<sub>i</sub>가 주어지면 테이블의 각 레코드가 그 조건을 충족할 확률을 구하는 것

만약 s<sub>i</sub>가 릴레이션r 에서 조건을 충족하는 튜플의 개수라고 하면, **θ<sub>i</sub>의 selectivity는 s<sub>i</sub>/n<sub>r</sub>**

![image-20240610184030494](../../assets/images/2024-06-04-SizeEstimation/image-20240610184030494.png){: width="70%"} 

<br>

<br>

<br>

# ⚪<span style="color: #D6ABFA;">Join Size Estimation</span>

![image-20240610225213683](../../assets/images/2024-06-04-SizeEstimation/image-20240610225213683.png){: width="80%"}

r,s의 자연조인일때, 한쪽이 foreign key이고 한쪽이 referencing 되는 입장일때

foreign key쪽의 튜플개수가 결과 튜플의 수임

<br>

![image-20240610225649249](../../assets/images/2024-06-04-SizeEstimation/image-20240610225649249.png){: width="80%"}

조인하는 컬럼이 두 릴레이션에서 모두 키가 아닐때

둘중에 낮은 값을 선택해서 추정함

<br>

![image-20240610230100459](../../assets/images/2024-06-04-SizeEstimation/image-20240610230100459.png){: width="80%"}

조인했을때 A컬럼이 R에서 pk일때, 조인결과 튜플의 개수는 S의 튜플개수보다 많을 수 없음 

(모두 매칭이 되어봤자 최대 S의 튜플개수이기 때문에)

<br>

![image-20240610230344439](../../assets/images/2024-06-04-SizeEstimation/image-20240610230344439.png){: width="80%"}

카티션곱을 했을때의 튜플의 수와 결과 튜플 한개가 차지하는 바이트

<br>

![image-20240610230506037](../../assets/images/2024-06-04-SizeEstimation/image-20240610230506037.png){: width="80%"}

겹치는게 컬럼이 없을때 자연조인하라는 것은 카티션곱과 동일함
