# AAM - ASCII Adjust After Multiplication

## Description

In unpacked [BCD](../topics/bcd.md) mode (also called ASCII BCD), each decimal digit is stored in a separate byte. The AAM instruction converts a single binary value in AL into an unpacked BCD value stored in AH and AL. Its counterpart, [AAD](aad.md) (ASCII Adjust before Division) does the opposite, i.e. converting an unpacked BCD value into a single binary value. While the names of both instructions suggest they need to be called respectively after multiplication and before division, they can actually be used as general-purpose conversion instructions. 

## Operands

None.

## Affected Flags and Registers

Flag | Effect
-----|------
CF   | (undefined)
ZF   | 1 if the result in AL is zero, 0 otherwise
SF   | 0 (barring some exotic conditions)
OF   | (undefined)
PF   | reflects the parity of the result in AL.
AF   | (undefined)

- AL contains value of the lowest decimal digit (units)
- AH contains the value of the highest decimal digit (tens)

## Example

Divide 84 by 7:

```nasm
MOV  AX,0804  ; puts decimal 84 in unpacked BCD format in AX
MOV  BL,07    ; put the divisor in BL
AAD  0A       ; convert to binary format: AH is 0, AL is 0x54 (84)
DIV  BL       ; divide by 7, AL is now 0x0C (12), AH is 0 (remainder is 0)
AAM  0A       ; convert the quotient back to BCD, AX is now 0x0102
