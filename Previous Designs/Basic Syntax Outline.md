MetaForma (to back these up)
```
import StandardComm as sc;

let Signature = metastruct();
let Statement = metastruct();

let MetaIterable<A> = interface { 
  next()->A;
};


let MetaIndexable<Content, Index> = metainterface {
  at(Index i)->Content;
};

meta def function(signature s, slist statements) {
};

mutable constructor_interfaces = metadict;
for (Any[] a in sc.types) {
  metadict[a] = function(

```

StandardBase (to back these up)
```
let string

Raw Forma 
```
import io

let main_signature = signature([ParamPair(int, string(['a', 'r', 'g', 'c'])),
                                ParamPair(array<string>, string(['a', 'r', 'g', 'v']))]);
let main = function(main_signature, {
  io.print(string(['H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd', '!');

  ifelse((greater(argc), 1), {
    io.print(add(string(['M', 'y', ' ', 'n', 'a', 'm', 'e', ' ', 'i', 's', ' ']), at(argv, 0)));
  }, {
    io.print(string['N', 'o', 't', ' ', 'e', 'n', 'o', 'u', 'g', 'h', ' ', 'a', 'r', 'g', 'u', 'm', 'e', 'n', 't', 's', '!']);
  });
});
```

Using StandardBase
```
import io

let main = function(int argc, string[] argv) {
  io.print("Hello World!");
  if (argc > 1) {
    io.print("My name is " + argv[0]);
  } else {
    io.print("Not enough arguments!");
};
```
