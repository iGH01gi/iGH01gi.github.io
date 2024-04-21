---
title: "[DB] Query Cost"
categories: Db
toc: true
toc_sticky: true
//author_profile: false 왼쪽에 따라다니는거 키고끄기
layout: single
show_Date: true
date: 2024-03-14
last_modified_at: 2024-03-14
---

# ⚪<span style="color: #D6ABFA;">기호 정의</span>

- **t<sub>S</sub>** : (=seek time) 책에서는 고려하지만 여기서는 고려하지 않겠음. 0으로 생각    
- **b<sub>r</sub>** : 릴레이션 r의 레코드들을 포함하고있는 **총 블록의 개수**
- **t<sub>T</sub>** : (=transfer time) 여기서는 그냥 1로 생각
- **h<sub>i</sub>** : B+ tree index의 높이
- **n** : 매칭된 레코드의 수
- **b** : clustering index일때 매칭된 레코드를 포함하고있는 블록들의 수 ( = ⌈n/bf(블록킹팩터)⌉)

이번 포스팅에서는 여러 요소가 책에서 소개되지만, block I/O (transfer) 만 고려함

이번 포스팅에서 key라고 말하는건 PK라고 생각하면 됨

<br>

<br>

<br>

# ⚪<span style="color: #D6ABFA;">Selection Operation</span>

## 🔹File scan

- 책에서는 **Algorithm A1 (linear search)** 라고 부름. (file scan을 linear search라고도 부름)
- 파일의 모든 블록을 읽어서 selection(관계 대수) condition을 충족하는지 확인하는 알고리즘

### 🔸Cost

- **Algorithm A1 (linear search)**
  - selection이 key(=PK) 속성에 관한 것일때의 Cost : b<sub>r</sub>/2 
    - record를 찾으면 멈출수 있기 때문
  - 그렇지 않을때의 Cost : b<sub>r</sub> 

## 🔹Index Scan

- index를 사용해서 검색하는 알고리즘
- selection(관계대수) condition은 search-key of index여야만 함

### 🔸Cost

- **A2 (clustering index, equality on key)** : h<sub>i</sub> + 1
  - 책에는 Cost = (h<sub>i</sub> + 1) * (t<sub>T</sub> + t<sub>S</sub>)
- **A3 (clustering index, equality on nonkey)** : h<sub>i</sub> + b
  - 책에는 Cost = h<sub>i</sub>  \* (t<sub>T</sub> + t<sub>S</sub>) + t<sub>S </sub> + t<sub>T </sub>\* b
  - b = number of blocks containing matching records
- **A4 (secondary index, equality on key / nonkey)** 
  - search-key가 candidate key여서 single record만 얻는 경우 :  h<sub>i</sub> + 1
    - 책에는 Cost = (h<sub>i</sub> + 1) * (t<sub>T</sub> + t<sub>S</sub>)
  - search-key가 candidate key가 아니여서 multiple record를 얻는 경우 : h<sub>i</sub> + n
    - 책에서는 Cost = (h<sub>i</sub> + n) * (t<sub>T</sub> + t<sub>S</sub>)
    - each of **'n'** matching records may be on a different block. 즉 n은 매칭된 레코드의 수
    - 최악의 경우임. 각각의 레코드가 다 다른 블록에 있는 경우

<br>

σ<sub>A </sub>≤ V (r) or σ<sub>A</sub> ≥ <sub>V</sub>(r) 와 같은 Comparison은 linear file scan 또는 indices를 사용하여서 수행될 수 있음

아래 2개는 indices를 사용한 경우임

- **A5 (clustering index, comparison)** (Relation is sorted on A)
  - σ<sub>A</sub> ≥ <sub>V</sub>(r) 일때 : h<sub>i</sub> + b
    - 책에서는 Cost = h<sub>i</sub>  \* (t<sub>T</sub> + t<sub>S</sub>) + t<sub>S </sub> + t<sub>T </sub>\* b
    - v를 탐색키로 인덱스를 사용해서 v이상이 되는 첫 튜플을 찾고 그곳에서부터 sequentially하게 relation을 scan함
  - σ<sub>A</sub> ≤  <sub>V</sub>(r) 일때 : index를 사용하지 않고 첫 레코드부터 sequentially하게 v보다 커지는 값이 나오기 전까지 스캔. (관련 비용은 16장에서 다뤄서 지금은 스킵)
- **A6 (Non clustering index, comparison)**
  - σ<sub>A</sub> ≥ <sub>V</sub>(r) 일때 : h<sub>i</sub> + n
    - 책에서는 Cost = (h<sub>i</sub> + n) * (t<sub>T</sub> + t<sub>S</sub>)
    - v를 탐색키로 인덱스를 사용해서 v이상이 되는 첫 인덱스엔트리를 찾고, 거기서부터 인덱스의 리프노드를 sequentially하게 스캔해서 각 레코드 포인터를 사용해서 레코드를 탐색
  - σ<sub>A</sub> ≤  <sub>V</sub>(r) 일때 : 인덱스의 맨 왼쪽 리프노드부터 오른쪽으로 쭉 스캔하면서 레코드 포인터를 얻음. entry > v가 될때까지 (관련 비용은 16장에서 다뤄서 지금은 스킵)
  - 두 경우 모두 최악의 경우 레코드 1개당 I/O가 발생할 수 있기 때문에 Linear file scan이 더 비용이 작을수도 있음

