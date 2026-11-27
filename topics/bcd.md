# Binary Coded Decimal mode

In assembly programming, most arithmetic operations are done on binary numbers, where bytes contain all possible values between 0 and 255 (0xFF in hexadecimal). Displaying a numeric value to the user requires in most cases to first convert this number to decimal notation, which is a cumbersome operation. 

To avoid this difficulty, the 8086 allows to perform arithmetic operations directly on decimal numbers. To this end, it encodes numbers into Binary Coded Decimal (BCD) format. In BCD, each decimal digit is stored separately in either the high and low nibble of a single byte or in two separate bytes. The former format is called packed BCD, the latter is called unpacked BCD.

Unpacked BCD is also referred to as ASCII BCD, as it allows to readily convert a digit value (0-9) to its corresponding ASCII character as the characters '0' to '9' have ASCII codes 0x30 to 0x39.

Conversion between binary and ASCII BCD format can be carried out by the [AAD](../instructions/aad.md) (ASCII Adjust before Division) and [AAM](../instructions/aam.md) (ASCII Adjust after Multiplication) instructions. Although their names suggest a close connection to division and multiplication operations, they can actually be used as general purpose conversion instructions.
