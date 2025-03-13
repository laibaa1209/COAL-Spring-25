# Lab 06

## Question 01:
```asm
include irvinve32.inc

.code
main proc
	mov ecx, 10
	mov ebx, 1
	mov edx, 0

	fibonacci:
		mov eax, edx
		call writeint
		call crlf

		add edx, ebx
		xchg edx,ebx

	loop fibonacci

	exit

main endp
end main
```
