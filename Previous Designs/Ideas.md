# Forma
## Variables 

Variables in Forma have static types, but the language allows for type inference.  This allows for the following:

```
let x = 1; // Creates an immutable int variable
mutable y = "hello"; // Creates a mutable string variable

y = x; // Causes a compiler error
```

To explicitly declare the type of a variable, the following syntax can be used:

```
let (int) x = 1;
let (string) y = 
```

## Types
### Record Types

To define a normal record type, we use
```
let MyRecord = struct(int a, char b);
```

Forma is also capable of dynamically modifying records at runtime, similar to the behavior found in scripting languages. 
In order to define a mutable record type, we use
```
mutable MyMutableRecord = struct(int a, char b);
```

To instantiate a record type, we simply use 
```
let rec = MyRecord(10, 'a');
```
or
```
mutable mrec = MyRecord(10, 'a');
```
If the record type is mutable, it's fields can be changed. If immutable, they are constant. 

## Interfaces

Interfaces are a crucial constant in Forma. There are two types of interfaces: interfaces and anonymous interfaces. Named interfaces are defined with 
```
let MyInterface = interface<A>(invert(A item)->A);
```
```
let a = function( interface<A>( invert(A item)->A ) invertable);
```

