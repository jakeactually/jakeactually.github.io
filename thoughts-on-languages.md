# Thoughts on languages

A personal exploration of how languages should be

#Methods

A language should have methods. Methods are just functions that take the data as a implicit first parameter.

```haskell
-- haskell
length list
```

```C#
// C#
list.Count()
```

Some languages make this fact explicit

```rust
// Rust
impl Point {
  fn manhathan(self) {
    self.x + self.y
  }
}
```

Function composition is parallel to chaining

```haskell
-- haskell
f = reverse . take 10 . drop 10
```

```
// C#
list.Drop(10).Take(10).Reverse();
```

But methods have the advantage of having autocomplete. There's no autocomplete without methods. Formally speaking, autocomplete is achieved when the data is written first so its type, thus its properties, can be inferred.

![intellisense](https://code.visualstudio.com/assets/docs/editor/intellisense/intellisense.gif)

#Types

A language should have types. The only use case for dynamic languages is for short scripts. Other than that, I don't want to manually keep track of my structures in a long project. If I change a definition, I want all the code that depended on that definition to break, on compile time.

#Inference

A language should have type inference. Nevertheless, types were never _that_ annoying. We always had method chaining and expressions to evade type declaration and importing

```java
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;

InputStream is = socket.getInputStream();
InputStreamReader reader = new InputStreamReader(is);
BufferedReader br = new BufferedReader(reader);
```

```java
import java.io.BufferedReader;

BufferedReader br = new BufferedReader(
  new InputStreamReader(socket.getInputStream())
);
```

#Switch

Most code is
- selecting a branch
- perform the action of the branch

This can be encoded as unions and interfaces. In fact, unions and interfaces are fancy switches.

#Unions

Consider this haskell

```haskell
data Animal = Dog | Cat | Bird Int
```

This means that a Animal can be a Dog, a Cat or a Bird. Branching can be performed on this data.

```haskell
case animal of
  Dog -> print "woof!"
  Cat -> print "meow!"
  Bird height -> print ("flying at " ++ show height ++ " meters")
```

#Interfaces

Interfaces are also a form of branching. Consider this C#

```C#
interface IDrawable { void Draw(); }

class Circle : IDrawable { void Draw() {} }
class Rectangle : IDrawable { void Draw() {} }
```

It can be said that IDrawable is a union type, and it can be a Circle or a Rectangle. Then consider this function

```C#
void Render(IDrawable drawable) {
  drawable.Draw();
}
```

Here, the interface chooses (branches) which version of the draw method is going to use, if the one of Rectangle or the one of Circle.

#Unions and interfaces

A language should have both unions and interfaces.

Unions leave the control flow explicit and are useful in the short range.

Interfaces leave the control flow implicit and are useful in the long range.

#Generics
#Pattern Matching
#Garbage collection
#Implicit
