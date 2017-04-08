# Parsing 
## Grammar

```
program
  | call 

call
  | ? in [mfunctions]
  | infix (? in [mfunctions])

function 
  | Created by argparser
  |
  |



parens 
  | LParen Stuff RParen

braces
  | LBrace Stuff RBrace

commas 
  | commas Comma stufff
  | stuff

angles (if possible)
  | LAngle stuff RAngle

brackets 
  | LBracket stuff RBracket

operators
  | operators Operator stuff
  | stuff

thing 
  | primary
  | parens
  | braces
  | brackets
  | commas 
  | semicolons

stuff
  | thing+

input 
  | stuff
```
