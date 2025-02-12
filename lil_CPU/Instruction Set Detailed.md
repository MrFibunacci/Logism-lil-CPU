\[] = 1 Byte

# Data Transfer
## MOV immediate to register
Description: Store a value directly into a selected register from opcode.

Binary: `[0000 0001] [W000 0reg] [data if W=1] [data]`
- W = word select bit
- reg is 3 bits for selection of [[Registers]]

Example: 
- Save 44 decimal into the [[Registers]]
- 00000001 00000101 00000000 00101100
- 01 05 00 2Ch
## MOV register to register
Description: Copy values from one register to another.

Binary: `[0000 0010] [W d reg1 reg2] [] []`
- W = word select bit
- reg =  3 bits for selection of [[Registers]]
- d = 0 from `reg1` to `reg2` 
- d = 1 from `reg2` to `reg1`

Example: 
- Copy content of AX Register to DX Register
- 00000010 10000011 00000000 00000000
- `02 83 00 00h`

## LOD/STO Memory from/to Register
Description: load or store data to/from memory

Binary: `[0000 0011] [Wd00 0reg] [Address high] [Adress Low]`
- W = word select bit
- reg = 3 bits for selection of [[Registers]]
- d = 0 save from reg to memory 
- d = 1 save to reg from memory
- last to bytes are combined the address to which the data should be stored or loaded
## PUSH from Register
Description: Push a value from a selected register to the [[Stack]]

Binary: `[0000 0100] [W000 0reg] [] []
- W = word select bit
- reg = 3 bits for selection of [[Registers]]
## POP to Register
Description: POP a value from the [[stack]] to a selected register
==TODO: consider moving this instruction together with PUSH like in [[Instruction Set Detailed#LOD/STO Memory from/to Register|LOD/STO]]==

Binary: `[0000 0101] [W000 0reg] [] []
- W = word select bit
- reg = 3 bits for selection of [[Registers]]
## Input from port
Description: 
==TODO: Still gonna need some consideration how many ports we should support==
## Output to port
Description: 
# Arithmetic
## ADD Immediate

Binary: `[00100 0000] [W000 0Reg] [Data if W=1] [Data]`
- Reg is a 3-Bit Number defining which Register the Immediate (Data Bytes) should be calculated with.  
- The calculation is Register + Immediate  
- The result will be stored in the Register defined with Reg.  
- If result goes past 16-Bit Carry flag is set to 1

Example:  
- Add 72 decimal to the AX Register  
- 00100000 10000000 00000000 01001000b  
- 20 80 00 48h
## ADD

Description: Perform Addition (ADD) of two values in registers and saves the result either in another register, the stack or in memory.

Binary: `[0010 0001] [WSrc0 0Reg] [0000 0A] [0000 0B]`

- Reg is a 3-Bit number defining what register the result should be saved to. Only relevant if Src is = 00 value will be ignored otherwise.
- A is a 3-Bit number defining the A value source register
- B is a 3-Bit number defining the B value source register
- Src is a 2-Bit number defining where the result should be saved. Encoded as below.
    - 00 = Register (uses Res to define what register precisely)
    - 01 = Stack (just “pops” the result to Stack)
    - 10 = Memory (will save result to whatever address is saved in BP register)
## IADD Integer Add (Signed)
Description: Acts same as ADD except signed

Binary: `[0010 0010] [WSrc0 0Reg] [0000 0A] [0000 0B]`
## FADD Float Add (Signed)
Binary:`[0010 0011] [] [] []
==TODO: Not sure yet if I will implement floating point numbers. Because I don’t really now how yet but I will leave this in here for now to block the op code number because I would like to keep the individual types of Arithmetic together==

## INC
Description: Increment value of selected Register
Binary: `[0010 0011] [W000 0Reg] [] []
- W word select bit
- Reg is 3-Bit Register Select
## SUB (Unsigned)
Description: Subtract two unsigned values
Binary `[0010 0100] [] [] []
## ISUB Integer Subtract (Signed)
Description: Subtract two signed values
Binary `[0010 0101] [] [] []
## DEC
Description: Decrement value of selected Register
Binary: `[0010 0110] [W000 0Reg] [] []
- W word select bit
- Reg is 3-Bit Register Select
## NEG = change sign
Binary: `[0010 0111] [W000 0Reg] [] []
## MUL = Multiply (Unsigned)
Binary: `[0010 1000] 
## IMUL integer Multiply (Signed)
Binary: `[0010 1001] 
## DIV Divide (Unsigned)
Binary: `[0010 1010] 
## IDIV Integer Divide (Signed)
Binary: `[0010 1011] 
# Logic
## Shift right
Binary: `[0011 0000] 
## Shift left
Binary: `[0011 0001] 
## Rotate right
Binary: `[0011 0010] 
## Rotate left
Binary: `[0011 0011] 
## Rotate through Carry flag left
Binary: `[0011 0100] 
## Rotate through Carry flag right
Binary: `[0011 0101] 
## NOT
Binary: `[0011 0110] 
## AND
Binary: `[0011 0111] 
## NAND
Binary: `[0011 1000] 
## OR
Binary: `[0011 1001] 
## NOR
Binary: `[0011 1010] 
## XOR
Binary: `[0011 1011] 
## XNOR
Binary: `[0011 1100] 
# Control Transfer
## JMP Unconditional Jump
## JE/JZ Jump on Equal/Zero
## JL/JNGE Jump on Less/Not Greater or Equal
## JLE/JNG Jump on Less or Equal/Not Greater
## JB/JNAE Jump on Below/Not Above or Equal
## JBE/JNA Jump on Below or Equal/ Not Above
## JO Jump on Overflow
## JS Jump on Sign
## JNE/JNZ Jump on Not Equal/Not Zero
## JNL/JGE Jump on Not Less/Greater or Equal
## JNLE/JG Jump on Not Less or Equal/Greater
## JNB/JAE Jump on Not Below/Above or Equal
## JNBE/JA Jump on Not Below or Equal/Above
## JNP/JPO Jump on Not Par/Par Odd
## JNO Jump on Not Overflow
## JNS Jump on Not Sign