---
title:  "연습 문제2 - fibonacci"
excerpt: "연습 문제2 풀이"

categories:
  - Javascript_Practice
tags:
  - [Javascript,codestates,toy problem]

comment: true

author: Beomhyuck

toc: true
toc_sticky: true
 
date: 2022-09-20
last_modified_at: 2022-09-20
---

문제
===

아래와 같이 정의된 피보나치 수열 중 n번째 항의 수를 리턴해야 합니다.

0번째 피보나치 수는 0이고, 1번째 피보나치 수는 1입니다. 그 다음 2번째 피보나치 수부터는 바로 직전의 두 피보나치 수의 합으로 정의합니다.
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, ...

<br>

입력
===
인자 1 : n

number 타입의 n (n은 0 이상의 정수)


문제풀이
===

## 1. 재귀함수를 이용하여 피보나치 수열을 만든다.
---  

0과 1일때는 각 값을 그대로 출력하고 2번째 부터 피보나치 수열을 만들어 문제를 해결하였다.


Pseudo Code   
1. n이 0일때 0 리턴
2. n이 1일때 1 리턴
3. n이 2이상일때 n값이 될때까지 이전값 2개를 더한 수열을 만든다.

```javascript
function fibonacci(n) {
  // TODO: 여기에 코드를 작성합니다.
  if(n == 0) return 0
  if(n == 1) return 1
  return calc_fibonacci(0,1,2,n)
}

function calc_fibonacci(first,second,n,fix){
  if(n === fix) return first + second

  return calc_fibonacci(second,first+second,n+1,fix)

}
```

더 나은 방법
===
내가 풀이한 방식으로 하면 시간복잡도 O(n<sup>2</sup>)가 나온다.

빠르게 해결하는 방법이 있다.

시간복잡도가 오래 걸리는 이유는 이전에 계산했던 값도 다시 계산하기 때문이다.

```
// fibo(10)   
// = fibo(9) + fibo(8)
// = fibo(8) + fibo(7) + fibo(7) + fibo(6)
```

그렇다면 이전에 계산했던 값을 저장해두었다 다시 사용하면 시간복잡도가 줄어들 것이다.

Pseudo Code  
1. 0,1의 값을 배열에 저장해둔다
2. n번째 값이 저장되 있으면 해당값을 출력한다.
3. n번째 값이 없으면 배열에서 n-1, n-2 번째 값을 더해서 n번째 배열에 저장한다.
4. 원하는 출력에 도달할때까지 2번으로 돌아가서 반복한다

```javascript
let fibonacci = function (n) {
  const memo = [0, 1];
  const aux = (n) => {
    // 이미 해결한 적이 있으면, 메모해둔 정답을 리턴한다.
    if (memo[n] !== undefined) return memo[n];
    // 새롭게 풀어야하는 경우, 문제를 풀고 메모해둔다.
    memo[n] = aux(n - 1) + aux(n - 2);
    return memo[n];
  };
  return aux(n);
};
```

문제를 해결해서 테스트는 통과했지만 만약 테스트 통과조건에 시간제한이 있었다면 통과하지 못했을 것이다.
문제의 풀이를 생각할때 가능하다면 시간이 적게 걸리는 방식으로 해결 할수 있도록 여러방면으로 고민해서 풀이를 작성해야 될 것이다.
