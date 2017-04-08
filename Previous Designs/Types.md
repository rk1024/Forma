# Types
So Forma is incredible flexible. However, it does have some basic builtin types. These are listed here.

## Builtin

### Integer (int)
Adjusts to size of the integer, cannot be overflowed. 

### Modular Integer (mint)
Acts similar to an unsigned int. Wraps around and has a value in the range [0, max)

### Overflow Integer (oint)
Acts simimlar to a signed int. Specify the number of bits that will be needed and it will act like a signed integer of that length. 

### Native List (<>, nlist)
Similar to arrays in C, C++. Has a fixed size and cannot be grown or shrunk. Note that in Forma THESE ARE BOUNDS CHECKED!

### Statement List ({}, slist)

### List ([], list)
Linked list. Less performance heavy than nlist, but good at iteration and easily modifyable

## StandardBase

### 
