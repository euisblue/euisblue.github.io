---
layout: post
title:  "Modern JavaScript 4.4"
subtitle: "Objects: Object methods, 'this'"
date:   2021-01-25 07:00:00 +1400
header-img: "img/post-bg-js.jpg"
header-mask: 0.5
catalog: true
hidden: false
lang: "en"
permalink: /en/modern-js/fundamental13/
tags:
  - javascript
  - modern js
---

## 4.4 Object methods, "this"
Let's recall what object is from previous units.
**Object** - an entity that represents the real world object.
```js
let user = {
    name: "euisblue",
    age: "19"
};
```

Objects in the real world have an action associated to it. For example, a human can _move_, _speak_, _eat_, and so on.. Similarly, objects in JavaScript can have an  _action_.

## Methods
```js
let user = {
    name: "euisblue",
    age: "19"
};

function sayHi() {
    console.log("Hi!");
}

// using a declared function
user.sayHi = sayHi;

// using a function expression
user.sayBye = function() {
    console.log("Bye!");
};

user.sayHi(); // Hi!
```

We added an _action_ or a **method** to the `user` object and it can speak now.

### Method shorthand
```js
// these objects do the same
user = {
    sayHi : function() {
        console.log("Hi!");
    }
};

// method shorthand
user = {
    sayHi() {
        console.log("Hi!");
    }
}
```
We can omit `function` and just write `sayHi()`. This shorter syntax is easier to read and is preferred to use in almost all cases. *Seems like there're exceptions but not discussed in this unit*.

## "this" in methods
We can access the object from the method using `this` keyword.
```js
let user = {
    name: "euisblue",
    sayHi() {
        console.log(`Hi! ${this.name}`);
    }
};

user.sayHi(); // Hi! euisblue
```

It is also possible to access the object without using `this`.

```js
let user = {
    name: "euisblue",
    sayHi() {
        console.log(`Hi! ${user.name}`);
    }
};

user.sayHi(); // Hi! euisblue
```

This approach, however, is risky. We can overwrite the outer object `user` to some other value and now `user.name` will reference something else or wont exist at all.
```js
let user = {
    name: "euisblue",
    sayHi() {
        console.log(`Hi! ${user.name}`);
    }
};

let admin = user;
user = null;

admin.sayHi(); // TypeError: null is not an object
```
The above code will work if we change `user.name` to `this.name`.

## "this" is not bound
The value of `this` is evaluated during the run-time.
```js
let guest = () { name: "Guest" }
let admin = () { name: "Admin" }

function sayHi() {
	console.log(this.name);
};

guest.f = sayHi();
admin.f = sayHi();

guest.f(); // Guest
guest.f(); // Admin
```

- Advantage: Reusability
- Disadvantage: More freedom -> more mistakes

## Arrow functions
Arrow functions do not have `this`.
```js
let user = {
    firstName: "Yuu",
    sayHi() {
        let arraw = () => alert(this.firstName);
        arrow();
    }
};

user.sayHi(); // Yuu
```

## Reference
- [4.4 Object methods, “this”](https://javascript.info/object-methods)