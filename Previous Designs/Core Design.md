Concepts

Meta - everything is performed at compiletime
- metainterface() - necessary for defining the behavious of all of the metastructs. One of the two top entities in the metaheirarchy, along with metastruct
  Low-Level:
  - byteconvert() - defines the properties of something that I can convert into LLVM data types
    things that conform to byteconvert() : records, functions, interfaces, etc. Anything at the Base level conforms to byteconvert
  ...
  other things like this
  ...
  Used for MetaLanguage:
  - callable() - defines the () syntax for calling things 
- metastruct() - all metaentities that are not interfaces (all concrete things)
  - interface() - just a type of metastruct() that checks that the thing that is plugged into it has the correct 
  - metafunction() - a metastruct that conforms to callable
  - record() - a metastruct that conforms to byteconvert() 

Base - everything is performed at runtime. Everything here conforms to byteconvert()
function()
