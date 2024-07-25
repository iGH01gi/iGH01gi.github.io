---
title: "[자료구조] 분리 집합(Disjoint Set), 유니온 파인드(Union Find)"

categories: DataStructure

toc: true
toc_sticky: true

layout: single

show_Date: true
date: 2024-07-15
last_modified_at: 2024-07-15
---



# ⚪<span style="color: #D6ABFA;">정의</span>

분리 집합(Disjoint Set), 또는 유니온-파인드(Union-Find) 자료구조는 주로 그래프 알고리즘에서 사용되는 자료구조로,   
**서로 중복되지 않는 부분 집합들로 나누어진 원소들을 효율적으로 관리**하는 데 사용된다.   
이 자료구조는 두 가지 주요 연산을 제공한다:

1. **Find**: 특정 원소가 속한 집합을 찾는다.
2. **Union**: 두 집합을 하나의 집합으로 합친다.



이 자료구조는 **경로 압축(Path Compression)**과 **랭크(Rank)를 이용한 유니온**을 통해 최적화될 수 있다.   
경로 압축은 `Find` 연산을 수행할 때 각 원소가 직접 루트에 연결되도록 하여 이후의 연산을 더 빠르게 한다.   
랭크를 이용한 유니온은 항상 랭크가 낮은 집합을 랭크가 높은 집합에 합치도록 하여 트리의 높이를 줄여서 Find 시간복잡도를 줄인다.

> Rank는 트리의 높이를 추정하는 값으로, 트리의 실제 높이와는 정확히 일치하지 않을 수 있다. 



집합을 구현하는 데는 비트벡터, 배열, 연결리스트, 트리 등을 이용할 수 있으나 그 중 가장 효율적인 트리구조를 이용하여 구현한다

<br>

<br>

<br>

# ⚪<span style="color: #D6ABFA;">코드</span>

```c++
#include <iostream>
#include <vector>

// Disjoint Set 클래스 정의
class DisjointSet 
{
    public:
        DisjointSet(int n);      // 생성자: n개의 원소를 가진 집합을 초기화
        int find(int x);         // find 함수: x가 속한 집합의 대표(루트)를 찾는 함수
        void unite(int x, int y); // unite 함수: x와 y가 속한 두 집합을 합치는 함수

    private:
        std::vector<int> parent; // 각 원소의 부모를 저장하는 벡터
        std::vector<int> rank;   // 각 집합의 높이를 저장하는 벡터 (트리의 추정 높이)
};

// 생성자: 초기화
DisjointSet::DisjointSet(int n)
{
    parent.resize(n); // parent 벡터의 크기를 n으로 설정
    rank.resize(n, 0); // rank 벡터의 크기를 n으로 설정하고, 초기값을 0으로 설정
    for (int i = 0; i < n; ++i)
    {
        parent[i] = i; // 초기에는 모든 원소가 자기 자신을 부모로 가리키도록 설정
    }
}

// Find 함수: 경로 압축 사용
int DisjointSet::find(int x)
{
    if (parent[x] != x)
    {
        parent[x] = find(parent[x]); // 재귀적으로 부모를 찾아가면서 경로 압축을 수행
    }
    return parent[x]; // 루트 노드를 반환
}

// Union 함수: 랭크를 이용한 합집합 연산
void DisjointSet::unite(int x, int y)
{
    int rootX = find(x); // x가 속한 집합의 루트 찾기
    int rootY = find(y); // y가 속한 집합의 루트 찾기

    if (rootX != rootY) // 두 집합이 서로 다른 경우에만 합침
    {
        //***항상 높이가 낮은 트리를 높이가 높은 트리에 붙인다.***//
        
        if (rank[rootX] > rank[rootY]) // rootX의 랭크가 더 큰 경우
        {
            parent[rootY] = rootX; // rootY를 rootX의 자식으로 설정
        }
        else if (rank[rootX] < rank[rootY]) // rootY의 랭크가 더 큰 경우
        {
            parent[rootX] = rootY; // rootX를 rootY의 자식으로 설정
        }
        else // 두 집합의 랭크가 같은 경우
        {
            parent[rootY] = rootX; // rootY를 rootX의 자식으로 설정하고
            rank[rootX]++; // rootX의 랭크를 증가시킴
        }
    }
}

// 예제 사용 코드
int main()
{
    DisjointSet ds(10); // 10개의 원소를 가진 분리 집합 생성

    ds.unite(1, 2); // 1과 2를 합침
    ds.unite(3, 4); // 3과 4를 합침
    ds.unite(2, 4); // 2와 4가 같은 집합이 되므로, 1, 2, 3, 4가 같은 집합으로 합쳐짐

    std::cout << "Find 1: " << ds.find(1) << std::endl; // 1의 루트 출력
    std::cout << "Find 2: " << ds.find(2) << std::endl; // 2의 루트 출력
    std::cout << "Find 3: " << ds.find(3) << std::endl; // 3의 루트 출력
    std::cout << "Find 4: " << ds.find(4) << std::endl; // 4의 루트 출력

    return 0;
}

```

> **출력결과:**
>
> Find 1: 1  
> Find 2: 1  
> Find 3: 1  
> Find 4: 1
