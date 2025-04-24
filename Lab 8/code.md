# Lab 8

## Question 1:
### code:
```asm
include Irivine32.inc

.data
	arr DWORD 4 dup(?)
	prompt byte "Enter the integers: ", 0
	prompt_end "The numbers are not equal", 0

.code
	main PROC

	mov edx, offset prompt
	call writestring
	
	mov ecx, lengthof arr
	mov esi, 0
	input: 
		call readint
		mov arr[esi], eax
		add esi, 4
		loop input

	mov esi, 0
	mov ecx, lengthof arr
	check:
		mov eax, arr[esi]
		cmp eax, arr[esi+4]
		add esi, 4
		JZ check

		mov edx, offset prompt_end
		call writestring

		exit
main endp
end main

```
### output:


## Question 2:
### code:
```asm
include Irivine32.inc

.data
	intArr SWORD 0, 0, 0, 150, 120, 35, -12, 66, 4, 0

.code
	main PROC
	
	mov ecx, lengthof intArr
	mov esi, 0
	
	comparision:
		mov eax, intArr[esi]
		cmp eax, 0
		jz found
		loop comparision

	found:
		mov eax, esi
		call writeint

		exit
main endp
end main

```
### output:


## Question 3:
### code:
```asm
include Irivine32.inc

.data
	var DWORD 5

.code
	main PROC
	
	mov edx, var+1
	mov ecx, 9

	cmp var, ecx
	jae else
	
	cmp ecx, edx
	jb else

	mov eax, 0
	mov x, eax

	else:
		mov eax, 1
		mov x, eax

	mov eax, x
	call writeint

		exit
main endp
end main

```
### output:


## Question 4:
### code:
```asm
include Irivine32.inc

.data
	var DWORD 0
	hello byte "hello", 0
	world byte "world", 0

.code
main PROC
	 
	 while:	
		cmp var, 10
		jbe inner_loop

		exit

	inner_loop:
		cmp var, 5
		jae else

		mov edx, offset hello
		call writestring

		inc var
		jmp while

		else:
			mov edx, offset world
			call writestring

			inc var
			jmp while

main endp
end main

```
### output:


## Question 5:
### code:
```asm
include Irivine32.inc

.data
	arr WORD 10, 4, 7, 14, 299, 156, 3, 19, 29, 300, 20
	value WORD ?
	prompt "Enter the value: ", 0

.code
main PROC
	 
	mov edx, offset prompt
	call writestring

	call readint
	mov value, eax

	mov ecx, lengthof arr
	mov esi, 0
	find_number:
		mov eax, arr[esi]
		cmp eax, value
		jz found

		add esi, 2
		loop find_number

	found:
		mov eax, esi
		call writeint

main endp
end main

```
### output:


## Question 6:
### code:
```asm

```
### output:


## Question 7:
### code:
```asm

```
### output:


## Question 8:
### code:
```asm

```
### output:
