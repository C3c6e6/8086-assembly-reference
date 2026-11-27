# ADC - Add with Carry

## Description

Adds two values and the value of the carry flag together and stores the result in the first operand. This operation is useful when chaining multiple 16-bit additions together to large numbers stored in 32-bit or larger fields (see the example below).

## Operands 

- register, register:

```nasm
ADC  AX, BX  ; Adds 16-bit register BX + Carry to AX
```

- register, memory:

```nasm
ADC  CX, [SI]  ; Adds 16-bit value from memory [DS:SI] + Carry to CX
```

- memory, register:

```nasm
ADC  [DI], DX  ; Adds 16-bit register DX + Carry to memory location [DS:DI]
```

- register, immediate:

```nasm
ADC  BX, 0x1000  ; Adds immediate constant 1000h + Carry to BX
```

- accumulator, immediate:

```nasm
ADC  AL, 0x05  ; Adds immediate byte 05h + Carry to AL accumulator
```

- memory, immediate:

```nasm
ADC  WORD [count], 100 ; Adds immediate 100 + Carry to 16-bit memory variable 'count'
```

## Affected Flags

Flag | Effect
-----|------
CF   | set if high bit of the result carries over, i.e. the destination is too big to contain the result.
ZF   | set if the result is zero
SF   | set if the high bit of the result is 1, i.e. the result can be interpreted as a negative number.
OF   | set if the result overflows, i.e. if the sign of the stored result is different from the sign of the actual result.
PF   | set to the parity of the result.
AF   | set if the low nybble of the result carries over.

## Example

Adds two 32-bit integers, 0x12345678 and 0x9ABCDEF0, together. The first value is stored in AX:BX, the second in CX:DX

```nasm
MOV  AX,1234  ; High word of the first value
MOV  BX,5678  ; Low word of the first value
MOV  CX,9ABC  ; High word of the second value
MOV  DX,DEF0  ; Low word of the second value
ADD  BX,DX    ; First add the low words together. BX=3568, CF=1
ADC  AX,CX    ; Add the high words together and add the value of CF. AX=ACF1
```
