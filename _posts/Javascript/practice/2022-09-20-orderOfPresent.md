---
title:  "연습 문제1 - orderOfPresent"
excerpt: "연습 문제1 풀이"

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

총 조의 수 N, 발표 순서 K가 주어질 때    
발표 순서가 총 경우의 수 중에서 몇번째인지 리턴해야합니다.

모든 경우의 수가 담긴 배열은 번호가 작을수록 앞에 위치한다고 가정합니다.    
ex) N = 3일경우, [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

<br>

입력
===
인자 1: N

Number 타입의 1 <= N <= 12인 조의 개수

인자 2: K

Number타입의 Array (0 <= index)

ex) n이 3이고 k가 [2, 3, 1]일 경우

모든 경우의 수를 2차원 배열에 담는다면 [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]이 되고,

반환하는 값은 3이 됩니다.


문제풀이
===

## 1. 순열을 이용하여 모든 경우의 수를 구한다.
---
문제를 보고 제일 처음 생각한 풀이 방식이다.   

Pseudo Code   
1. 주어진 순서 K로 만들 수있는 모든 경우의 수를 순열로 만든다.
2. 만들어진 경우의 수를 오름차순으로 정렬한다.
3. 앞에서 부터 K와 경우의 수를 순차적으로 비교한다.
4. 비교한 값이 일치할때 해당 순서를 리턴한다.

```javascript
function orderOfPresentation (N, K) {
  let arr = permutation(N,K) // 1. 경우의 수 순열로 만듬
  let result = 0
  arr.sort()  // 2. 오름차순 정렬
  arr.forEach((v,idx,arr)=>{ 
    if(compareArray(v,K)){  // 3. K와 경우의 수 순차적 비교
      result = idx // 4. 일치할때 순서 저장
      break
    }
  })
  return result // 4. 일치할때 순서 리턴
}
```

시행착오   
1. 주어진 순서가 배열로 이루어져 있어 배열을 바로 비교할 수 없었다.   
-> JSON.stringify를 사용하여 배열을 Json 문자열로 변환하여 비교하였다.   
* JSON.sringify : JavaScript 값이나 객체를 JSON 문자열로 변환합니다.   
2. 순서의 숫자가 9까지는 동작하였으나 12까지 증가하자 stack overflow가 발생하였다.   
-> 발표 순서는 순열로 만들어 입력이 12로 들어오면 최대 크기는 12!이다.   
이때 stack overflowd의 발생으로 순열을 전부 생성하는 것은 무리라고 판단하여 다른 방식을 탐색하였다.


```javascript
function orderOfPresentation (N, K) {
  let arr = permutation(N,K)
  let result = 0
  arr.sort()
  arr.forEach((v,idx,arr)=>{
    if(compareArray(v,K)){
      result = idx
      break
    }
  })
  return result
}

const compareArray = function(a, b){
  if(JSON.stringify(a) == JSON.stringify(b)){
    return true;
  }
  else{
    return false;
  }
}

function permutation(N,K) {
  // TODO: 여기에 코드를 작성합니다.
  
  if(N == 1) 
  {
      //console.log(N)
      return K.map((v)=>[v])
  }
  //console.log(K)
  K.forEach((fixed,idx,arr) => {
    //console.log(N)
    const rest = [...arr.slice(0,idx), ...arr.slice(idx+1)];
    console.log(rest)
    const permut = permutation(N-1,rest)
    const attach = permut.map((v) => [fixed, ...v]);
    result.push(...attach)
    //console.log(result)
  })
  return result
}
```

## 2. 순서를 계산 할 수 있는 수식을 만든다.
처음 생각한 풀이에서 수행횟수가 너무 많은게 문제가 되었으므로 수행횟수를 줄여서 문제의 답을 구하고자 했다.   
발표 순서는 순열의 오름차순으로 구성되므로 발표 순서를 수식으로 만들면 몇번째인지 계산할 수 있을거라 생각 했다.    

순열의 구성 방식이 "첫번째값, (첫번째값을 제외한 나머지 값중 선택1)"의 반복이므로   
[1,2,3,4,5,6,7]로 구성할 수 있는 순열의 수는 7!이 된다.   
이중 맨 앞자리가 7로 고정될경우 7을 제외한 수로 구성되는 순열이므로 6!이 된다.

그렇다면 [1,2,3,4,5,6,7]의 값으로 구성 된 순열을 오름차순으로 정렬했을때 첫번째 자리 값을 3으로 가지는 배열은 첫번째 자리값이 [1,2]로 가지는 배열보다 항상 뒤의 순서로 오게 된다.    
첫째자리를 1,2로 고정했을때 가질 수 있는 순열은 각 6!로 2*6!로 표현할수 있다.   
이를 좀더 정리하면 (첫째 자리수보다 작은값 * 남은수!)로 표현된다.   

문제로 돌아와서 [2,3,1]의 값의 순서를 구해보면   
1. 첫번째자리를 2로 했을떄 2를 제외한 배열에서 2보다 작은값 1로 만들수 있는 순열의수 2!
2. 두번째자리를 3으로 했을때 2,3을 제외한 배열에서 3보다 작은값 1로 만들수 있는 순열의 수 1!
3. 세번째자리를 1로 했을때 1을 제외한 배열에서 1보다 작은값은 없으므로 만들수 있는 순열의 수 0!
4. 2! + 1! + 0! = 3

이 과정을 Psedo code로 만들면

Psedu code
1. 배열의 첫번째 값을 고정한다.
2. 고정한 값을 제외한 나머지 배열을 구한다
3. 배열중 고정한 값보다 작은 값의 갯수를 구한다.
4. 작은값의 갯수와 남은 배열의 수로 만들 수 있는 순열의 수를 곱한다.
5. 남은 배열을 가지고 1.의 과정으로 돌아가 남은 배열의 크기가 0이 될때까지 반복한다.
6. 4.에서 구해진 모든 값을 더한다.

```javascript
function orderOfPresentation (N, K) {
  let result = 0

  K.forEach((fixed,idx,arr)=>{  // 1. fixed 값이 첫번째값이 된다. / 5. 반복한다.
      const rest = [...arr.slice(idx+1)]; // 2. 고정값을 제외한 나머지 배열을 구한다.
      const lowNumber = rest.filter((element)=> element < fixed) // 3. 배열중 고정값보다 작은값을 구한다.
      result += lowNumber.length*factorial(rest.length) // 4. 순열의수와 작은값을 곱한다.  / 6. 모든값을 더한다.
  })

  return result
}

function factorial(n) {
  function cal(n, result) {
    return n === 0 ? result : cal(n - 1, n * result);
  }

  return cal(n, 1);
}
```

2번쨰 풀이방식으로 문제를 해결하였다.   
이번 문제를 풀면서 수행시간을 고려하지 않아 풀이에 시간이 걸렸다.
문제를 해결함에 있어 메모리와 시간을 고려해서 알고리즘을 작성 해야함을 깨달았다.