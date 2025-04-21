# Lab 07:

## Question 01:
```asm
include irvine32.inc

.data
		arr WORD 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
		emptyarr WORD 10 dup(?)

.code
main PROC

	mov esi, 0
	mov ecx, lengthof arr

	pushing_ele:
		mov ax, arr[esi]
		push ax
		add esi, 2
		loop pushing_ele

	mov edi, 0
	mov ecx, lengthof emptyarr

	popping_ele:
		pop ax
		mov emptyarr[edi], ax
		add edi, 2
		loop popping_ele

	mov ecx, lengthof emptyarr
	mov esi, 0

	print_:
		movzx eax, emptyarr[esi]
		call writedec
		add esi, 2
		call crlf
	loop print_
	
	exit

main endp
end main


```

## output:
![image](https://github.com/user-attachments/assets/73738159-c9fc-49a2-917a-49f0a19e8f6e)


## Question 02:
```asm
include irvine32.inc

.data
		var1 dword 20
		var2 dword 30
		var3 dword 40

.code
main PROC

	mov eax, var1
	mov ebx, var2
	mov ecx, var3

	push eax
	push ebx
	push ecx

	pop eax
	pop ebx
	pop ecx

	add eax, ebx
	add eax, ecx

	call writedec
	
	exit

main endp
end main
```

## output:
![image](https://github.com/user-attachments/assets/ef959719-8341-48c6-99f9-0e35a7963721)


## Question 03:
```asm
include irvine32.inc

.data
		arr1 dword 1, 2, 3, 4, 5
		arr2 dword 6, 7, 8, 9, 10

		sum1 dword ?
		sum2 dword ?
		total dword ?

.code

add_sum1 proc
	mov esi, 0
	mov ecx, lengthof arr1
	mov eax, 0

	add_:
		add eax, arr1[esi]
		add esi, 4
		loop add_
		
		mov sum1, eax
		ret 

add_sum1 endp

add_sum2 proc
	mov esi, 0
	mov ecx, lengthof arr2
	mov eax, 0

	add_:
		add eax, arr2[esi]
		add esi, 4
		loop add_
		
		mov sum2, eax
		ret 

add_sum2 endp

total_sum proc
	mov eax, sum1
	add eax, sum2

	mov total, eax
	ret

total_sum endp

main PROC
	call add_sum1
	call add_sum2
	call total_sum

	mov eax, total
	call writedec

	exit

main endp
end main



```

## output:
![image](https://github.com/user-attachments/assets/66f88375-0fc6-4e16-b5c6-5b9e4ac045ff)


## Question 04:
```asm
include irvine32.inc

.data
    var dword 5
.code
main proc
    
    call print_seq
     exit
main endp

print_seq proc
    mov ebx, 5  
    mov ecx, var 
    mov edx, 1  

outter_pattern:
    push ecx       
    mov ecx, ebx  
print_space:
    mov eax, 32    
    call writechar
    loop print_space

    mov ecx, edx    
inner_pattern:
    mov eax, 42     ; ASCII '*'
    call writechar
    loop inner_pattern

    call crlf       
    inc edx         
    dec ebx         

    pop ecx         
    loop outter_pattern

    ret

    print_seq endp

end main

```

## output:
![image](https://github.com/user-attachments/assets/e49b1ffe-c5a9-4b08-a000-08c5d16e941b)

## Question 05:

```asm
include irvine32.inc

.data
    prompt byte "Enter a number n: ", 0
    prompt_sum byte "The sum is: ", 0
    n dword ?

.code
main proc
    call print_sum
    exit
main endp

print_sum proc
    mov edx, offset prompt
    call writestring
    call readint 
    
    mov n, eax
    mov ecx, n  
    mov ebx, 0   

    sum_loop:
        add ebx, ecx  
        loop sum_loop 

    mov edx, offset prompt_sum
    call writestring

    mov eax, ebx  
    call writedec
    call crlf

    ret
print_sum endp

end main

```

## output
![image](https://github.com/user-attachments/assets/9620eed8-b4b1-4cc9-b50b-fe6db0ffbac7)
