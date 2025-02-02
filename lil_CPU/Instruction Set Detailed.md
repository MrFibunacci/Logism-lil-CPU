\[] = 1 Byte

# Data Transfer
## MOV immediate to register
Description: Store a value directly into a selected register from opcode.

Binary: `[0000 0001] [W000 0reg] [data if W=1] [data]`
- reg is 3 bits for selection of [[Registers]]

Example: 
- Save 44 decimal into the [[Registers]]
- 00000001 00000101 00000000 00101100
- 01 05 00 2Ch
## MOV register to register
Description: Copy values from one register to another.

Binary: `[0000 0010] [W d reg1 reg2] [] []`
- reg =  3 bits for selection of [[Registers]]
- d = 0 from `reg1` to `reg2` 
- d = 1 from `reg2` to `reg1`
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

Binary: `[0010 0001] [WSrc0 0Res] [0000 0A] [0000 0B]`

- Res is a 3-Bit number defining what register the result should be saved to. Only relevant if Src is = 00 value will be ignored otherwise.
- A is a 3-Bit number defining the A value source register
- B is a 3-Bit number defining the B value source register
- Src is a 2-Bit number defining where the result should be saved. Encoded as below.
    - 00 = Register (uses Res to define what register precisely)
    - 01 = Stack (just “pops” the result to Stack)
    - 10 = Memory (will save result to whatever address is saved in BP register)

## IADD Integer Add

Description: Acts same as ADD except signed

Binary: `[0010 0010] [WSrc0 0Res] [0000 0A] [0000 0B]`