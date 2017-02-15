# Forma

*Name subject to change.*

Functions:

```
def Foo(arg1, arg2) => value;

def Bar(arg1, arg2) {
  <do stuff>

  return value;
}
```

## Variables

Variables in Forma have static types, but the language allows for type inference.  This allows for the following:

```
let x = 1; // Creates an immutable int variable
var y = "hello"; // Creates a mutable string variable

y = x; // Will cause a compiler error
```

To explicitly declare the type of a variable, the following syntax can be used:

```
let int x = 1;

string y = "hello";
```

## Types

### Record Types

The record type is the simplest kind of type - it is essentially an atomic, un-evaluatable function. The members of a
record are represented by the arguments passed to its constructor.

Because a record is a function at heart, records can be defined as functions with no body, like this: *(Can we get away
with this?)*

```
def MyRecord(int a, char b);
```

Record types are intended to be atomic, and as such are immutable.  If a modified copy of a record is needed, the `with`
syntax may be used:

```
let x = MyRecord(1, 'a');
let y = x with(a = 2);
```

### Structure Types

```
struct MyStruct {
  int a;
}
```

## Interfaces

Some sketches of interesting ideas in interfaces (as well as other stuff)

```
interface MyInterface {
  def AbstractFunc(x);

  def DefaultedFunc(y) => 2 * AbstractFunc(y);
}
```

```
declare MyType is MyInterface {

}
```

```
def A(int x, int y);

interface Foo<T> {
  def int Get(this T);

  def Set<TValue>(this T, TValue);
}

provide Foo<A> {
  def Get(this A(x,)) => x;

  def Set<int>(this A, int) => throw TypeImmutableError(typeof(A));

  def Set<T>(this A, int) => throw BadTypeError(typeof(this));
}

struct B {
  A myA;
}

provide Foo<B> with myA;

struct C {
  var A myA;
}

provide Foo<C> with myA {
  def Set<int>(this A, int value) => this.myA := this.myA with(x = value);

  // Set<T> is still provided by myA to throw a BadTypeError
}
```