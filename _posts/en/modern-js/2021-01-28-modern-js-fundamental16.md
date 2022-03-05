---
layout: post
title:  "Modern JavaScript 4.7"
subtitle: "Objects: Symbol type"
date:   2021-01-28 08:00:00 +1400
header-img: "img/post-bg-js.jpg"
header-mask: 0.5
catalog: true
hidden: false
lang: "en"
permalink: /en/modern-js/fundamental16/
tags:
  - javascript
  - modern js
---

## 4.7 Symbol type
Object property keys may be either of string type, or of symbol type.o

### symbols
A *symbol* represents a unique identifier. We can use `Symbol()` to create one.

```js
// id is a new symbol
let id = Symbol();
```

We can pass in a name, or a description, to the symbol which is mostly used for debugging.
```js
// id is a new symbol with a label "id"
let id = Symbol("id");
```

**Symbols are guaranteed to be unique**.
```js
let id1 = Symbol("id");
let id2 = Symbol("id");

console.log(id1 == id2); // false
```

The above comparison part evaluates to false because symbols are unique. A label is only a description not a value.

> Symbols don't auto-convert to a string. To show a symbol, use `.toString()` or `.description()` to get the label only.

### *Hidden* properties
By using symbols as a key, we can create a *hidden* properties of an object so that no other part of code can accidentally access or overwrite.

```js
let user  ={
    name: "euisblue"
};

let id = Symbol("id");

user[id] = 1;

// access the data using the symbol as the key
console.log( user[id] ); 
```

### what's the benefit?
Why use `Symbol("id")` over a string `"id"`? Because it is safer. 
When we use a string as a key, it can be accessed and/or overwritten. But with a symbol as a key, not that only the third-party cannot access nor overwrite, they (probably) won't even see it.

Also imagine you're using multiple scripts written by multiple other developers. They may want to add their own identifier to the object. If they use a string as a key, there may be a conflict and overwrite some properties by accident. But with a symbol, there will be no conflict.

### Symbols in an object literal
To add a symbol in an object literal `{ ... }`, use square brackets.

```js
let id = Symbol("id");

let user = {
    name: "euisblue",
    [id]: 1
};
```

### for ... in
Symbols are skipped in `for..in` loop. This is part of the general "hiding symbolic properties" principle.

### Object.assign
But when we copy an object using `Object.assign`, it will copy both string and symbol properties.

### Global symbols
All symbols are unique, however, we sometimes  want to create a shared entity using the same id. To achieve this, there exist a *global symbol registry*. Symbols inside this registry is called **global symbols**.

```js
// read from the  global registry
let  id  = Symbol.for("id"); // create one if doesn't exist

// read from the  global registry
let idAgain = Symbol.for("id");

console.log( id === idAgain ); // true
```

> Symbols inside the registry are called _global symbols_. If we want an application-wide symbol, accessible everywhere in the code – that’s what they are for.

### Symbol.keyFor
- `Symbol.for(key)` returns a symbol by name
- `Symbol.keyFor(sym)` returns a name by global symbol.
	--> internally looks up in the *global registry*, so it doesn't work for non-global symbols; it will return `undefined`.

```js
// get symbol by name
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");
let localSym = Symbol("local");

// get name by symbol
console.log( Symbol.keyFor(sym) ); // name
console.log( Symbol.keyFor(sym2) ); // id
console.log( Symbol.keyFor(localSym) ); // undefined, not global

// but we can use '.description'
console.log( localSym.description ); // local
```

### System symbols
There exist many *system symbols* that JavaScript uses internally.
For example:
- `Symbol.hasInstance`
- `Symbol.isConcatSpreadable`
- `Symbol.iterator`
- `Symbol.toPrimitive`
- ...and so on

You can see the full list of Well-Known Symbols [here](https://tc39.es/ecma262/#sec-well-known-symbols).

## Reference
- [4.7 Symbol type](https://javascript.info/symbol)