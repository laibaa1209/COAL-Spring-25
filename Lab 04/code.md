# Lab 04

## Question 02:
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

## Question 03:
```asm
include irvine32.inc

.data
	varB BYTE +10
	varW WORD -150
	varD DWORD 600
.code
main PROC
	MOVZX EAX, varB
	MOVSX EBX, varW
	MOV ECX, varD
	exit
main endp
end main
```

## Question 4
### part 1:
```asm
include irvine32.inc

.code
main PROC
	MOV AX, 89
	
	ADD AX, 75h
	ADD AX, 1101b

	SUB AX, 46q
	SUB AX, 28

	MOVZX EAX, AX
	call WriteInt
	exit
main endp
end main
```

### part 2:
```asm
include irvine32.inc

.data
	Val1 DWORD 25h
	Val2 BYTE 36o
	Val3 WORD 20d

.code
main PROC
	MOV EAX, Val1 
	MOVZX EBX, Val2

	ADD EAX, EBX
	SUB EAX, 654h
	
	MOVZX EBX, Val3

	ADD EAX, EBX

	call WriteInt
	exit
main endp
end main
```
