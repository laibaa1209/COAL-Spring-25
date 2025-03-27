# Lab 07:

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
