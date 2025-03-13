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
include Irvine32.inc

.code
main proc
    mov eax,1
    mov ebx,1
    mov ecx,5
    pattern:
    
    mov edx, ecx
    mov ecx,ebx
    innerloop:
    mov eax,1
     call writedec
    loop innerloop
        
        call crlf
    inc ebx
    mov ecx, edx
    loop pattern


    exit               

main endp
end main
```

### pt 2
```asm
include Irvine32.inc

.code
main proc
    mov eax,1
    mov ecx, 4

    pattern:
        mov edx, ecx
        
        print_num:
            call writeint
            dec edx
            jnz print_num
            call crlf

    loop pattern


    exit               

main endp
end main

```
