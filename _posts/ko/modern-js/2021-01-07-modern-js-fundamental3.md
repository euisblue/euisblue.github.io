---
layout: post
title:  "모던 자바스크립트 2.8"
date:   2021-01-07 07:00:00 +1400
subtitle: "기본 연산자와 수학"
header-img: "img/post-bg-js.jpg"
header-mask: 0.5
catalog: true
permalink: /ko/modern-js/fundamental3/
lang: ko
english: true
japanese: true
hidden: false
tags:
  - javascript
  - modern js 
---

#  2.8 기본 연산자와 수학

## 용어

- 피연산자 (operand) → 연산자가 수행하는 대상 <br />
    ex) `A * B` 라면 피연산자는 `A` 와 `B`

- 단항 연산자 (unary) → 한 개의 피연산자를 받는 연산자 <br />
    ex) `A = -A` 여기서 `-` 연산자는 부호를 뒤집는다.

- 이항 연산자 (binary) → 두 개의 피연산자를 받는 연산자 <br />
    ex) `A - B` 여기서 `-` 연산자는 뺄셈을 의미한다.

## 수학

- 덧셈 `+`
- 뺄셈 `-`
- 곱셈 `*`
- 나눗셈 `/`
- 나머지 `%`
- 거듭제곱 `**`

### 나머지 연산자 %

나머지 연산자 (modulus operator)는 두 수를 나누었을 때의 나머지를 반환한다.

```js
let a = 5;
let b = 3;
console.log(a % b); // 2
```

### 거듭제곱 연산자 **

거듭제곱 연산자 `**` 연산자를 사용해서 표현. $2^3$을 연산자를 사용해서 표기하면 `2 ** 3` 이 된다.

### 이항 연산자 '+'와 문자열 연결

덧셈 연사자를 사용해서 문자열을 합칠 수 있다.

```js
let name = 'euisblue';
let s = 'my name is ';
console.log(s + name); // my name is euisblue
```

두 피연산자 중 하나라도 문자열이면, 결과는 문자열이 된다.

```js
console.log("1" + 2); // 12
console.log(1 + "2"); // 12
console.log(1 + 2); // 3
console.log(1 + 2 + "9") // 39
```

이렇듯 문자열을 더하는 것은 가능하지만 빼는것과 나누는 것은 불가능하다.

그렇기 때문에 뺄셈과 나눗셈의 경우는 문자열이 아닌 숫자로 묵시적 형변환이 이루어진다.

```js
console.log("1" - 2); // -1
console.log(1 - "2"); // -1
console.log(1 - 2); // -1
console.log(1 + 2 - "9") // -6 
```

### 단항 연산자 +와 숫자형으로의 변환

덧셈 연산자인 `+` 를 단항 연산자로 사용할 수 있다.

일단 피연산자가 **숫자인 경우에는 아무일도 일어나지 않는다.**

음수에 `+` 를 한다고 해서 양수가 되는 것이 아님을 아래 코드에서 확인하자.

```js
let a = 1;
console.log(+a); // 1

let b = -1;
console.log(+b); // -1 (+1 이 아니다)
```

하지만 피연산자가 숫자가 아닌 경우에는, 숫자로의 형변환이 이루어진다.

```js
console.log(+true); // 1
console.log(+false); // 0
console.log(+""); // 0
```

`Number(...)` 와 동일한 일을 한다.

아래와 같은 일을 할 수 있다.

```js
let apples = "2";
let oranges = "3";

console.log(apples + oranges); // 23 
console.log(+apples + +oranges); // 5*
```

## 연산자 우선순위

수학에서의 [PEMDAS](https://www.mathsisfun.com/operation-order-pemdas.html) 처럼 자바스크립트에도 연산자의 우선순위가 있다.

## 할당 연산자

자주 사용하는 `=` ← 이것 또한 연산자 (할당 연산자).

### 할당 연산자 체이닝

할당 연산자의 특성을 사용 하여 여러 개를 연결(체이닝)할 수도 있다.

```js
let a, b, c;
a = b = c = 2;
console.log(a); // 2
console.log(b); // 2
console.log(c); // 2
```

### 복합 할당 연산자

복합 할당 연산자라는 것이 있다.

- `a += 5` → `a = a + 5` 와 같다.
- `b *= 2` → `b = b * 2`

```js
let n = 2;
n *= 3 + 5; // n *= 8

console.log(n); // 16
```

### 증가·감소 연산자

증가/감소 연산자는 숫자를 하나 늘리거나 줄이는데 사용된다.

#### 전위형 & 후위형 `++`

- 전위 증감 (pre-increment) → `++x`

값을 증가시키고, 변화한 값으로 연산을한다.

```js
let x = 2;
console.log(++x); // 3
console.log(x); // 3
```

- 후위 증감 (post-increment) → `x++`

연산을 끝낸 후에, 값을 증가시킨다.

```js
let x = 2;
console.log(x++); // 2 ; 출력 연산이 끝난 뒤, 증감.
console.log(x); // 3
```

#### 전위형 & 후위형 `--`

- 전위 감소 (pre-decrement) → `--x`
- 후위 감소 (post-decrement) → `x--`

증감/감소 연산자를 연산 중간에 사용하는 것은 바람직하지 않다.

1. 가독성이 떨어진다.
2. 결과값을 알 수가 없다. (Undefined Behavior)

```js
let x = 3;
console.log(2 * ++x - x--);
```

## 비트 연산자

비트 연산자는 인수를 32비트 정수로 변환하여 이진 연산을 수행한다.

- AND `&`
- OR `|`
- XOR `^`
- NOT `~`
- 왼쪽 시프트 `<<`
- 오른쪽 시프트 `>>`
- 부호없는 오른쪽 시프트 `>>>`

## Reference
- [2.8 기본 연산자와 수학](https://ko.javascript.info/operators)