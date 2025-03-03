# Lab 04

## Question 01:
```asm
include irvine32.inc

.code
main PROC
	MOV AL, 'L'
	MOV BL, 'A'
	MOV CL, 'I'

	call DumpRegs
	call crlf

	MOVZX EAX, AL
	call writeHex
	call crlf

	MOVZX EAX, BL
	call writeHex
	call crlf

	MOVZX EAX, CL
	call writeHex
	call crlf

	exit
main endp
end main

```
