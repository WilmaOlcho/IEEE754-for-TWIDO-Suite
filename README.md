# IEEE754-for-TWIDO-Suite
When your PLC does not support foating point numbers, you can force it to calculate them.

This code can be imported in TWIDO Suite, it converts DWORD values into IEEE754 floating point single precision format in subrountine.
It can also adding, substracting, multiplying and dividing these values, it is possible to convert IEEE754 back into DWORD and enyoy calculated value.

This program uses memmory addresses described below:
MD984 as input A
MD986 as output
MD988 as input B
MD990 - MD1010 as internal variables
S17 as ALU carrying bit
M250 - M255 as internal bit settings
SR1 as converting DWORD into IEEE754 subrountine
SR2 as converting IEEE754 into DWORD subrountine
SR3 as Multiplication IEEE754 subrountine
SR4 as Addition and Substraction IEEE754 subrountine
SR5 as Dividion IEEE754 subrountine
L5,6,10,11,14,15,16,17,18,20,21,22,23,24,30,31,32 labels for internal loops

DWORD values are 2's complement signed integers
Adding negative numbers into values causes substraction

Examples:
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

