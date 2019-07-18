# Css principles

# 1.- Components
Style elements by its relation to its component.

```css
  .modal h1 {}
```

Flatten as posible, but use subcomponents if they are more expressive.

```css
  .modal .grid-item img {}
  .modal .grid-item a {}
```

Areas can be components.

```css
  #login form {}
  #login button {}
```

# 2.- Don't prefix structure
Instead of this

```css
  .modal {}
  .modal-title {}
```

do this

```css
  .modal {}
  .modal .title {}
```

# 3.- Order
Declare things in the order they appear on the site.
Describe components variations before describing its children.

```css
  .modal {}
  .modal.visible {}
  
  .modal h1 {}
  .modal.visible h1 {}
```

# 4.- Track root components
Root components are the ones preventing collision, so check they don't collide.

```css
  #main-section .modal { color: blue; }
  #imported-section .modal { color: red; }
```

or

```css
  .modal { color: blue; }
  .super-modal { color: red; }
```

# 5.- Don't pollute
Beware of too specific styles on broad elements, it makes styles scatter and it's messy when importing.

Instead of

```css
  p { padding: 30px; }
```

maybe what is really wanted is something like

```css
  #content p { padding: 30px; }
```

This is fine because there is only one body element.

```css
  body { font-family: sans-serif; }
```

# 6.- Don't use !important

Overwriting should be done with stronger selectors.

```css
  #main-section .modal {}
```
