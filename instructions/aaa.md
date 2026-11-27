# AAA - ASCII Adjust after Addition

## Description

In unpacked [BCD](../topics/bcd.md) mode (also called ASCII BCD), each decimal digit is stored in a separate byte. After addition with another unpacked BCD value, the AAA instruction corrects the values in AH and AL so that the result is again in unpacked BCD format.

## Operands

None.

## Affected Flags and Registers

Flag | Effect
-----|------
CF   | set if the high byte had to be adjusted
ZF   | (undefined)
SF   | (undefined)
OF   | (undefined)
PF   | (undefined)
AF   | set if the high byte had to be adjusted

- The high nibble (i.e. bits 4-7) of AL is cleared.

## Example

Calculating 28 + 13:

```nasm
MOV  AX, 0x0208  ; puts decimal 28 in unpacked BCD in AX
ADD  AX, 0x0103  ; adds decimal 13 to 28, AX is now 0x030B
AAA              ; AX is now 0x0401 to represent decimal 41
```
