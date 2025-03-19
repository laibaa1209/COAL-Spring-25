# Lab 06

## Question 01:
```asm
include Irvine32.inc

.code
main proc
    mov ecx, 10       
    mov ebx, 1        
    mov edx, 0         

fibonacci:
    mov eax, edx      
    call WriteInt     
    call Crlf          

    add edx, ebx       
    xchg edx, ebx      

    loop fibonacci     

    exit               

main endp
end main
```

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
