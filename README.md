# ASS_MBLY

Commands
---
Commands are formed by writing the word ASSEMBLY with specific letters replaced with underscores.

### Move value of Loc2 + imm to Loc1

imm is a 2 bit two's compliment integer where a letter represents a 1 and an underscore represents a 0
```
_S(Loc1)(Loc2)(imm)
```
### Add value of Loc2 + imm to Loc1
```
AS(Loc1)(Loc2)(imm)
```

##### Locations
2 bits

$r1    -> `**`

$sp  -> `_*`

memory[$sp]  -> `*_`

$zero -> `__`


### Jump to command at Loc1 if value at Loc2 satisfies Condition

$r1 will be overwritten with the return location
```
A_(Loc1)(Loc2)(Condition)
```
#### Conditions
2 bits

###### First Bit

Greater Than -> `*`

Equal to -> `_`

###### Second bit

$r1    -> `*`

$zero -> `_`

### IO
```
__SE(R/W)(char/int)(Loc)
```
Read -> `*`

Write -> `_`

Char -> `*`

Int -> `_`

### Subroutine
The address of all subroutines will be initialized into memory in order of appearance starting at mem[-1] and continuing towards negative infinity.

The return address will be put into $r1

`_ _ _ _ _ _ _ _`

### EXIT
Exit code is a non-zero unsigned int
```
_ _ _ _ (Exit code)
```
1 -> Clean Exit

15  -> Debug (dumps stack and registers)

___

Sample Program
---

### Hello World
prints "Hello world!"
```
AS_E__LY  //-1 + sp
A_S_____  //jmp to mem[sp]
AS_E__LY
A_S_____
AS_E__LY
A_S_____
_SS_MBLY //move space to r1
AS_E___Y //+1 to sp
_SS_MB__ //move r1 to mem[sp]
AS_E__LY //-1 to sp
AS_E__LY
A_S_____
AS_E__LY
A_S_____
AS_E__LY
A_S_____
AS_E__LY
A_S_____
ASS___L_
__SE_BL_ //prints H
AS_E__LY
A_S_____
AS_E__LY
A_S_____
AS_E__LY
A_S_____
ASS___LY
__SE_BL_ //prints e
_SSEM_LY //move d to r1
AS_E__LY //2 + sp
_S_EMB__ //move d to mem[sp]
AS_E__LY //-1 + sp
AS_E__LY //-1 + sp
_SS___L_
_SS___L_
_SS___L_
_SS____Y
__SE_BL_ //print l
__SE_BL_ //print l
_SS___L_ //+3 to mem[sp]
_SS____Y
__SE_BL_ //print o
_SSEM___ //move o to r1
AS_E___Y //add 1 to sp
__SE_BL_ //print space
AS_E__LY //2 + sp
_S_EMB__ //move o to mem[sp]
_S_E____ //0 to sp
A_S_____ //add 20
ASS___LY //-1 + mem[sp]
A_S_____
ASS___LY //-1 + mem[sp]
__SE_BL_ //print w
AS_E___Y //add 1 to sp
AS_E___Y //add 1 to sp
AS_E___Y //add 1 to sp
__SE_BL_ //print o
_SS___L_
_SS____Y
__SE_BL_ //print r
_SS___LY
_SS___LY
_SS___LY
_SS___LY
_SS___LY
_SS___LY
__SE_BL_ //print l
_S_S__L_ //move 2 to sp
__SE_BL_ //print d
_S_S___Y
ASS____Y
__SE_BL_ //print !
_______Y //EXIT
________ //ADD 10 to mem[sp]
AS_E___Y
_SS___LY  
_SS___LY
_SS___LY
_SS___LY
_SS___LY
A_SE____
```
