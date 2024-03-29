---
layout: post
title:  "시간 & 공간 복잡도 (Time & Space Complexity)"
subtitle: "PS에서의 시간복잡도? 공간복잡도? Big-Oh? 는 무엇을 의미하는가"
date:   2021-05-03 07:00:00 +1400
header-img: "img/post-bg-ds-algo.jpg"
header-mask: 0.6
catalog: true

lang: "ko"
english: true
japanese: true

published: true
hidden: false

permalink: /ko/algorithm/complexity/
tags:
  - algorithm
  - ps
---

## 시간 복잡도 (Time Complexity)
- 입력의 크기와 문제를 해결하는데 걸리는 시간의 상관관계
- 보통 코딩테스트(코테) 혹은 PS 에서 1억 번의 연산을 1초로 계산.
  + TMI: 2021년 5월 기준, 최고 성능의 슈퍼컴퓨터는 일본에 [후가쿠(Fugaku)](https://blog.global.fujitsu.com/fgb/2020-06-22/supercomputer-fugaku-named-world-fastest/)이며 최고 연산 속도는 537petaFLOPS(PF)인듯하다. 1PF가 1000조 만큼의 연산속도를 의미하므로 Fugaku는 1초에 약 53.7경 만큼의 연산을 수행할 수 있다는 의미입니다.

아래 `countEven` 함수가 있습니다. 이 함수는 1 부터 N사이 짝수의 갯수를 반환합니다.
각 연산들이 몇 번 수행되는지 확인해봅시다.

<br>

```cpp
int countEven(int N) {
    int cnt = 0;

    for(int i=1; i<=N; ++i) {
        if(i % 2 == 0) ++cnt;
    }

    return cnt;
}
```


**2번째 줄** `cnt = 0`에서 1번. **4번째 줄** 반복문 `i=1`에서 1번, 그리고 이후는 N번 반복되는데 `i <= N`와 `++i` 각각 1번. 
**5번째 줄** `i % 2 == 0`에서 2번 `++cnt`에서 1번. 그리고 마지막 **8번째 줄**에서 1번의 연산이 이루어집니다. 
이로 인해 `countEven`함수는 총 `1+1*N(2+2+1)+1 = 5N+3`번의 연산이 이루어진다는 걸 알 수 있습니다.

<br>

위에서 1초에 대략 1억번의 연산이 수행된다고 했었죠. N이 1000만이면, 대략 5000만번의 연산을 하는데 이는 1초안에 충분히 수행됩니다. 하지만 N이 5000만이면 대략 2억5천만번의 연산이 필요하기 때문에 1초 이상의 시간을 필요로 합니다.

<br>

그래서 `5N + 3`이 시간복잡도와 무슨 연관이 있느냐. 여기서 중요한 것은 `N`에 비례한다는 것입니다. `N`이 작으면 총 연산횟수도 적어지므로 함수가 빨리 종료되고, 반대로 `N`이 커지면 연산 횟수도 비례해서 늘어나니 함수의 실행시간이 늘어나겠죠 (즉, 프로그램이 느려진다). 이를 빅오표기법을 사용해서 '`O(N)`의 시간복잡도를 가진다'라고 합니다.

### 빅오표기법 (Big-Oh Notation)
주어진 식에서 값이 가장 큰 대표항만 남개서 나타내는 표기법입니다.

```
- O(N)   ==> N+3, 10N + logN, 5N + 10sqrtN, ...
- O(N^2) ==> 5N^2 + 10N + 7, 10N^2 + 1, ...
- O(1)   ==> 1, 5, 17, ...
```

여러 대표적인 시간복잡도를 그래프로 나타내보면 아래와 같습니다.

![Big-Oh Chart](/img/in-post/ds-algo/complexity/big-oh.png)

입력 크기로 주어질수 있는 N의 최대 크기를 자신이 작성한 알고리즘의 사간복잡도에 대입해보면, 해당 문제의 제한시간 (언어에 따라 다르지만 보통 1~5초 사이)에 해결이 가능한지 파악이 가능합니다.

## 공간 복잡도 (Space Complextiy)
- 입력의 크기와 문제를 해결하는데 필요한 공간의 상관관계
- 보통 코테에서 512MB의 메모리를 제한으로 두는데 이는 약 1.2억개의 int형 변수를 의미한다.

알고리즘 문제에서는 보통 시간복잡도를 많이 보기 때문에 공간복잡도는 크게 시간쓰지 않아도 됩니다. 하지만 가끔가다 메모리 제한이 있는 문제들이 있으니 유의하기 바랍니다.

## Reference
- [https://blog.encrypted.gg/922](https://blog.encrypted.gg/922)
- [Big Oh Chart](https://danielmiessler.com/study/big-o-notation/)