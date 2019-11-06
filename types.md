# types

# unions

a "type A union B" (A \| B) is a type that can be A or B

typescript encodes unions very formally

```ts
type Animal = Cat | Dog;
```

c# can encode unions like this

```cs
class Animal { }

class Cat : Animal { }
class Dog : Animal { }
```

unions can't do nothing except branch, or better said, unions can't do nothing before branching

```haskell
case maybe of
    Just x -> "just"
    Nothing -> "nothing"
```

other interesting unions are interfaces. interfaces also branch but that is done by the compiler.

```cs
interface Animal { }

class Cat : Animal { }
class Dog : Animal { }
```

# intersections

a "type A intersection B" (A & B) is a type that is A and B

typescript encodes intersections very formally

```ts
type Serializable = Readable & Writable;
```

c# can encode intersections like this

```cs
interface Readable { }
interface Writable { }

class Serializable : Readable, Writable { }
```

intersections can do everything their components do

```cs
serializable.Read();
serializable.Write();
```

some interesting intersections are haskell typeclasses

```haskell
class (Functor t, Foldable t) => Traversable t
```

yup, traversables can do everything functors and foldables do

# inheritance

inheritance (T: A) is a form of intersection.

```cs
class Parent { }
class Child : Parent { }
```

is akin to

```ts
class Parent { }
class Anonymous { }

type Child = Anonymous & Parent;
```

is like saying "this new type can do everything its parent can plus..."
