# MetaForma 
The most powerful feature of Forma is it's metaprogramming abilities. In fact, Forma is made up of two levels: BaseForma and MetaForma.
MetaForma is structured almost identically to BaseForma. 
It has functions (termed metafunctions), records (metarecords), and interfaces (metainterfaces). 
Essentially any concept that BaseForma has, MetaForma has as well (though its name is prefixed with meta).
While this may appear to be rather foreign, we have already seen many parts of MetaForma. 
It turns out that `function()`, `struct()`, and `interface()` are all metafunctions, provided through the CoreBase module (which is automatically imported into Forma projects). 
It turns out that most of Forma is actually implemented through MetaForma, imported through the module CoreBase. 
MetaForma essentially provides a window into the compiler. Through a combination of syntax extensions and MetaForma, the entire language is built.
You may be wondering, if all of BaseForma was built using MetaForma, isn't it possible to take MetaForma and to build up an entirely different language? The answer is yes. 
However, due to the fact that Forma is a compiled language after all, we must limit your creativirity slightly. 
In order to manage their transformation into LLVM bytecode, all MetaConcepts 
(a term encompassing metarecords, metafunctions, and pretty much everything else you do in MetaForma) 
must conform to a set of core metainterfaces. These metainterfaces are contained in the `Core` module and are the heart of Forma. 
Metafunctions take types as their paramaters. Similarly, metarecords take types as their 

