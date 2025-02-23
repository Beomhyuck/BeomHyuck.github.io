---
title:  "JavaScript 변수 선언"
excerpt: "JavaScript 변수 선언 3가지의 차이점"

categories:
  - Javascript
tags:
  - [Javascript, html]

comment: true

author: Beomhyuck

toc: true
toc_sticky: true
 
date: 2022-09-18
last_modified_at: 2022-09-19
---

JavaScript에서 변수 선언 방법에 대해서 알아본다.
 
JavaScript에서 변수 선언을 할때 데이터 타입을 따로 필요로 하지 않는다. 변수에 넣는 값에 따라서 동적으로 데이터 타입이 결정된다.  
변수에 데이터가 없는 경우 undefined 값이 들어간다.

JavaScript의 변수 선언에는 3가지 방법이 있다.   
1. var
2. const
3. let


Var
=== 
## 1. 중복선언
같은 변수명으로 선언해도 오류없이 새 값으로 할당된다.   

```javascript
var a = 10
console.log(a)  // 10

var a = 20
console.log(a)  // 20
```

## 2. 초기화 없이 선언
초기화 없이 변수명만 가지고도 선언이 가능하다.
```javascript
var a
console.log(a) // undefined

a = 10
console.log(a) // 10
```

## 3. 값 재할당
값을 다시 할당 할 수 있다.
```javascript
var a = 10
console.log(a) // 10

a = 20
console.log(a) // 20
```

## 4. Scope   
함수내부에서 선언된 값만 지역변수, 나머지는 전역변수로 취급한다.
```javascript
function LocalA()
{
  var a = 10
}

LocalA()
consol.log(a) // reference Error 
```

```javascript
if(true)
{
  var a = 10;
}

consol.log(a) // 10
```

let
===
## 1. 중복선언
중복 선언 불가능

```javascript
let a = 10
console.log(a)  // 10

let a = 20 // Syntax Error
console.log(a)  // 10
```

## 2. 초기화 없이 선언
초기화 없이 선언 가능
```javascript
let a
console.log(a) // undefined

a = 10
console.log(a) // 10
```

## 3. 값 재할당
값을 다시 할당 할 수 있다.
```javascript
let a = 10
console.log(a) // 10

a = 20
console.log(a) // 20
```

## 4. Scope   
선언된 변수는 블록 내부에서만 사용가능하다.
```javascript
function LocalA()
{
  let a = 10
  consol.log(a) // 10
}

LocalA()
consol.log(a) // reference Error 
```

```javascript
if(true)
{
  let a = 10;
  consol.log(a) // 10
}

consol.log(a) // reference Error
```

Const
===
## 1. 중복선언
중복 선언 불가능

```javascript
const a = 10
console.log(a)  // 10

const a = 20 // Syntax Error
console.log(a)  // 10
```

## 2. 초기화 없이 선언
초기화 없이 선언 불가능. 초기화 반드시 필요
```javascript
const a     //SyntaxError

const a = 10
console.log(a) // 10
```

## 3. 값 재할당
값을 다시 할당 할 수 없다. 초기화시 값 고정
```javascript
const a = 10
console.log(a) // 10

a = 20  // type Error
console.log(a) // 10
```

## 4. Scope   
선언된 변수는 블록 내부에서만 사용가능하다.
```javascript
function LocalA()
{
  const a = 10
  consol.log(a) // 10
}

LocalA()
consol.log(a) // reference Error 
```

```javascript
if(true)
{
  const a = 10;
  consol.log(a) // 10
}

consol.log(a) // reference Error
```

## 비교
   
||중복선언|초기화|재할당|스코프|
|:---:|:---:|:---:|:---:|:---:|
|var|가능|초기화 없이 선언가능|가능|함수내부만 지역변수, 나머지는 전역변수|
|let|불가능|초기화 없이 선언가능|가능|블록 내부에서만 사용가능|
|const|불가능|초기화 필요|불가능|블록내부에서만 사용가능|
   
<br><br>


호이스팅
===
JavaScript에서는 코드 실행전 변수 선언을 미리 해둔다. 따라서 뒤에서 선언된 변수라도 코드 앞에서 참조가 가능해진다.

var 로 선언할경우
```javascript
console.log(a) // undefined

var a = 10
console.log(a) // 10
```

let, const로 선언할 경우
```javascript
console.log(a) // ReferenceError

let a = 10
console.log(a) // 10
```
var로 변수를 선언하면 코드실행전 변수에 undefined값으로 초기화하여 변수 선언 되어있다.   

let과 const로 변수를 선언했을 경우 호이스팅이 발생하지 않은것 처럼 보이지만 이는 호이스팅의 동작이 다르기 때문에 발생한 문제이다.   
let/const로 선언할 경우 변수는 선언만 해두고 초기화는 변수 선언문을 만났을때 한다.
이렇게 변수선언과 초기화 사이에 참조할수 없는 구간은 TDZ(Temporal Dead Zone)이라고 한다.


JavaScript에서 변수를 선언할 수 있는 3가지 방법을 알아봤다.   
각 방법의 차이가 있으니 필요한 상황에 따라서 선택해서 사용하면 된다.  
하지만 대부분 추천하는 방법은 아래와 같으니 참고하자.

1. const 사용
2. 재할당이 필요한 경우 let 사용
3. var는 사용하지 않는다.