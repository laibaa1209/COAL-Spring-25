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
include irvine32.inc

.data
   arr DWORD 8, 5, 1, 2, 6

.code
main proc
    mov ecx, lengthof arr

    outter_loop:
        mov esi, 0
        mov edi, 1
        mov edx, ecx
        mov ecx, lengthof arr -1

        inner_loop:
            mov eax, arr[esi*4]
            cmp eax, arr[edi*4]
            jl no_swap

            xchg eax, arr[edi*4]
            mov arr[esi*4], eax

            no_swap:
            inc esi
            inc edi
            loop inner_loop

            mov ecx, edx
            loop outter_loop

        mov esi, 0
        mov ecx, lengthof arr
        
        print:
            mov eax, arr[esi*4]
            call writedec
            mov eax, 32
            call writechar
            inc esi

            loop print
   
    exit

main endp
end main
```
### output:


## Question 7:
### code:
```asm
include Irivine32.inc

.data
	Monday Byte "Monday", 0
	Tuesday Byte "Tuesday", 0
	Wednesday Byte "Wednesdy", 0
	Thursday Byte "Thursday", 0
	Friday Byte "Friday", 0
	Saturday Byte "Saturday", 0
	Sunday Byte "Sunday", 0
	day byte ?
.code
main PROC

	call readint
	mov day, eax

	cmp day, 1
	jnz day2

	mov edx, offset Monday
	call writestring

	jmp end_prog

	day2:
		cmp day, 2
		jnz day3

		mov edx, offset Tuesday
		call writestring

		jmp end_prog

	day3:
		cmp day 3
		jnz day4

		mov edx, offset Wednesday
		call writestring

		jmp end_prog

	day4:
		cmp day, 4
		jnz day5

		mov edx, offset Thursday
		call writestring

		jmp end_prog

	day5:
		cmp day, 5
		jnz day6

		mov edx, offset Friday
		call writestring

		jmp end_prog

	day6:
		cmp day, 6
		jnz day7

		mov edx, offset Saturday
		call writestring

		jmp end_prog

	day7:
		mov edx, offset Sunday
		call writestring
	 
	exit

main endp
end main

```
### output:


## Question 8:
### code:
```asm
include Irivine32.inc

.data
	inputChar Byte "B"
	isAlpha Byte "It is an alphabet", 0
	notAlpha Byte "It is not an alphabet", 0

.code
main PROC

	movzx eax, inputChar
	cmp al, "A"
	jl check_lower
	cmp eax, "Z"
	jle is_alpha

	check_lower:
		cmp al, "a"
		jl not_alpha
		cmp al, "z"
		jle is_alpha

	not_aplha:
		mov edx, offset notAlpha
		call writestring
		call crlf
		jmp exit_prog
	 
	is_alpha:
    mov edx, offset isAlpha
    call WriteString
    call Crlf

	exit_prog:
		exit

main endp
end main

```
### output:
