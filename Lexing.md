# Lexing 

Name | Description | Extra Notes
--- | --- | ---
Identifier | {Letter \| \_} ID\_CHAR\* |
Operator | {Punctuation}+ |
LParen | ( |
RParen | ) |
LBracket | [ |
RBracket | ] |
LBrace | { |
RBrace | } |
LAngle | < | May or may not be possible.
RAngle | > | May or may not be possible.
Comma | , |
Semicolon | ; |
Whitespace | {Space \| Newline}+ |
SQLiteral | '(.~('~\\'))' | Reserved for syntax extensions. The only way of making syntax extensions with unseparated sequences of characters.
DQLiteral | "(.~("~\\"))" | Used for strings
NumericLiteral | {Number} ID\_Char\* | May be replaced by RawNumeric
RawNumeric | {Number}+ | May be replaced by NumericLiteral
ID\_CHAR | {Letter \| Number \| Connector} |

