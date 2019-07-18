# Web design 101

# 1. Display
The first thing is display. The more important are: inline, inline-block and block.

## 1.1. Inline
Inline elements behave like text, they are like lines, flow one next to each other.

Some tags with inline default display are: a, span, strong, em, b, i, mark.

They don't have width, height or transform.

They have padding and margin, but top and bottom won't affect the layout.

## 1.2. Inline-Block
Inline block elements behave like images, they are rectangles, but flow one next to each other.

Some tags with inline-block default display are: img, canvas, button, input, select, textarea.

They have the full [box model](https://www.w3schools.com/css/css_boxmodel.asp).

## 1.3. Block
Block elements don't flow one next to each other. They go one below the other.

Some tags with block default display are: div, body, header, nav, main, sidebar, section, article, h1, form, label, ul, footer.

They have the full box model.

# 2. Flex
## 2.1. Intro
The most important thing to know about flex is that it is a _linear_ layout.

It has two directions: row ➡️ and column ⬇️

flex-basis and flex-grow size childrens on the same vector ➡️ ➡️

justify-content aligns children on the same vector ➡️ ➡️

align-items aligns children on the perpendicular vector ➡️ ⬇️

More info [here](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).

By switching direction from none (or column) to row, a layout will also work on desktop.

Flex direct child nodes will have their display ignored in order to work as flex-childs (see guide). Note that text is also a node.

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="result" data-user="JakeActually" data-slug-hash="EoEpRM" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Text is a node">
  <span>See the Pen <a href="https://codepen.io/JakeActually/pen/EoEpRM/">
  Text is a node</a> by Jeyko Caicedo (<a href="https://codepen.io/JakeActually">@JakeActually</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## 2.2. How to
You can do any responsive layout if you decompose it in lines. Everything is lines and alignment. Here, I first did one row (red), then two columns (blue, aligned to right).

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="result" data-user="JakeActually" data-slug-hash="PEEeLr" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="All layouts are lines">
  <span>See the Pen <a href="https://codepen.io/JakeActually/pen/PEEeLr/">
  All layouts are lines</a> by Jeyko Caicedo (<a href="https://codepen.io/JakeActually">@JakeActually</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

In some cases "margin: auto;" is useful over justify-content, like the second column where one yellow item is apart from the others without dividing it in two more columns.

## 2.3. Flex vs grid
Layouts that are 2d and single deep (markup) are more easily expressed with grid. Greater deep is hard to express, at least until sub-grid is supported. Mixed directions are hard to express. Simple linearity is verbose to express. Finally, thinking in lines eases nesting and reuse.

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="result" data-user="JakeActually" data-slug-hash="RxxBNR" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Flex vs grid">
  <span>See the Pen <a href="https://codepen.io/JakeActually/pen/RxxBNR/">
  Flex vs grid</a> by Jeyko Caicedo (<a href="https://codepen.io/JakeActually">@JakeActually</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

# 3. Structure
## 3.1. Html
Use the ! emmet code. In VS Code, it looks like this.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

## 3.2. Body
The tags will usually look like this. Note the corresponding use of the tags. Note the recursive list nature of the navigation.

Header and footer should have an id as there can be more than one in the document. The id on the main tag should qualify the page and be unique across the entire site. Section an articles ids should be unique in the document but not across the site. Navigation ul tags should have classes to help styling different depths.

```html
<body>
    <header id="header">
        <nav>
            <ul class="menu">
                <li>
                    <a href="#"></a>
                    <ul class="submenu"></ul>
                </li>
                <li>
                    <a href="#"></a>
                </li>
            </ul>
        </nav>
    </header>

    <main id="home">
        <section id="posts">
            <article id="post-1"></article>
        </section>
        <section> id="clients"</section>
    </main>

    <footer id="footer"></footer>
</body>
```

# 4. Base site
Finally, an example of a base site. It implements the Material Design's navigation, so it's just a bar with a icon and a title, the nav appears from the left so it's usable from mobile first. Personally I think it's the most minimal form for a semi-long navigation (no accordions).

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="result" data-user="JakeActually" data-slug-hash="aymoVj" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Site base">
  <span>See the Pen <a href="https://codepen.io/JakeActually/pen/aymoVj/">
  Site base</a> by Jeyko Caicedo (<a href="https://codepen.io/JakeActually">@JakeActually</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
