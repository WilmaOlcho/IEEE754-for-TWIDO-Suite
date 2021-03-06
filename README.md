# IEEE754-for-TWIDO-Suite
## When your PLC does not support foating point numbers, you can force it to calculate them.

This code can be imported in TWIDO Suite, it converts DWORD values into IEEE754 floating point single precision format in subrountine.
It can also adding, substracting, multiplying and dividing these values, it is possible to convert IEEE754 back into DWORD and enyoy calculated value.

### This program uses memmory addresses described below:
|address|description|
|-----|-------------|
|MD984|input A|
|MD986|output|
|MD988|input B|
|MD990-MD1010|internal variable|
|S17|ALU carrying bit|
|M250-M255|internal bit settings|
|SR1|converting DWORD into IEEE754 subrountine|
|SR2|converting IEEE754 into DWORD subrountine|
|SR3|Multiplication IEEE754 subrountine|
|SR4|Addition and Substraction IEEE754 subrountine|
|SR5|Division IEEE754 subrountine|
|L16-L32| label for internal loop|


## Important information:
 DWORD values are 2's complement signed integers.
 Adding negative numbers into values causes substraction.

## Examples:
```
(*Area of the circle*)
LD 1
[%MD984 := 25] (*or any other value, variable etc. for input A as radius*)
LD 1
SR1 (*Begin conversion DWORD into IEEE754*)
LD 1
[%MD988 := %MD986] (*Store output value in input B*)
[%MD984 := %MD986] (*Copy it to input A too*)
LD 1
SR3 (*Begin multiplication*)
LD 1
[%MD984 := %MD986] (*Store output as input A*)
[%MD988 := #40490FDB] (*Write IEEE754 PI as input B*)
LD 1
SR3 (*Begin multiplication*)
LD 1
[%MD984 := %MD986] (*Copy result as input A*)
LD1
SR2 (*Convert IEEE754 to signed DWORD*)
LD 1
[%MD100 := %MD986%] (*copy result into some variable, use it in program, display on HMI etc.*)
(*Now the %MD100 have value of area of the circle with radius described at first*)
```
