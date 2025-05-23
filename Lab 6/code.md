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
include irvine32.inc

.data
    write_id byte "Enter Employee ID: ", 0
    id DWORD 5 dup (?)  

    write_name byte "Enter the name of Employee: ", 0
    e_name byte 5 * 8 dup (?)  

    write_birthyear byte "Enter Birth Year: ", 0
    birth_year DWORD 5 dup (?)

    write_salary byte "Enter annual salary: ", 0
    annual_salary DWORD 5 dup(?)

    prompt byte "The total annual salary is: ", 0


.code
main proc
    mov esi, 0
    mov ecx, 5  

credentials:
    mov ebx, ecx  

    mov edx, offset write_id
    call writestring
    call ReadInt
    mov id[esi*4], eax  

    mov edx, offset write_name
    call writestring

    mov edx, offset e_name
    mov edi, esi
    imul edi, 8
    add edx, edi
    mov ecx, 8
    call readstring

    mov edx, offset write_birthyear
    call writestring
    call readint
    mov birth_year[esi*4], eax

    mov edx, offset write_salary
    call writestring
    call readint
    mov annual_salary[esi*4], eax


    inc esi

    mov ecx, ebx
    loop credentials

    mov ecx, 5
    mov esi, 0

print:
    mov ebx, ecx

    mov eax, 32
    call writechar

    mov eax, id[esi*4]  
    call writedec      

    mov eax, 32
    call writechar

    mov edx, offset e_name
    mov edi, esi
    imul edi, 8
    add edx, edi
    mov ecx, 8
    call writestring

    mov eax, 32
    call writechar

    mov eax, birth_year[esi*4]
    call writedec

    mov eax, 32
    call writechar

    mov eax, annual_salary[esi*4]
    call writedec

    call crlf

    inc esi

    mov ecx, ebx
    loop print

    mov eax, 0
    mov esi,0
    mov ecx, lengthof annual_salary
    cumulative:
        add eax, annual_salary[esi*4]
        inc esi

    loop cumulative

    mov edx, offset prompt
    call writestring
    call writedec
    exit

main endp
end main

```

## output:
![image](https://github.com/user-attachments/assets/725390d1-f509-43fd-9609-45bc583ee795)


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
## output:
![image](https://github.com/user-attachments/assets/f9e33623-264c-4ecd-a934-33cd2efa1b7a)
