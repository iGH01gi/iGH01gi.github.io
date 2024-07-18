---
title: "[Algorithm] 선택 정렬(Selection Sort)"

categories: Algorithm

toc: true
toc_sticky: true

layout: single

show_Date: true
date: 2024-07-02
last_modified_at: 2024-07-02
---

# ⚪<span style="color: #D6ABFA;">원리와 예시 코드</span>

![SelectionSort](../../assets/images/2024-07-02-SelectionSort/SelectionSort.gif)

버블 정렬이 비교하고 바로 바꿔 넣는 걸 반복한다면   
이쪽은 일단 1번째부터 끝까지 훑어서 가장 작은 게 1번째, 2번째부터 끝까지 훑어서 가장 작은 게 2번째……해서 (n-1)번 반복



인간이 사용하는 정렬 방식을 가장 많이 닮았다



선택 정렬은 배열에서 가장 작은 (또는 가장 큰) 요소를 찾아서 맨 앞 (또는 맨 뒤)로 이동하는 방식으로 동작함.   
이로 인해, 선택 정렬은 **입력 데이터의 순서에 관계없이 항상 동일한 수의 비교와 교환을 수행**   
(보통 버블 정렬보다 두 배 정도 빠르다)



```cpp
#include <iostream>
#include <vector>

void SelectionSort(std::vector<int>& arr)
{
    int n = arr.size();
    for (int i = 0; i < n-1; i++)
    {
        int minIndex = i;
        for (int j = i+1; j < n; j++)
        {
            if (arr[j] < arr[minIndex])
                minIndex = j;
        }
        std::swap(arr[minIndex], arr[i]);
    }
}

int main()
{
    std::vector<int> arr = {64, 34, 25, 12, 22, 11, 90};
    SelectionSort(arr);
    std::cout << "Sorted array: \n";
    for(int i = 0; i < arr.size(); i++)
    {
        std::cout << arr[i] << " ";
    }
    return 0;
}
```



> 정렬을 했을 때 중복된 값들의 순서가 변하는 **불안정(Unstable) 정렬**에 속한다

<br>

<br>

<br>

# ⚪<span style="color: #D6ABFA;">시간 복잡도</span>

**O(n<sup>2</sup>)**

<br>

<br>

<br>

# ⚪<span style="color: #D6ABFA;">파생형 이중 선택 정렬</span>

**이중 선택 정렬(Double Selection Sort)**

끝까지 훑어서 최솟값과 최댓값을 동시에 찾아낸 뒤 최솟값은 1번째와 바꾸고 최댓값은 끝과 바꾼 다음 훑는 범위를 양쪽으로 한 칸씩 줄여서 반복하는 방식

이 방법을 쓰면 반복 횟수가 반으로 줄어든다.
