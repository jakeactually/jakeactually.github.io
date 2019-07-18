# Thoughts on languages

A personal exploration of how languages should be

# Methods

A language should have methods. Methods are just functions that take the data as a implicit first parameter.

```haskell
-- haskell
length list
```

```cs
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

```cs
// C#
list.Drop(10).Take(10).Reverse();
```

But methods have the advantage of having autocomplete. There's no autocomplete without methods. Formally speaking, autocomplete is achieved when the data is written first so its type, thus its properties, can be inferred.

![intellisense](https://code.visualstudio.com/assets/docs/editor/intellisense/intellisense.gif)

# Types

A language should have types. The only use case for dynamic languages is for short scripts. Other than that, I don't want to manually keep track of my structures in a long project. If I change a definition, I want all the code that depended on that definition to break, on compile time.

# Inference

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

# Switch

Most code is
- selecting a branch
- perform the action of the branch

This can be encoded as unions and interfaces. In fact, unions and interfaces are fancy switches.

# Unions

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

# Interfaces

Interfaces are also a form of branching. Consider this C#

```cs
interface IDrawable { void Draw(); }

class Circle : IDrawable { void Draw() {} }
class Rectangle : IDrawable { void Draw() {} }
```

It can be said that IDrawable is a union type, and it can be a Circle or a Rectangle. Then consider this function

```cs
void Render(IDrawable drawable) {
  drawable.Draw();
}
```

Here, the interface chooses (branches) which version of the draw method is going to use, if the one of Rectangle or the one of Circle.

# Unions and interfaces

A language should have both unions and interfaces. Unions leave the control flow explicit and are useful in the short range. Interfaces leave the control flow implicit and are useful in the long range.

# Pattern Matching

Pattern matching consists of 5 things

- Check the type of the data
- Then safely extract its properties
- Make a equality test on this properties
- Make other tests on this properties
- Follow the resulting branch

```haskell
case point of
  Cartesian(2, 2) -> 4 -- equality test, x and y must be 2
  Cartesian(x, y) if x + y == 6 -> 6 -- other tests, here, sum must be 6
  Cartesian(x, y) -> x + y -- just property extraction
  Polar(angle, magnitude) -> angle + magnitude -- other types
  _ -> 0 -- default
```

Every language can do this, but some, like haskell, have first class syntax for it. This results in a powerful control flow tool.

# Generics

Languages should have generics. The purpose of generics is **not** code reuse, is type preservation. Interfaces reuse code. There can always be a list of type (interface) Any

```scala
val s: Seq[Any] = Seq(1, "a")

println(s.length)
```

So no generics are needed. In fact, dynamic languages and the linux kernel do this.

```c
list_for_each(list, &current->children) {
  task = list_entry(list, struct task_struct, sibling);
}
```

But this loses type guarantees. Generics preserve them.

```scala
val list: List[String] = List[String]("a", "b", "c")
list(0) // Guaranteed to be string
```

Some languages make generics easy to write by inferring them.

```scala
val list = List("a", "b", "c")
list(0) // Guaranteed to be string
```

# Implicit

Languages should be implicit. Languages should not be understood by everyone, but by persons that study that language. And languages should empower writers (programmers) not give them burden.

# Garbage collection

Languages should be garbage collected. Man, it feels good not having to worry about handling memory. Sometimes you can't afford that then you should use Rust.
