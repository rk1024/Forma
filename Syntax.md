# Syntax (and the structure of Forma)

### Example of Forma Code
Here's an example of Forma Code which we will analyze in the following sections. 
It servers to display the full default syntax of Forma.

```
import io;

let a = 3;

let main() = function((int argc, string[] argv), {
  io.print("Hello World!");
  let seven = NumberWrapper(7);
  sayHelloTo(seven); // Will result in a Compiler Error if NumberWrapper fails to conform to _Stringable
  return 0;
});

let _Invertible = interface<A>((invert(A item), A));
let _Addable = interface<A>((add(A left, A right), A));
let _Subtractable = interface<A>((subtract(A left, A right), A));
let _Multiplyable = interface<A>((multiple(A left, A right), A));
let _Divideable = interface<A>((divide(A left, A right), A));
let _FullArithmetic = interface(_Addable,
                                _Subtractable,
                                _Multiplyable,
                                _Divideable);

let NumberWrapper = struct(int my\_value);
assert(checkConforms(NumberWrapper, \_FullArithmetic),
       "NumberWrapper does not correctly conform to _FullArithmetic");

let add = function((NumberWrapper left, NumberWrapper right), {
  return add(left.my_int, left.my_int);
});
let subtract = function((NumberWrapper left, NumberWrapper right), {
  return subtract(left.my_int, left.my_int);
});
let add = function((NumberWrapper left, NumberWrapper right), {
  return subtract(left.my_int, left.my_int);
});
let add = function((NumberWrapper left, NumberWrapper right), {
  return subtract(left.my_int, left.my_int);
});
let string = function((NumberWrapper item), {
  return string(item.my_int);
});


let _Stringable = interface<A>(string(A item)->string);

let sayHelloTo = function((_Stringable item), {
  io.print(add("Hello ", string(item)));
});
```

Let's go through this code and learn the structure of Forma from it. 
```
import io;
``` 
Forma believes in having a very minimal standard library and being incredibly extensible. 
Because of this, most of Forma's functionality are stored in libraries called `modules`. 
In order to use these modules, we must `import` them using the syntax seen above. 
To use structs, records, or functions from these modules, it is necessary to prefix them 
with the name of the module. The standard module that is imported into projects for use in 
base Forma is `StandardBase`. Many other modules are shipped with Forma and can be easily 
imported.

```
let main() = function((int argc, string[] argv), {
  io.print("Hello World!");
  let seven = NumberWrapper(7);
  sayHelloTo(seven); // Will result in a Compiler Error if NumberWrapper fails to conform to _Stringable
  return 0;
});
```

Here we define our first function, `main`. `main` always serves as the entry point in Forma 
programs, taking the standard `argc` and `argv`. You may notice that the declaration of main
actually looks like an assignment and a function call, and this is because it is! 

Forma is actually a two-part language, made up of a base language called BaseForma and a meta 
language called MetaForma. MetaForma has many of the same constructs as BaseForma: structs and 
functions. However, MetaForma has the task of communicating your program to the compiler. 
While this may sound complicated, it is actually what gives Forma its incredible syntactic 
flexibility. So `function` is actually a metafunction that creates the a metastruct called 
`Function` which is used in communicating with the compiler. 

The next line, 
```
let seven = NumberWrapper(7);
```
creates a constant named `seven` and assigns it to a `struct` called `NumberWrapper` which 
has a constructor taking an `int`. To define a mutable variable instead, we use `mut`. Note, however, that Forma highly discourages the use of mutable variables due to the difficulty
they can lead to in producing easily readable and debuggable code. It turns 
out the `let` and `mut` are actually also metafunctions. However, they take advantage 
of a feature in MetaForma called `argsp`. `argsp` allows metafunctions to define the syntax of 
their arguments in a custom format which is parsed. The compiler actually allows us to
overload these metafunctions not only through changing the arguments, but also through 
changing the `argsp`. This allows us to have multiple different syntaxes in Forma using 
syntax extensions, such as the two equivalent ones below.
```
import io;
import RepetitiveBrackets;

// Not using the syntax extensions provided by RepetitiveBrackets
let main = function((int argc, string[] argv), {
  io.print("Hello World");
});

// Using the syntax extensions provided by RepetitiveBrackets
let main = function(int argc, string[] argv) {
  io.print("Hello World");
};
```
While this is a rather small improvement, you should be able to see how we could use to 
dramatically change Forma's syntax to whatever style we are programming in. For example, 
the standard set of modules includes modules such as `ObjectOriented`, `Functional`,
`Interfaces`, and many others that use syntax extensions and the minimalistic structure 
of Forma to emulate many different programming paradigms without the difficulty of going
against a language's syntax. 

Moving onto the next, we come to our first self-defined function. 
```
sayHelloTo(seven); 
```
Looking through our code, we see that later in the code we define `sayHelloTo` as 
```
let sayHelloTo = function((_Stringable item), {
  io.print(add("Hello ", string(item)));
});
```
Well, that's strange. We are passing in a `NumberWrapper` but the signature of `sayHelloTo`
states that the function takes a `_Stringable` as a parameter. Do we have a type mismatch here?.
It turns out that `_Stringable` is an interface. Interfaces are an incredible important 
concept in Forma. To enable polymorphism, most functions stay away from requiring types in
their type signature, instead choosing to use interfaces. For example, all of the basic math 
operators in Forma are derived from a module called `Operators` which defines a set of four 
interfaces: `_Addable`, `_Subtractable`, `_Multiplyable`, and `_Dividable`. In order to use 
the standard +, -, \*, / operators, we must ensure that our struct conforms to these interfaces. 
Conformance to an interface can be checked two ways: through the function `checkConformance`
and through passing into a function. The first method can be seen in the below line from 
the code sample:
```
assert(checkConforms(NumberWrapper, \_FullArithmetic),
       "NumberWrapper does not correctly conform to _FullArithmetic");
```
Here we check if the `NumberWrapper` struct conforms to an interface called `_FullArithmetic`. 
If it does not, we will raise a compiler error that will display the given message. Checking 
the conformance of your type for all of the relevant interfaces can be long and laborious at
times, and Forma was designed for ease of use. Conformance to interfaces is also checked by 
passing structs into functions. Due to Forma's static inference, it is capable of finding 
all of the functions that you pass a struct into and testing for conformance to those 
functions signatures. If your struct fails to confom, the compiler will display a compile-time
error message. 

So if interfaces are such an important concept in Forma, you may be wondering how to create
your own interface and how to make a struct conform to it. Fortunately, these two tasks 
constitute the next section of the example code, shown below:
```
let _Invertible = interface<A>((invert(A item), A));
let _Addable = interface<A>((add(A left, A right), A));
let _Subtractable = interface<A>((subtract(A left, A right), A));
let _Multiplyable = interface<A>((multiple(A left, A right), A));
let _Divideable = interface<A>((divide(A left, A right), A));
let _FullArithmetic = interface(_Addable,
                                _Subtractable,
                                _Multiplyable,
                                _Divideable);
```
Here we define some interfaces. We look at the first definition as an example. 
```
let _Invertible = interface<A>((invert(A item), A));
```
Similar to our function and struct definitions, the definition of a struct looks like an
assignment. This is because similar to functions and structs, an interface is a metarecord 
used for communicating with the compiler (called `Interface`) and the way we construct an
interface is using a metafunction. The angle bracket syntax is implemented using `argsp` 
and tells simply defines the type that is attempting to conform to `_Invertible` to be 
`A`. The `_Invertible` interface requires that we implement one function with the signature
`invert(A item)` that returns a struct of type `A`. 

You may notice that the last interface, `_FullArithmetic` is defined somewhat differently. 
It would be rather tedious to type 
```
let arithemeticer = function(((_Addable, Subtractable, _Multiplyable, Dividable) item) { ... });
```
Everytime we wanted to define a function that required that paramters conform to each of 
these interfaces. Checking conformance to all of these interfaces would also be tedious to 
write. Fortunately, Forma has a way of avoiding all of this tedious typing. We can combine
multiple interfaces into a single interface using the syntax 
```
let _FullArithmetic = interface(_Addable,
                                _Subtractable,
                                _Multiplyable,
                                _Divideable);
```
If any type conforms to `_FullArithmetic`, it conforms to all four of its subinterfaces. 

## MetaForma
So now that we have covered an example of basic Forma, it is time to dive a little deeper. 
You may remember from the previous section that many of the major components of BaseForma, 
such as `function`, `struct`, and `interface`, are actually metafunctions. So what are
metafunctions? Well, it turns out that they are simply functions that act on the BaseForma 
language, allowing us to modify syntax and create other language-level effects that would 
not be possible using only BaseForma. In order to learn how to program in MetaForma, we are
going to examine syntax extensions, which often rely heavily on MetaForma. For an explanation 
of these syntax extensions, see `Extensions Examples.md`.

### Where Clauses
The simplest type of syntax extension, `where` clauses are grouped into the general group 
of additional keywords. `where` clauses in Forma are designed to imitate those used in 
Haskell, allowing us to define functions using the syntax 
```
let a = function(Invertible myparam) 
  where Invertible = interface<A>((invert(A item), A));
```
In order to do this, we simply define a metafunction called where that is called when the 
parser/compiler sees the identifier `where`. 

## Scope in Forma
