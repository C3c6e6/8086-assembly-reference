# AAD - ASCII Adjust before Division

## Description

In unpacked [BCD](../topics/bcd.md) mode (also called ASCII BCD), each decimal digit is stored in a separate byte. The AAD instruction converts an unpacked BCD value stored in AH and AL into a single binary value in AL. Its counterpart, [AAM](aam.md) (ASCII Adjust after Multiplication) does the opposite, i.e. converting a single binary value into an unpacked BCD value. While the names of both instructions suggest they need to be called respectively before division and after multiplication, they can actually be used as general-purpose conversion instructions. 

## Operands

None.

## Affected Flags and Registers

Flag | Effect
-----|------
CF   | (undefined)
ZF   | 1 if the result in AL is zero, 0 otherwise
SF   | Can only be 0 with valid inputs.
OF   | (undefined)
PF   | reflects the parity of the result in AL.
AF   | (undefined)

- AL contains the result in binary format
- AH is set to 0x00

## Example

Divide 84 by 7:

```nasm
MOV  AX,0804  ; puts decimal 84 in unpacked BCD format in AX
MOV  BL,07    ; put the divisor in BL
AAD  0A       ; convert to binary format: AH is 0, AL is 0x54 (84)
DIV  BL       ; divide by 7, AL is now 0x0C (12), AH is 0 (remainder is 0)
AAM  0A       ; convert the quotient back to BCD, AX is now 0x0102
```
