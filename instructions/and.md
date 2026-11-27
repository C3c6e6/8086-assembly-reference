# AND - Bitwise AND


## Description

Performs the logical and between all pairs of bits of two operands. The result is stored in the first operand.

## Operands 

- register, register

```nasm
AND  AL, BL  ; Performs bitwise AND between AL and BL, storing result in AL
```

- register, memory

```nasm
AND  CX, [mask_var]  ; Performs bitwise AND between CX and 16-bit memory variable [mask_var]
```

- memory, register

```nasm
AND  [BX], DX  ; Performs bitwise AND between 16-bit memory location [DS:BX] and DX
```

- register, immediate

```nasm
AND  CX, 0x00FF   ; Masks off upper byte of CX by ANDing with immediate word 0x00FF
```

- memory, immediate

```nasm
AND  BYTE [status], 0x0F; Masks lower nibble of byte variable [status]
```

- accumulator, immediate (Optimized opcode encoding)

```nasm
AND  AL, 0b11011111  ; Converts lowercase ASCII character in AL to uppercase by clearing bit 5
```

## Affected Flags

Flag | Effect
-----|------
CF   | set to 0
ZF   | set if the result is zero
SF   | set if the high bit of the result is 1, i.e. the result can be interpreted as a negative number.
OF   | set to 0
PF   | set to the parity of the result.
AF   | set if the low nybble of the result carries over.

