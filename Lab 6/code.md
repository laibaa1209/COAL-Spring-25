# Lab 06

## Question 01:
```asm
include irvine32.inc

.code
main proc
	mov edx, 0
	mov ecx, 10
	mov ebx, 1

	fibonacci:
		mov eax, edx
		call WriteDec
		call crlf
		
		add edx, ebx
		xchg edx, ebx
	
	loop fibonacci
	exit

main endp
end main
```
## Output:
![image](https://github.com/user-attachments/assets/50b36bf8-e234-4bd7-9448-5eabc7d7534f)


## Question 02:

### pt 1
```asm
include irvine32.inc

.code
main proc
	mov eax, 1
	mov ebx, 1
	mov ecx, 4

	outter_pattern:
		mov edx, ecx
		mov ecx, ebx
		inc ebx

		inner_pattern:
			call writedec
		loop inner_pattern

	call crlf
	mov ecx, edx

	loop outter_pattern

exit
main endp
end main
```
## Output:
![image](https://github.com/user-attachments/assets/ae267d0e-a389-4ccc-ad77-cf9a70cbd073)


### pt 2
```asm
include irvine32.inc

.code
main proc
	mov eax, 1
	mov ebx, 4
	mov ecx, 4

	outter_pattern:
		mov edx, ecx
		mov ecx, ebx
		dec ebx

		inner_pattern:
			call writedec
		loop inner_pattern

	call crlf
	mov ecx, edx

	loop outter_pattern

exit
main endp
end main

```
## Output
![image](https://github.com/user-attachments/assets/6c7a0157-c93c-47a3-8690-564a0af78c94)

### pt 3
```asm
include irvine32.inc

.code
main proc
	mov ebx, 4
	mov ecx, 4

	outter_pattern:
		mov eax, 4
		mov edx, ecx
		mov ecx, ebx
		dec ebx

		inner_pattern:
			call writedec
			dec eax
		loop inner_pattern

	call crlf
	mov ecx, edx

	loop outter_pattern

exit
main endp
end main
```

## ouput
![image](https://github.com/user-attachments/assets/d30d2022-dddf-49b6-9bca-124f7b6a4537)

### pt 4
```asm
include irvine32.inc

.code
main proc
	mov ebx, 4
	mov ecx, 4

	outter_pattern:
		mov eax, 1
		mov edx, ecx
		mov ecx, ebx
		dec ebx

		inner_pattern:
			call writedec
			inc eax
		loop inner_pattern

	call crlf
	mov ecx, edx

	loop outter_pattern

exit
main endp
end main
```
## output
![image](https://github.com/user-attachments/assets/804722ed-a906-46bb-9d02-ecfa90cdbe0f)

## Question 03:
```asm

```

## output:

## Question 04:
```asm
include irvine32.inc

.data
	source byte "Gotta copy this string",0
	target byte 22 dup (?)

.code
main proc
	mov esi, 0
	mov edi, 0
	mov ecx, 22
	
	transfer:
		mov al, source[esi]
		mov target[edi], al
	
		inc esi
		inc edi
	loop transfer

	mov edx, offset target
	call writestring

	exit

main endp
end main
```

## output:
![image](https://github.com/user-attachments/assets/dea0d5eb-3595-4954-92be-d221d9c068fc)

## Question 05:
```asm
include irvine32.inc

.data
	arr word 1, 2, 3, 4, 5, 6, 7, 8, 9

.code
main proc
	mov esi, offset arr
	mov edi, offset arr + sizeof arr - 2
	mov ecx, lengthof arr/2
	
	transfer:
		mov ax, [esi]
		xchg ax, [edi]
		mov [esi], ax
	
		add esi, 2
		sub edi, 2
	loop transfer

	mov ecx, 9
	mov esi, offset arr

	print:
		mov ax, [esi]
		movzx eax, ax
		call writedec

		mov al, ' '
		call writechar
		
		add esi, 2

	loop print
	exit

main endp
end main
```

## output:
![image](https://github.com/user-attachments/assets/d6ab3a44-b213-4568-a047-a2375dfae156)


## Question 06:
```asm
include irvine32.inc

.data
	write_id byte "Enter Employee ID: "
	id word 5 dup (?)

	write_name byte "Enter the name of Employee: "
	e_name byte 5 * 8 dup (?)

.code
main proc
	mov esi, 0
	mov ecx, 5

	credentials:
		mov edx, offset write_id
		call writestring
		call ReadInt
		mov id[esi], ax

		mov edx, offset write_name
		call writestring

		mov edx, offset e_name
		call ReadString
		

		add esi, 2

	loop credentials

	mov ecx, 5
	mov esi, offset id

	print:
		mov ax, [esi]
		movzx eax, ax
		call writedec

		mov al, ' '
		call writechar

		; Print Employee Name
		mov edx, offset e_name
		add edx, esi * 8     
		call writestring

		call crlf            
		
		add esi, 2

	loop print

	exit

main endp
end main
```
## output:
