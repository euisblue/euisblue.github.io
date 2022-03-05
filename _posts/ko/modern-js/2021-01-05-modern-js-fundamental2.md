---
layout: post
title:  "모던 자바스크립트 2.6 - 2.7"
subtitle: "alert, prompt, confirm을 이용한 상호작용 • 형 변환"
date:   2021-01-05 07:00:00 +1400
header-img: "img/post-bg-js.jpg"
header-mask: 0.5
catalog: true
permalink: /ko/modern-js/fundamental2/
hidden: false
lang: ko
english: true
japanese: true
tags:
  - javascript
  - modern js 
---

## 2.6 alert, prompt, confirm을 이용한 상호작용

### - alert

```js
alert('hello world');
```

위 코드를 실행하면 'hello world'라는 메세지를 보여주는 모달 창(modal window)이 뜬다.

### - prompt

사용자가 입력할 수 있는 입력 필드와 확인 및 취소가 달린 모달 창을 띄운다.

```js
let name = prompt(message, [default]);
```

`prompt`는 두 개의 인자를 받는다. 

1. message → 사용자에게 보여줄 문자열
2. default → 초기 값

`[default]` 에서 대괄호는 이 인자가 필수가 아닌 선택값이라는 것을 의미.

```js
let name = prompt(message); // 잘 작동한다.
```

하지만 IE 에서는 초기값을 쓰지 않으면 `undefined`가 명시된다고 한다.

아래의 코드를 실행하고 '**euisblue**'를 입력하면 `name` 변수에는 문자열 '**euisblue**'가 저장된다.

```js
let name = prompt("당신의 이름은?", '이름을 입력해주세요');

console.log(name); // euisblue
```

### - 컨펌(confirm) 대화상자

```js
confirm(question)
```

사용자가 질문(`question`)에 확인을 누르면 `true`, 그 외의 경우는 `false`를 반환하는 모달 창을 띄운다.

```js
let isEven = confirm("숫자를 하나 생각해주세요. 이 숫자는 짝수인가요?")

console.log(isEven); // 확인을 눌렀으면 true 아니면 false
```

## 2.7 형 변환(Type Conversion)

- **묵시적 형변환**(Implicit Conversion)**이란**
  + 자동으로 변환이 이루어진다.
  + `alert`의 경우 전달받은 값이 무엇이든지 문자열로 자동 변환해서 모달 창에 출력한다.
    ```js
    alert(123);
    ```

- **명시적 형변환**(Explicit Conversion)**이란**
  + 의도를 가지고 직접 타입을 명시한다.
    ```js
    // 명시적으로 숫자 123을 문자열로 변환.
    let value = String(123);
    typeof(value); // 'String'

    // 문자열을 숫자로 변환.
    value = Number("123");
    typeof(value); // 'Number'
    ```

---

### 숫자형 변환

#### - 묵시적 형변환

나누기 연산의 경우 자동으로 문자열을 숫자로 형변환하여 값을 계산한다.

```js
console.log("9" / "3"); // 3이 출력된다.
```

숫자인 문자열이 아닌, 모든 문자열이다. 그래서 아래와 같이 `'abc'`를 가지고도 일단 연산은 가능하다. 하지만 결과는 `NaN` (Not a Number)이 된다.

```js
console.log('abc' / '3'); // NaN / 3 -> NaN
```

#### - 명시적 형변환

`Number(데이터)` 와 같이 형변환이 가능하다.

숫자형 변환 규칙

```js
Number(undefined); // NaN
Number(null);      // 0

Number(true);      // 1
Number(false);     // 0

Number('   ');     // 0 -> 공백이 제거되고 빈 문자열은 0
Number('  9 ');    // 9
Number('abc');     // NaN
```

---

### 불린형 변환

#### - 묵시적 형변환

논리 연산을 수행할 때 자동으로 불린형 형변환이 일어난다.

```js
console.log(3 > 5);  // false
console.log(3 < 5);  // true
```

#### - 명시적 형변환

`Boolean(데이터)` 와 같이 형변환이 가능하다.

불린형 변환 규칙

- `false` → 숫자 0, 빈 문자열, `NaN`, `undefined`
- `true` → 위 `false`에 해당하지 않는 모든 값

## Reference
- [2.6. alert, prompt, confirm을 이용한 상호작용](https://ko.javascript.info/alert-prompt-confirm)
- [2.7. 형 변환](https://ko.javascript.info/type-conversions)