# Mixed style guide

# 1. Strings

In general, always use single quotes unless interpolation is required

## 1.1. Php

Simple text

```php
<?
  $array = ['key' => 'value'];
?>
```

Interpolation

```php
<?
  $string = "Text $variable text";
?>
```

Html

```php
<?
  ob_start();
  ?>
    <p><?= $variable ?></p>
  <?
  $string = ob_get_clean();
?>
```

## 1.2. Javascript

Simple text

```javascript
const string = 'www.example.com';
```

Interpolation

```javascript
const string = `${variable}`;
```

## 1.3. Html, Css

Always use double quotes

```html
<input type="text">
```

```css
input[type="text"]
```

# 2. Casing

In general, use lowerCamelCase for variables and symbols and PascalCase for types.

Use lowerCamelCase for variables and symbols and PascalCase for types in:
sql, C#, java, scala, kotlin, haskell, javascript, elm, and php.

Use snake_case for variables and symbols and PascalCase for types in:
c, rust, c++, python, elixir and ruby.

Use hyphen-case in:
html and css

# 3. Characters
Use spaces in front of commas and to separate operators.

```js
const f = (a, b, c) => {};

let a = 1 + 2 % 3 > 0 || true;
```

Brackets and square brackets should be like this, except in Haskell like languages and if it contradicts specific language guides (brackets on C#). Indent properly and delete unnecesary blank lines.

```js
if (true) {
  let array = [
  ];
}
```

# 4. Routes and files

On apps, use rails convention for routes: hyphen-case, no trailing slash.

C# convention is also acceptable: PascalCase, no trailing slash.

On blogs, wordpress convention may be used: hyphen-case with trailing slash

Files that will appear in a url should be named hyphen-cased.

Source code files should be named according to its language casing.
