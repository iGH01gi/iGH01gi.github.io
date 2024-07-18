---
title: "[Algorithm] 삽입 정렬(Insertion Sort)"

categories: Algorithm

toc: true
toc_sticky: true

layout: single

show_Date: true
date: 2024-07-03
last_modified_at: 2024-07-03
---

# ⚪<span style="color: #D6ABFA;">원리와 예시 코드</span>

![InsertionSort.mp4 [speed output image]](../../assets/images/2024-07-03-InsertionSort/ezgif-4-03594bcb56.gif)

k번째 원소를 1부터 k-1까지와 비교해 적절한 위치에 끼워넣고 그 뒤의 자료를 한 칸씩 뒤로 밀어내는 방식

**평균적으론 O(n<sup>2</sup>)중 빠른 편**이나 **자료구조에 따라선 뒤로 밀어내는데 걸리는 시간이 크면 비효율적**이고,  
**작은 게 뒤쪽에 몰려있으면(내림차순의 경우 큰 게 뒤쪽에 몰려있으면) 비효율적**이다.

**배열이 작을 경우에 역시 상당히 효율적**이다.   
일반적으로 빠르다고 알려진 알고리즘들도 배열이 작을 경우에는 대부분 삽입 정렬에 밀린다.   
따라서 고성능 알고리즘들 중에서는 배열의 사이즈가 클때는 O(nlogn) 알고리즘을 쓰다가 정렬해야 할 부분이 작을때 는 삽입 정렬로 전환하는 것들도 있다.

```cpp
#include <iostream>
#include <vector>

void InsertionSort(std::vector<int>& arr)
{
    int n = arr.size();
    for (int i = 1; i < n; i++)
    {
        int key = arr[i];
        int j = i - 1;

        // arr[0..i-1]의 요소 중 key보다 큰 요소들을
        // 그들의 현재 위치보다 한 위치 뒤로 이동시킵니다.
        while (j >= 0 && arr[j] > key)
        {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

int main()
{
    std::vector<int> arr = {64, 34, 25, 12, 22, 11, 90};
    InsertionSort(arr);
    std::cout << "Sorted array: \n";
    for(int i = 0; i < arr.size(); i++)
    {
        std::cout << arr[i] << " ";
    }
    return 0;
}
```

> 정렬을 했을 때 중복된 값들의 순서가 유지되는 **안정(Stable) 정렬**에 속한다

<br>

<br>

<br>

# ⚪<span style="color: #D6ABFA;">시간 복잡도</span>

**O(n<sup>2</sup>)**

<br>

<br>

<br>

# ⚪<span style="color: #D6ABFA;">파생형 이진 삽입 정렬</span>

**이진 삽입 정렬(Binary Insertion Sort)**

[이진 탐색](https://igh01gi.github.io/algorithm/BinarySearchUpperLowerBound/){:target="_blank"}을 활용해 새로운 원소가 위치할 곳을 미리 찾아서 정렬하는 방식

원소크기를 비교하는 조건 부분을 log⁡𝑛log*n* 수준으로 낮춰 조금은 더 빠르게 수행할 수 있다
