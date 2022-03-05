---
layout: post
title:  "JavaScriptの基礎 2.1 - 2.5"
subtitle: "Hello, world!・コード構造モダンなモード, 'use strict'・変数・データ型"
date:   2021-01-04 07:00:00 +1400
header-img: "img/post-bg-js.jpg"
header-mask: 0.5
catalog: true
permalink: /ja/modern-js/fundamental1/
hidden: false
lang: ja
korean: true
english: true
tags:
  - javascript
  - modern js
---

## 2.1・Hello, World!

`Node.js`などのサーバ環境では`$ node test.js`のようにコマンドでと一緒に実行することができます。

```bash
$ node test.js
```

### 'script' タグ

`<script>`タグを使用してHTML文書の任意の部分にJavaScriptプログラムを挿入することができます。

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

⚠️ とても簡単なコードの場合には、HTMLに`script`タグで挿入してもいいですが、直接挿入することは推奨されていません。下の**外部スクリプト**パートを参照してください。

### 最新のマークアップ

- `type` 属性: <br>
    HTML4では`<script type='text/javascript'>`のようにタイプを明示するのが必須でした。しかしモダーンHTMLではその意味が変わり、JavaScriptモジュールに使用されます。

- `language` 属性: <br>
`<script language="javascirpt">`は「scriptにJavaScriptプログラムを挿入します」という意味でscriptの言語を表示するために使いました。最近ではJavaScriptが基本系なので今は意味があまりない属性です。

- コメント(comments): <br>
    スクリプトの中に下記のようにコメントがついてるコードがある場合があります。
    ```html
    <script type="text/javascript"><!--
    ...
    //---></script>
    ```
    このコードはブラウザが`script`タグを読めない場合に対応して、スクリプトが実行されるのを防止するために使いました。今はほとんどのブラウザが`script`タグをサポートするので上のようなコードの場合は、古いコードであると思ってもオッケーです。

### 外部スクリプト

JavaScriptプログラムを複数のファイルに分割できます。分割されたファイルは`<script src='test.js'>`のように参照が可能です。またはURLをプロパティで渡すこともできます。

```html
<script src="./logic/script1.js"></script>
<script src="./logic/script2.js"></script>

<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.11/lodash.js"></script>
```

> ⚠️ scriptタグにsrc属性がある場合、そのタグの中のコードは無視されます。

### キャッシュ(cache)

ブラウザはダウンロードしたスクリプトをキャッシュ(cache)に保存するので性能に利点もあります。
例えば、複数のページで同じスクリプトを使う場合、ブラウザは毎回ダウンロードせず、キャッシュに保存されたスクリプトをロードして使います。

## 2.2・コード構造

### 文(命令文)

- 「文」というのは文法構造(syntax constract)と命令文(command)を意味します。
- それぞれの文はセミコロン(`;`)で区分します。
    ```js
    // 二つのalert命令文ををセミコロンで区分しました。
    alert('hello'); alert('world');

    // 読みにくいなので下記のように作成するのが普通です。
    alert('hello');
    alert('world');
    ```

### セミコロン(semicolon)

- 自動セミコロン挿入(automatic semicolon insertion)
    ```jsx
    alert('hello')
    alert('world')
    ```
    → JavaScriptは改行を'暗黙'のセミコロンと解釈します。しかし”常に”ではありません。なので文の最後には必ずセミコロンを付けてください。

### コメント(comments)

- 1行のコメント →  `//`
- 複数行のコメント → `/* .... */` <br>
    入れ子のコメントはサポートしない → `/*  /* ... */ */`
    ```js
    // 1行コメント
    alert ('this one is printed');

    /* 複数行のコメント
    alert('this one wont be printed');
    */
    ```

## 2.3・モダンなモード, "use strict"
[JavaScript ES5](https://www.w3schools.com/js/js_es5.asp)

- 2009年ECMAScript5(ES5)が登場する前までは、JSに互換性として問題はありませんでした。
- ES5からの新しい機能により、JSの本来の機能の一部が変更されたので、下位互換性の問題が発生する可能性があります。なので通常の場合は、ES5の変更事項を適用しないようにしました。
- スクリプトの最上段に`"use strict"`を入れると、モダンなモードでJavaScriptが実行されます。つまり、ES5の文法が適用されます。

### ブラウザコンソール

開発者コンソールを使う場合、`use strict`がデフォルトではないことに留意してください。

### “use strict” は必要？

モダンなJavaScriptは「クラス」や「モジュール」という構造をサポートしており、これらは自動的に`use strict`を有効にします。

## 2.4・変数と定数

### 変数(variable)

データを保存するとき使用する**名前がついているコンテナー**です。`let`キーワードを使用し、`=`演算子を使用してデータを保存します。

```js
let name = 'euisblue';
let age = 21;

console.log('name: + ' + name); // name: euisblue
console.log('age: ' + age); // age: 21

// 値の変更
name = 'john';
age = 24;

console.log('name: + ' + name); // name: john
console.log('age: ' + age); // age: 24
```

- `var` → 古いスクリプトには`let`の代わりに`var`を使えますが、**ほとんど**一緒です。微妙な違いありますが、気にする必要はありません。

### 変数のネーミング

1. 変数名には文字、数字、記号`$`と`_`のみを含む必要があります。
    ```js
    let userName1 = 'euisblue';
    let userName2 = 'euisblue';

    let $ = 'dollar';
    let _ = 'underscore';
    ```
2. 数値から開始はできません。
    ```js
    let 1abc; // ダメ！
    ```

3. 大文字小文字の区別します。
    ```js
    // 'apple'と'Apple'は別の変数です
    let apple = 5; 
    let Apple = 9;
    ```
4. 予約された名前（keyword）は変数名で使えません。
    ```js
    // 不可能
    let let = 5; 
    let var = 3; 
    ```

### 定数(constant)

定数を宣言する時は`let`の代わりに`const`を使います。

```js
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";

let myColor = COLOR_RED;
console.log(myColor); // #F00
```

- 定数の場合、変数名は大文字で表記します。
- ランタイムに値が決められる定数の場合、一般的な方式で変数名を付けます。
```js
const pageLoadTime = /*ページをロードするのにかかる時間 */;
```

## 2.5・データ型

JavaScriptはC++またはJavaなどとは違い、**動的タイプ(dynamically typed)言語**です.

動的タイプというのはデータを保存する変数のコンテナにはデータ型がないので同じコンテナに数字、文字列、Booleanなどをすべて保存することができます。

```js
let storage = "文字列";
storage = 123;
storage = "他の文字列";
storage = true;
```

### 【１】数値

```js
let num = 123;
num = 3.14159;
```

整数とIEE754方式の浮動小数点(floating point number)を表します。数字は`2の53乗 - 1`まで表現できます。

特別な数値型(special numeric value) <br>
→ `Infinity(+∞)`/`-Infinity(-∞)`:数学的な無限大 (+∞) を表します。<br>
→ `NaN`: 'Not a Number'の略字で計算上のエラーを表します。正しくないもしくは未定義の数学的な操作の結果です。
```js
console.log(1/0); // Infinity
console.log(-1/0); // -Infinity
console.log('abc' / 2); // NaN
```

### 【２】BigInt

[ES2020 (ES11)](https://carloscaballero.io/es2020-features-in-simple-examples/)から追加された文法であり、2021年１月の現在IE以外のブラウザでは互換できます。
数字型では`2の53乗 - 1`の範囲外の数字は表現できないがBigInt使えば制限なく表現できます。

普通の数字と`bigint`を区分するため、`bigint`最後に`n`を付けます。

```js
const bigNumber = 1234567890123456789012345678901234567890n;
```

### 【３】文字列

```js
let str = "euisblue";
let str2 = 'Quadcore';
let str3 = `다른 변수를 삽입: ${str} and ${str2}`;
```

JavaScriptで`''`と`""`はほぼ同じです。

バッククォートの場合、文字列補間(string interpolation)を使用することができます。変数や数式を`${...}`の中にラップすることで文字列の中で表現することができます。

### 【４】論理型(boolean)

論理タイプで`true`と`false`を表現できるデータ型。

```js
console.log(1 > 2); // false
console.log(2 > 1); // true

let a = 3;
let b = 5;
let isGreater = a > b;
console.log(isGreater); // false;
```

### 【５】'null' 値

`null`型には三つの意味がありますが、データとしては`null`だけを示します。
1. **nothing**: 存在しないデータ。
2. **empty**: 空いているデータ。
3. **unknown**: わからないデータ。

```js
let age = null; // 年齢不明
```

### 【６】'undefined' 値

`undefined`型は値が割り当てられていない状態を意味する

```js
let age;
console.log(age); // undefined
```

### 【７】オブジェクト

オブジェクト(`object`)は複雑なオブジェクトを表現する構造を持つデータ型です。

### 【８】シンボル

シンボル(`symbol`)型はオブジェクトの固有識別子(unique identifier)を作るときに使われる。

### typeof 演算子

`typeof`演算子はデータの資料型を返します。

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

`typeof Math`の場合、数学演算をサポータする内蔵オブジェクトなので`object`が返されます。

`typeof null`の結果は`object`ですが、これは実は、JSの設計の問題です。下位互換性を保つため修正せずに残しておいただけで、オブジェクトではありません。

`function`資料型はないです。しかし、`typeof`で関数を確認するとfunctionを返すように設計ができています。（本来関数はオブジェクトに属します）

## Reference
- [2.1・Hello, World!](https://ja.javascript.info/hello-world)
- [2.2・コード構造](https://ja.javascript.info/structure)
- [2.3・モダンなモード, “use strict”](https://ja.javascript.info/strict-mode)
- [2.4・変数と定数](https://ja.javascript.info/variables)
- [2.5・データ型](https://ja.javascript.info/types)