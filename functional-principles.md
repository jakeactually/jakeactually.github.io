# Functional principles

# 1. Evaluation - execution
Functions are just a evaluation of input to output. They don't affect the outside.

```js
const add = (x, y) => x + y;
```

Procedures are instead a series of steps or orders.

```js
const home = () => {
  document.querySelector('#header').style.display = 'block';
  document.querySelector('#body').style.display = 'block';
  document.querySelector('#footer').style.display = 'block';
};
```

To decrease a program complexity, always try to separate evaluation (functions) from execution (procedures). That is because functions can be proved correct.

# 2. Data - logic
Similar to evaluation - execution. Watch out for patterns where you can avoid conditionals and favor types or maps. Don't mix the data with the logic.

```js
const data = [
 { name: "John", authorized: false },
 { name: "Ana", authorized: true }
];

data.forEach(person => {
  if (person.name == current.name && person.authorized) {
   pass();
  } else {
   block();
  }
});
```

# 3. Abstraction
In functions and procedures, repetitive patterns can be abstracted.

```js
const show = section => {
  document.querySelector(section).style.display = 'block';
};

const home = () => {
  show('#header');
  show('#body');
  show('#footer');
};
```

Be sure that the pattern is consistent, if not, it is better to copy and paste the code.

# 4. Bindings
Think of bindings instead of variables.

Bindings are inmutable, so don't assign to them twice.

```php
<?
  $variable = 1;
  $variable = 2; // Don't
?>
```

Instead think of better names.

```php
<?
  $image = image();
  $proccessedImage = process($image);
?>
```

Name long or useful expressions.

```php
<?
  $valid = logged($user) && owns($user, $item);
  
  $height = 200;
  $margin = 5;
  $heightPlusMargin = $height + $margin * 2;
?>
```

If something is repeated, is good to caché it.

```php
<?  
  $post = $query->post[0];
?>
```

Use bindings to reduce logic to nicely ordered equations

```js
const sum = current ? 1 + 2 : 1 + 2 + 3;
const mod = sum > 2 ? 2 : sum % 2;
const valid = sum - mod == 6;
```

# 5. Functions are values
Change a function behaviour with a value throught currying, that is, functions that return functions.

```javascript
const makeListener = postId => () => alert(postId);

postButton.onclick = makeListener(postButton.id);
```

Define algebraic functions throught high-order, that is, functions that take functions as parameters. This allows powerfull abstractions.

```javascript
const work = howShouldIMapTheObject => ({
  timestamp,
  data: howShouldIMapTheObject(object)
});

const log = work(x => x.id);
```

# 6. Pass - state
Always pass the needed data and avoid state.

Don't

```js
let a;

const work = () => {
  a = 1;
  moreWork();
}

const moreWork() {
  alert(a);
}
```

Do

```js
const work = () => {
  moreWork(1);
}

const moreWork = neededData => {
  alert(neededData);
}
```

# 7. Types
Use the language type system, let the compiler help.

```php
<?
  function login(User $user): Connection {
    return $user->connect();
  }
?>
```

Use them with typeclasses - traits - interfaces to group types and apply generic functions to them.

```php
<?
  interface User {
    function connect(): Connection;
  }
  
  class FacebookUser implements User {
    function connect() {
      return new FacebookConnection();
    }
  }
?>
```

# 8. Avoid _this_

In javascript, _this_ is obscure. Prefer lambdas.

```javascript
el.onclick = ev => {
  console.log(ev.currentTarget)
};
```
