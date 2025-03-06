# Lab 05

## Question 01:
```asm
include irvine32.inc

.data
	arrB BYTE 61,43,11,52,25
	newarrB BYTE 5 dup(?)
.code
main proc
	mov esi, offset newarrB

	mov AL, arrB[2]
	mov [esi], AL
	INC esi

	mov AL, arrB[4]
	mov [esi], AL
	INC esi

	mov AL, arrB[1]
	mov [esi], AL
	INC esi

	mov AL, arrB[3]
	mov [esi], AL
	INC esi

	mov AL, arrB[0]
	mov [esi], AL
	
	mov esi, offset newarrB
	mov ecx, lengthof newarrB
	l: 
		movzx eax, BYTE ptr [esi]
		call writeint
		call crlf
		INC esi

	loop l
	
	exit
main endp
end main
```

## Question 02:
```asm
include irvine32.inc

.data
	arrayB BYTE 10, 20, 30 
	arrayW WORD 150, 250, 350 
	arrayD DWORD 600, 1200, 1800
	SUM1 DWORD ?
	SUM2 DWORD ?
	SUM3 DWORD ?
.code
main PROC
	MOVZX EAX, arrayB[0]
	MOVZX EBX, arrayW[0]
	ADD EAX, EBX
	ADD EAX, arrayD[0]
	MOV SUM1, EAX
	call writeint
	call crlf

	MOVZX EAX, arrayB[1]
	MOVZX EBX, arrayW[2]
	ADD EAX, EBX
	ADD EAX, arrayD[4]
	MOV SUM2, EAX
	call writeint
	call crlf

	MOVZX EAX, arrayB[2]
	MOVZX EBX, arrayW[4]
	ADD EAX, EBX
	ADD EAX, arrayD[8]
	MOV SUM1, EAX
	call writeint
	call crlf

exit
main endp
end main
```

## Question 03:
```asm
include irvine32.inc

.data
	array1 BYTE 10, 20, 30, 40
	array2 BYTE 4 DUP (?)
.code
main PROC
	MOV ESI, offset array1+3
	MOV EDI, offset array2

	MOV AL, [ESI]
	DEC ESI
	MOV [EDI], AL
	INC EDI

	MOV AL, [ESI]
	DEC ESI
	MOV [EDI], AL
	INC EDI
	
	MOV AL, [ESI]
	DEC ESI
	MOV [EDI], AL
	INC EDI

	MOV AL, [ESI]
	MOV [EDI], AL

	mov esi, offset array2
	mov ecx, lengthof array2
	l: 
		movzx eax, BYTE ptr [esi]
		call writeint
		call crlf
		INC esi

	loop l
exit
main endp
end main
```
