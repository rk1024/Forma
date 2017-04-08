# Syntax Extensions
Along with interfaces, syntax extensions and powerful metaprogramming are a core part of Forma. Some example syntax extensions are shown below.

## Where Clauses
Often when working with Forma's declaration syntax, lines can start to look very complicated. For example, take the interface defined earlier:
```
let a = function( interface<A>( invert(A item)->A ) myparam);
``` 
On first sight, the meaning is obscured due to the necessity of defining the interaface as the function restriction. Fortunately, using syntax extensions, we can pull this part out of the declaration
```
let a = function(Invertible myparam) 
  where Invertible = interface<A>(invert(A item)->A);
```
# Quickcheck Integration
The testing framework that is currently all the rage is Quickcheck[https://hackage.haskell.org/package/QuickCheck]. 
Using Quickcheck, it is possible to do property-based testing in a far more elegant way than using conventional means. 
To use Quickcheck-style testing in Forma, we can use the power of syntax extensions to write
```
let Invertible = interface<MultaplicativeGroup A>(invert(A item)->A)
                    satisfying<x> invert(x) * x = identity(A);
```
Now, at compile time, the compiler will detect any types that are attempting to conform to the `Invertable` interface and will automatically check that they satisfy the condition. 
If they do not conform, you will receive a compiler error. 

## Object Notation
Now, it whould be widely known that at least one of the creators of Forma strongly dislikes object-oriented programming and, as such, an object-oriented programming was not explicitly included in Forma. 
However, as typical, one can be easily created using syntax extensions. Forma sees object-orientation as 
```
let MyCounterObject = struct(int a);

let increment = function(mutable MyCounterObject self, { self.a = self.a + 1; });
```
The usage of this would then look like
``` 
mutable counter = MyCounterObject(0);
increment(counter);
increment(counter);
```
While this bears resemblance to object-oriented programming, the syntax still feels rather unusual. Using the ObjectOriented syntax extension though, this becomes
```
let MyCounterObject = object({
  int a;

  let increment = method({ self.a = self.a + 1; });
});

mutable counter = MyCounterObject(0);
counter.increment();
counter.increment();
```

## Repetivite Brackets
You may have noticed in the previous syntax extension (and when writing everyday Forma) that you often get repetitive brackets such as 
```
let MyCounterObject = object({
  int a;

  let increment = method({ self.a = self.a + 1; });
});
```
While, yes, you could simpy go about you lives irritated by this and the world would be just fine, this is Forma! Using syntax extensions, this can be nicely simplified to 
```
let MyCounterObject = object {
  int a;

  let increment = method {
    self.a = self.a + 1;
  };
};
```

## Operators
I think we can agree that overall, operators in programming languages are a mess. Forma has attempted to fix this. 
Using the Operator syntax extension, the definition of operators is a simple and easy process.
In fact, operators do not exist in Forma. They are implemented in Operator, which is imported by default in the StandardBase module. 
To `Operator`, operators are simply syntactic sugar for the following function calls

Operator | Function Call 
--- | ---
+ | add(Addable a, Addable a) 
- | subtract(Subtractable s, Subtractable s) 
* | multiply(Multiplyable m, Multiplyable m) 
/ | divide(Dividable d, Dividable d) 

The interfaces `Addable`, `Subtractable`, `Multiplyable`, and `Dividable` are interfaces implemented in `Operator` that require the presence of each of these objects. 
