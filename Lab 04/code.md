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

## Question 06:
```asm
include irvine32.inc

.data
	SecondsinDays = 24 * 3600

.code
main PROC
	MOV EAX, SecondsinDays
	
	call WriteInt
	exit
main endp
end main
```

## Question 07:
```asm
include irvine32.inc

.data
	A Word 0FF10h
	B Word 0E10Bh

.code
main PROC
	MOV AX, A
	XCHG AX, B
	MOV A, AX
	
	MOVZX EAX, A
	call WriteHex
	call crlf

	MOVZX EAX, B
	call WriteHex
	call crlf
	
	exit
main endp
end main
```

## Question 08:
```asm
include irvine32.inc

.data
	val1 BYTE 10h
	val2 WORD 8000h
	val3 DWORD 0FFFFh
	val4 WORD 7FFFh

.code
main PROC
	INC val2 ; val2 = 8001h
	
	MOV EAX, 0
	SUB EAX, val3

	MOV AX, val2
	SUB AX, val4
	
	exit
main endp
end main
```
