# AAS - ASCII Adjust after Subtraction

## Description

In unpacked [BCD](../topics/bcd.md) mode (also called ASCII BCD), each decimal digit is stored in a separate byte. After subtracting a single unpacked BCD value from AL, the AAS instruction corrects the values in AH and AL so that the result is again in unpacked BCD format. 

## Operands

None.

## Affected Flags and Registers

Flag | Effect
-----|------
CF   | set to 1 if the high byte had to be adjusted; 0 otherwise
ZF   | (undefined)
SF   | (undefined)
OF   | (undefined)
PF   | (undefined)
AF   | set to 1 if the high byte had to be adjusted; 0 otherwise

- The high nibble (i.e. bits 4-7) of AL is cleared.
* Adjusts AH if the subtraction resulted in a borrow.

## Example

Calculating 31 - 16:

```nasm
MOV  AX,0301  ; Load decimal 31 in unpacked BCD format in AX
SUB  AL,06    ; First subtract the units, AL is now 0xFB
AAS           ; ASCII adjust, AL is now 0x05
SUB  AH,01    ; now subtract the 10s. AX is now 0x0105 i.e. 15 in unpacked BCD
```
