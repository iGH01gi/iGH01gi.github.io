---
title: "[Algorithm] 버블 정렬(Bubble Sort)"

categories: Algorithm

toc: true
toc_sticky: true

layout: single

show_Date: true
date: 2024-07-01
last_modified_at: 2024-07-01
---

# ⚪<span style="color: #D6ABFA;">원리와 예시 코드</span>

![Szvcoad1t6eqmx0PkV3YxaW11wp1isNJng3y5CiXsScmTbxKz5jnmnF00GgxjalXZXvpuXf2RI4CKCQO2ZUIqw.mp4 [video-to-gif output image]](../../assets/images/2024-07-18-f/ezgif-6-88ab0612f7.gif)

1번째와 2번째 원소를 비교하여 정렬하고, 2번째와 3번째, ..., n-1번째와 n번째를 정렬한 뒤   
다시 처음으로 돌아가 이번에는 n-2번째와 n-1번째까지,   
...해서 최대 n(n-1)/2번 정렬한다.



큰 수부터 하나씩 차례대로 자리가 확정되는 방식



**거의 모든 상황에서 최악의 성능**을 보여준다.   
단, 이미 정렬된 자료에서는 1번만 돌면 되기 때문에 최선의 성능을 보여준다. 



```cpp
#include <iostream>
#include <vector>

void BubbleSort(std::vector<int>& arr)
{
    int n = arr.size();
    bool swapped;

    for (int i = 0; i < n-1; i++)
    {
        swapped = false;
        for (int j = 0; j < n-i-1; j++)
        {
            if (arr[j] > arr[j+1])
            {
                std::swap(arr[j], arr[j+1]);
                swapped = true;
            }
        }

        // 만약 내부 반복문에서 두 요소가 교환되지 않았다면, 그 배열은 정렬된 상태
        if (!swapped)
            break;
    }
}

int main()
{
    std::vector<int> arr = {64, 34, 25, 12, 22, 11, 90};
    BubbleSort(arr);
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

# ⚪<span style="color: #D6ABFA;">파생형 칵테일 정렬</span>

![CocktailSort.mp4 [video-to-gif output image]](../../assets/images/2024-07-01-BubbleSort/ezgif-2-f501cd3101.gif)

**칵테일 정렬(cocktail sort)** 또는 **셰이커 정렬(shaker sort)**라고도 하는 버블 정렬의 파생형.

홀수 번째 돌 때는 앞부터, 짝수 번째는 뒤부터 훑는 정렬. 

당연하겠지만 이 쪽은 마지막과 처음이 번갈아가며 정렬된다.   
제일 처음에 하나, 제일 뒤에 하나, 다시 제일 앞에 하나, 또 제일 뒤에 하나를 정렬하면서 마치 정렬하는 과정이 앞뒤로 마구 흔드는게 칵테일을 마구 흔들어 섞는것과 비슷해보인다 하여 칵테일(혹은 이름을 합쳐서 칵테일 셰이커) 정렬이라는 이름이 붙었다.

