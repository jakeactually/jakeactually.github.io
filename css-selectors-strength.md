#Css selectors strength

# 1.- Order

The later style gets applied.

```css
.selector { content: "overridden"; }
.selector { content: "applied"; }
```

# 2.- Inline

Inline styles are considered _the latest_.

```html
<div style="content: 'applied';"></div>
```

# 3.- Tag < class < id

Id selectors are stronger than class selectors

class selectors are stronger than tag selectors

```css
#section { content: "applied"; }
.section { content: "can't override"; }
section { content: "can't override"; }
```

# 4.- Multiple

Selectors with multiple tokens are evaluated like this:

The one with more id tokens _or_

the one with more class tokens _or_

the one with more tag tokens

Example

```css
#article #div.div { content: "applied"; }
body section #article #div { content: "can't override"; }
```

Both have the same amount of id tokens but the
first has more class tokens so the
number of tags is not considered
