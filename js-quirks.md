# Js quirks

# 1. Booleans
In javascript and some other languages you can use many types as true or false.

```js
1 == true
2.5 == true
"a" == true
[] == true
{} == true

0 == false
"" == false
undefined == false
null == false
```

Some tricks come from this:

Easy checking

```js
if (!maybeValue) {
  exit();
}
```

Short circuiting as coalescence (prefer function and destructuring default arguments though)

```js
let a = maybeValue || default;
```

Short circuiting as null propagation

```js
let a = b && b.c;
```

# 2. References
In javascript, passing number, string, bool or any native results in that value copied.

```js
let a = 1;
let b = a;

b = 2;
a; // 1 // Unchanged
```

When passing objects or arrays, you pass a reference. The reference does get copied, but it is a reference.

```js
let a = { x: 1 };
let b = a;

b.x = 2;
a; // { x: 2 } // Changed
```
