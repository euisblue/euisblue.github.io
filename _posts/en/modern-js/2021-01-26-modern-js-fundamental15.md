---
layout: post
title:  "Modern JavaScript 4.6"
subtitle: "Objects: Optional chaining '?.'"
date:   2021-01-26 08:00:00 +1400
header-img: "img/post-bg-js.jpg"
header-mask: 0.5
catalog: true
hidden: false
lang: "en"
permalink: /en/modern-js/fundamental15/
tags:
  - javascript
  - modern js
---

## 4.6 Optional chaining '?.'
> Recently added feature. Older browsers may need *polyfills*.

The optional chaining `?.` is a safe way to access nested object properties.

## The “non-existing property” problem
Let say you have an object `user` with a property `address` that has a `street` name. 
```js
function User(address) {
  this.address = address;
};

let user = new User({street: "some street"});
console.log(user.address.street); // some street
```

We can get the street name of a user by `user.address.street`.
What if the user did not provide such data and our `address` is `null`? 

> TypeError: Cannot read property 'street' of null

To avoid such issues we need check whether the object exist first, and then access its properties.
```js
let user = {}; // user has no address

let street = user.address ? user.address.street : undefined
```

Let say we want to get `user.address.street.name`.
```js
let user = {}; // user has no address

let streetName = user.address ? user.address.street ? user.address.street.name : undefined;
```

or we can use our AND (&&) property.
```js
let user = {}; // user has no address

let streetName = user.address && user.address.street && user.address.street.name;
```

You see how messy it quickly becomes. They added optional chaining `?.` to the language to solve these kind of issues.

## Optional Chaining

> If using Node to run JavaScript scripts using optional chaining, you need a Node version >= 14 and need `--harmony` flag to turn it on.

Syntax: `foo?.bar`
- if `foo` exists, that is `foo` is neither `undefined` nor `null`, it works as `foo.bar`.
- if `foo` is either `undefined` or `null`, it returns `undefined`.

### Short-circuiting
Similar to other bitwise operators, optional chaining also does it. When the value before `?.` is `undefined / null`, the evaluation will stop and return `undefined`.

### variants: `?.()`, `?.[]`
Optional chaining `?.` is not an operator. It is a special syntax construct that it also works with functions and square brackets.

```js
let user = {};
user.sayHi?.(); // nothing (no such method)

let euisblue {
    sayHi () {
        console.log("Hello!");
    }
}

euisblue.sayHi?.(); // Hello
```

Same when trying to access properties using square brackets.
```js
let key = 'first name';

let user1 = {
    'first name': "euisblue"
};

let user2 = { };

console.log(user1?.[key]); // euisblue
console.log(user2?.[key]); // undefined
```

We can also use optional chaining with `delete`. That is, delete the property if it exists.

``` js
delete user?.name // delete user.name if user exists
```

## Reference
- [4.6 Optional chaining '?.'](https://javascript.info/optional-chaining)