# Compiler Interface

## Summary
In order to compile the code, the metacode must submit a variety of constructs to the compiler for compilation and transformation into the bytecode. 
Obviously, a structure to this input is necessary to prevent the difficulties of compiling unknown objects.
In fact, in order to ensure a very structured interaction with the compiler, a very limited set of possible interactions is defined
**Note:** All of these interactions are defined in the `Core` module. 

### MetaStructs
The 3 main metastructs needed for interaction with the compiler are `Function`, `Interface`, and `Struct`. 

`Function` - Contains all of the metadata such as signature, name, etc. necessary for the function.
Also contains a `Block` that contains the Forma code that makes up the function

`Interface` - Don't know yet

`Struct` - Don't know yet

There are some other MetaStructs that help for interaction with the main 3 metastructs.
Note that these are all used to make up the main metastructs.

`Block` - A sequence of calls surrounded by curly braces

### MetaFunctions
`compile(Function)` - Passes a `Function` to the compiler for compilation
`compile(Interface)` - Passes an `Interface` to the compiler for compilation
`compile(Struct)` - Passes a `Struct` to the compiler for compilation

### Compiler Functionality
Interaction with the compiler is not one way. 
The metacode can also request certain functionality from the compiler.
This functionality is listed below:

`emulate(Block)` - The compiler loops through the Block and extracts metadata from it such as any local variables defined.
This data is then returned to the metacode in the format of a metastruct.
**Usage:** Necessary for the implementation of syntax extensions such as `ObjectOriented` 
due to the necessity of pulling information such as member variables and functions out of blocks.
