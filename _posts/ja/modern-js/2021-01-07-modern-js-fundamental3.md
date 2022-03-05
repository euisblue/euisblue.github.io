---
layout: post
title:  "JavaScriptの基礎 2.8"
subtitle: "JavaScriptの演算子"
date:   2021-01-07 07:00:00 +1400
header-img: "img/post-bg-js.jpg"
header-mask: 0.5
catalog: true
permalink: /ja/modern-js/fundamental3/
hidden: false
lang: ja
korean: true
english: true
tags:
  - javascript
  - modern js
---

#  2.8 演算子

## 用語

- *オペランド* (operand) → 演算子が適用されるもの。<br />
    例えば、 乗算`5 * 2`では、左のオペランド`5`と右のオペランド`2` 、二つのオペランドがあります。("オペランド" は "引数" と呼ばれることもあります)

- *単項演算子* (unary operator) → 演算子が単一のオペランドをもつ場合は *単項演算* です。 <br />
    例えば、負の単項演算`-`は、数値の符号を反転します：`A = -A`

- *二項演算子* (binary operator) → 演算子が2つのオペランドを持つ場合は *二項演算* です。 <br />
    同じ`-`演算子ですが、オペランドが二つある場合、二項演算による減算になります：`A - B`

## Maths

- `+` 加算
- `-` 減算
- `*` 乗算
- `/` 除算
- `%` 剰余
- `**` べき乗

### 剰余 %

剰余演算子(`%`)は、`a % b`の時、`a`を`b`で除算したあまりを返します。

```js
let a = 5;
let b = 3;
console.log(a % b); // the remainder of 5/3 is 2
```

### べき乗 **

べき乗演算子`a ** b`は`a`自身を`b`回かけます。

```js
console.log( 2 ** 2 );  // 4 (2 * 2, 2回)
console.log( 2 ** 10 ); // 1024 (2 * 2 *  ... * 2 * 2, 10回)
```

### 文字列の連結、二項演算子 +

二項演算`+`が文字列に適用された場合は、お互いの文字を結合します。

```js
let name = 'euisblue';
let s = 'my name is ';
console.log(s + name); // my name is euisblue
```

一方のオペランドが文字列の場合、その式の結果も文字列になることに注意してください。

```js
console.log("1" + 2); // 12
console.log(1 + "2"); // 12
console.log(1 + 2); // 3
console.log(1 + 2 + "9") // 39
```

しかし、二項演算`-`は文字列に適用できません。
減算と除算の場合、文字列は自動に数字型に変更します。

```js
console.log("1" - 2); // -1
console.log(1 - "2"); // -1
console.log(1 - 2); // -1
console.log(1 + 2 - "9") // -6 
```

### 数値変換 単項演算子 +

二項演算プラスは2つのオペランドが必要でした。しかし単項演算子プラスは、1つのオペランドに適用します。

単一の値に適用されるプラス演算子`+`は数値に対しては何もしません。
例えば、音数の数値に単項演算子プラスを付けても正数にはなりません。

```js
let a = 1;
console.log(+a); // 1

let b = -1;
console.log(+b); // -1 (it's not +1)
```

しかし、オペランドが数値ではない場合は数値に変換します。
```js
console.log(+true); // 1
console.log(+false); // 0
console.log(+""); // 0
```

単項演算子プラスは`Number(...)`と同じ効果があります。なので、近道としてこんな使い方ができます。

```js
let apples = "2";
let oranges = "3";

console.log(apples + oranges); // 23 
console.log(+apples + +oranges); // 5
```

## 演算子の優先順位

式が一つ以上の演算子を持つ場合、実行順はそれらの演算の*優先順位 (precedence)*により決められます。

全ての演算子手はないですが、下の[優先順位テーブル](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)をご覧してください。
![PEMDAS](/img/in-post/modern-js/fundamental3/js-pemdas-ja.png)

一つのオペランッドに適用する単項演算子プラス(`+`)の優先順位が一番高いです。その次が、べき乗(`**`)、乗算(`*`)、除算(`/`)、加算(`+`)、そして減算(`-`)の順に演算が実行します。

## 代入

優先順位テーブルをみると「代入」が一番下にあります。そうです。代入も演算子です。 <br>
代入演算子(`=`)の役割は、右側の数値を左側に返すことです。

```js
let a = 1;
let b = 2;

let c = 3 - (a = b + 1);

alert( a ); // 3
alert( c ); // 0
```

右から左に返すので、代入のチェーンというのができます。

```js
let a, b, c;
a = b = c = 2;
console.log(a); // 2
console.log(b); // 2
console.log(c); // 2
```

### インプレース(in-place)修正

変数の数値を変更し、同じ変数にその数値を保存するときがあります。

```js
let a = 0;  // a = 0
a = a + 5;  // a = 5

let b = 2;  // b = 2
b = b * 10; // b = 20
```

この表記は`+=`や`*=`を使用して短縮することができます。

```js
lat a = 0;
a += 5;     // a=5 (a = a + 5 と同じ)

let b = 2;
b *= 10;    // b = 20 (b = b * 10 と同じ)
```

このような演算子は、一般の代入演算子(`=`)と同じ優先順位になります。なので、他のほとんどの計算の後に実行されます。

```js
let n = 2;
n *= 3 + 5; // n = n * (3 + 5)

console.log(n); // 16
```

### インクリメント・デクリメント

変数を１増加または減少するオペランドがあります。

- **インクリメント** `++` 変数を１増加させる:
    ```js
    let x = 2;
    let y = 2;
    console.log(++x); // 3
    console.log(y++); // 2
    ```

- **デクリメント** `--` 変数を１減少させる:
    ```js
    let x = 2;
    let y = 2;
    console.log(--x); // 1
    console.log(y--); // 2
    ```

演算子`++`/`--`は式の中では使用しないようにしてください:
```js
let a = 3;
let b = 5;

let c = 2 * a++ - b--;
console.log(c); // 結果は？
```
上のコードように使う場合、可読性がなくし、結果もコンパイラーについて違うので*UB(undefined behavior)*になります。

## ビット演算子

ビット演算子は引数を 32ビットの整数値として扱い、それらのバイナリ表現のレベルで処理します。
ビット演算子は多くのプルグラミング言語でッサポートされています。

- `&` AND
- `|` OR
- `^` XOR
- `~` NOT
- `<<` LEFT SHIFT
- `>>` RIGHT SHIFT
- `>>>` ZERO-FILL RIGHT SHIFT

## Reference
- [2.8 演算子](https://ja.javascript.info/operators)