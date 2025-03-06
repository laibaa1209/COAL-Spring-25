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
