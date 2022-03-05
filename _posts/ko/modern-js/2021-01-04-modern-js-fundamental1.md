---
layout: post
title:  "모던 자바스크립트 2.1 - 2.5"
subtitle: "자바스크립트 기본 • 코드 구조 • 엄격 모드 • 변수와 상수 • 자료형"
date:   2021-01-04 07:00:00 +1400
author: "Blue"
header-img: "img/post-bg-js.jpg"
header-mask: 0.5
catalog: true
permalink: /ko/modern-js/fundamental1/
hidden: false
lang: ko
english: true
japanese: true
tags:
  - javascript
  - modern js 
---

## 2.1 Hello, World!

`Node.js` 와 같은 서버 사이드 환경이라면 `node` 명령어를 사용해서 js 스크립트를 실행 시킬 수 있다. 

```bash
$ node test.js
```

### 'script' 태그

`<script>` 태그를 사용해서 자바스크립트 코드를 HTML 페이지 어디에도 삽입할 수 있다.

```html
<!DOCTYPE html>
<html>

<body>
    <script>
        console.log('hello world');
    </script>
</body>
</html>
```

⚠️ 아주 간단한 코드의 경우는 제외하고, HTML안에 JS코드를 직접 삽입하는 것은 권장되지 않는다. 아래 **외부 스크립트** 파트 참고.

### 모던 마크업

- `type` 속성: <br>
    HTML4 에서는 `<script type='text/javascript'>` 와 같이 명시해주어야 했다. 모던 HTML 표준에선 의미가 바뀌어 자바스크립트 모듈에 사용된다.

- `language` 속성: <br>
`<script language="javascirpt">` 와 같이 현재 사용하고 있는 언어를 나타낼 때 사용되었으나, 지금은 기본형이 자바스크립트이므로 사실 상 의미가 없는 속성이다.

- 주석 (comments): <br>
    스크립트 안에 주석이 달린 코드를 마주하게 될수도 있다.
    ```html
    <script type="text/javascript"><!--
    ...
    //---></script>
    ```
    위 코드는 브라우저가 `script` 태그를 읽지 못 할 경우를 대비해서 스크립트의 실행을 막기위해 주석 처리를 한것이다. 하지만 지금 `script` 태그를 지원하지 않는 브라우저는 거의 없기 때문에 위와 같은 방식의 코드를 보게된다면 아주 오래된 코드라는 사실을 알 수 있다.

### 외부 스크립트

자바스크립트 코드를 여러개의 파일로 분할해서 사용할 수 가 있다. 분할한 파일은 `<script src='...'>` 와 같이 참조할 수 있으며 URL 전체를 속성으로 사용할 수도 있다.

```html
<script src="./logic/script1.js"></script>
<script src="./logic/script2.js"></script>

<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.11/lodash.js"></script>
```

⚠️ script에 src 속성이 있으면 안에 코드는 무시된다.

### 캐시 (cache)

브라우저는 다운 받은 스크립트를 캐시(cache)에 저장하기 때문에 성능에 이점도 있다. 쉽게 말해, 여러 페이지에서 동일한 스크립트를 사용하는 경우, 브라우저는 매번 다운을 받지 않고 캐시에 저장된 스크립트를 사용하게 된다.

## 2.2 코드 구조

### 문 (statements)

- 문법 구조(syntax constract)와 명령어(command)를 의미.
- 각각의 문은 `;` 세미콜론으로 구분한다.
    ```js
    // 2개의 alert를 세미콜론으로 구분했다.
    alert('hello'); alert('world');

    // 가독성이 안좋으니 아래와 같이 작성.
    alert('hello');
    alert('world');
    ```

### 세미콜론(semicolons)

- 세미콜론 자동 삽입(automatic semicolon insertion)

    → 자바스크립트는 줄 바꿈을 '암시적' 세미콜론으로 해석하기 때문에 아래와 같은 코드에서 세미콜론을 생략할 수 있다.

    ```jsx
    alert('hello')
    alert('world')
    ```

    하지만 자동으로 삽입되지 않는 **예외의 경우**도 있기 때문에 항상 세미콜론을 넣어준다. 실제로 JS 커뮤니티에서도 이를 권장한다.

### 주석 (comments)

- 한 줄 주석 →  `//`
- 여러 줄 주석 → `/* .... */` <br>
    중첩 주석은 지원하지 않는다 → `/*  /* ... */ */`
    ```js
    // 한 줄 주석
    alert ('this one is printed');

    /* 여러 줄 주석
    alert('this one wont be printed');
    */
    ```

## 2.3. 엄격 모드
[JavaScript ES5](https://www.w3schools.com/js/js_es5.asp)

- 2009년 ECMAScript5(ES5)가 등장 하기 전까지 JS는 호환성 이슈없이 잘 커왔다.
- ES5 에서 새로운 기능이 나왔고 이 기능들이 기존 JS 기능 중 일부를 변경해서 하위 호환성 문제를 야기할 수 있다.
- 그래서 변경사항 대부분을 ES5 기본모드에서는 비활성화 함.
- `"use strict"`를 사용하는 순간 모던한 방식으로 실행된다.
- `"use strict"` 는 반드시 최상단에 위치시킨다.

### 브라우저 콘솔

Chrome Dev Tools와 같은 개발자 콘솔은 기본적으로 `use strict` 가 적용되어있지 않다.

### 'use state' 꼭 사용해야 하나?

modern JS는 클래스와 모듈이라는 구조를 제공하는데 이 둘을 사용할 때 자동으로 `use strict` 가 적용된다.

## 2.4 변수와 상수

### 변수 (variable)

데이터를 저장할 때 쓰이는 **이름이 붙은 저장소**. `let` 키워드를 쓰며 `=` 연산자를 사용해서 데이터를 저장한다. 

```js
let name = 'euisblue';
let age = 21;

console.log('name: + ' + name); // name: euisblue
console.log('age: ' + age); // age: 21

// 이미 만든 변수에 새로운 데이터를 저장. 이전 값을 덮어쓴다.
name = 'john';
age = 24;

console.log('name: + ' + name); // name: john
console.log('age: ' + age); // age: 24
```

- `var` → 오래된 코드에서 `let` 대신 `var` 을 쓰는 경우가 있는데 **거의** 동일하게 작동한다.

### 변수 명명 규칙

1. 변수명에는 오직 문자와 숫자, 그리고 `$` 와 `_` 만 들어갈 수 있다.
2. 첫 글자는 숫자가 될 수 없다.
    ```js
    let userName1 = 'euisblue';
    let userName2 = 'euisblue';

    let $ = 'dollar';
    let _ = 'underscore';

    let 1abc; // 오류. 숫자로 시작할 수 없다.
    ```

3. 대소문자를 구분한다. `apple` 과 `Apple` 은 두 개의 다른 변수이다.
4. **예약어(keyword)**를 변수명으로 사용할 수 없다.
    ```js
    let let = 5;  // 불가능
    let var = 3;  // 불가능
    ```

### 상수 (constant)

변수의 값이 절대 변하지 않음을 의미하는 값. `const` 를 사용한다. 

```js
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";

let myColor = COLOR_RED;
console.log(myColor); // #F00
```

- 위 색깔 처럼 처음부터 값을 알고있는, 하드코딩한 상수는 대문자로 표기한다.
- 런타임에 값을 계산하지만 최초 할당 이후 값이 변하지 않는 상수는 일반적인 방식으로 변수명을 짓는다 (ex. `const pageLoadTime = /* 페이지를 로드하는데 걸린 시간 */`).

## 2.5 자료형

자바스크립트는 C++ 또는 Java와는 달리 **동적 타입 (dynamically typed)** 언어이다.

동적 타입이란 데이터 자체의 자료형은 존재하지만 값을 저장하는 변수는 타입이 없어서 언제든지 숫자에서 문자열로, 문자열에서 숫자로 바뀔수가 있다.

```js
let storage = "문자열"
storage = 123
storage = "다시 문자열"
storage = 1;
```

### 1. 숫자형

```js
let num = 123;
num = 3.14159;
```

정수와 부동소수점(floating point number)을 나타내며 IEEE-754 방식으로 저장한다.
IEEE-754 방식이기 때문에 2<sup>53</sup> - 1의 값을 나타낼 수 있다.

특수 숫자 값 (special numeric value) <br>
→ `Infinity`: 어떤 숫자보다 큰 값 (+∞) <br>
→ `-Infinity`: 어떤 숫자보다 작은 값 (-∞) <br>
→ `NaN`: 'Not a Number'의 약자로 부정확하거나 정의되지 않은 수학 연산을 사용하면 NaN을 반환한다.
```js
console.log(1/0); // Infinity
console.log(-1/0); // -Infinity
console.log('abc' / 2); // NaN
```

### 2. bigint

[ES2020 (ES11)](https://carloscaballero.io/es2020-features-in-simple-examples/) 에서 추가된 문법이며 현재 (2021-01) IE를 제외한 모든 브라우저에서 호환이 된다.
숫자형으로는 2<sup>53</sup> - 1 범위 밖의 숫자는 표현할 수가 없는데 BigInt를 사용하면 제한없이 표현이 가능하다.

`bigint`를 나타내기 위해 정수 리터럴 끝에 `n` 을 붙인다.

```js
const bigNumber = 1234567890123456789012345678901234567890n;
```

### 3. 문자형

```js
let str = "euisblue";
let str2 = 'Quadcore';
let str3 = `다른 변수를 삽입: ${str} and ${str2}`;
```

자바스크립트에서 `str` 과 `str2`와 같이 큰따옴표와 작은따옴표의 차이는 없다.

역 따옴표인 `str3` 의 경우 string interpolation이 사용 가능하다. 문자열 중간에 `${}`를 사용해서 원하는 변수나 표현식을 집어넣을 수 있다.

### 4. 불린형

논리 타입으로 `true` `false` 두 가지 밖에 없는 자료형.

```js
console.log(1 > 2); // false
console.log(2 > 1); // true

let a = 3;
let b = 5;
let isGreater = a > b;
console.log(isGreater); // false;
```

### 5. null

아래 세 가지를 의미하는 자료형으로 `null`값은 오로지 `null`만 표현할 수 있다.

→ nothing: 존재하지 않는 값 <br>
→ empty: 비어 있는 값 <br>
→ unknown: 알 수 없는 값

```js
let age = null; // 나이를 알 수 없음 
```

### 6. undefined

`null` 과 마찬가지로 오로지 `undefined`만 표현할 수 있는 자료형. 

→ 값이 할당되지 않은 상태를 의미

```js
let age;
console.log(age); // undefined
```

### 7. 객체

객체(`object`)형은 복잡한 개체를 표현하는 구조를 가지는 자료형이다.

### 8. 심볼

심볼(`symbol`)형은 객체의 고유 식별자(unique identifier)를 만들 때 사용된다.

### typeof 연산자

`typeof` 연산자는 데이터의 자료형을 반환합니다.

```js
typeof undefined // 'undefined'
typeof 1 // 'number'
typeof 1n // bigint'
typeof true // 'boolean'
typeof 'foo' // 'string'
typeof Symbol('id') // 'symbol'

typeof Math // 'object'
typeof null // 'object'
typeof alert // 'function'
```

`typeof Math`의 경우 수학 연산을 제공하는 내장 객체이므로 `object`가 출력된다.

`typeof null`의 결과로 `object`가 출력되었는데 이는 사실 상 버그이다. 하위 호환성을 유지하기 위해 수정하지 않고 남겨둔 것일 뿐, 객체는 아니다.

`function` 자료형은 따로 존재하지 않는다. 하지만 `typeof`의 피연산자가 함수일 경우 (형식 상 잘못 되었지만) 함수를 의미하는 `function` 을 반환하도록 설계가 되었다. 원래 함수는 객체형에 속한다.

## Reference
- [2.1 Hello, world!](https://ko.javascript.info/hello-world)
- [2.2: 코드 구조](https://ko.javascript.info/structure)
- [2.3: 엄격 모드](https://ko.javascript.info/strict-mode)
- [2.4: 변수와 상수](https://ko.javascript.info/variables)
- [2.5: 자료형](https://ko.javascript.info/types)