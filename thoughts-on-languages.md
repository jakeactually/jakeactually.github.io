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

Piping is chaining, so a language shouldn't have both.

```fs
// F#
list |> List.skip 10 |> List.take 10 |> List.rev
```

```cs
// C#
list.Drop(10).Take(10).Reverse();
```

But methods have the advantage of having autocomplete. There's no autocomplete without methods. Formally speaking, autocomplete is achieved when the data is written first so its type, thus its properties, can be inferred.

![intellisense](https://code.visualstudio.com/assets/docs/editor/intellisense/intellisense.gif)

A counter argument to methods is that functions (like haskell ones) allow removing all type signatures. However I prefer autocompletion.

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

Destructuring is really important in functional languages, but not so quite in object oriented ones
where structure is easily accessed.

```cs
switch (animal) {
  case Dog d:
    return d.bark;
  case Cat c:
    return c.meow;
}
```

"Control flow as expressions" turns out useful even in object oriented languages. Above, it would helped remove the return keyword. Control flow as expressions help making [pure functions](https://en.wikipedia.org/wiki/Pure_function).

Pattern matching is mainly useful for handling [unions](https://jakeactually.github.io/types).

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

# Garbage collection

Languages should be garbage collected. Man, it feels good not having to worry about handling memory. Sometimes you can't afford that then you should use Rust.
