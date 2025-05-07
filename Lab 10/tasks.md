## Question 01:
### code:
```asm
include irvine32.inc

.data
	var1 dword 3
	var2 dword 4
	var3 dword 5
.code
main PROC
	push var3
	push var2
	push var1
	call ThreeProd

	exit
main endp

ThreeProd Proc
	push ebp
	mov ebp, esp
	mov eax, [ebp + 16]
	mov ebx, [ebp + 12]
	mov ecx, [ebp + 8]

	xor edx, edx
	mul ebx ;eax=eax*ebx

	xor edx, edx
	mul ecx ;eax=eax*ecx

	call writedec
	pop ebp
ThreeProd endp

end main
```
### output:
![image](https://github.com/user-attachments/assets/9d0bcbe8-113f-4574-8db1-d8d999768dc1)

## Question 02:
### code:
```asm
include irvine32.inc

.data
    arr dword 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
.code
main PROC
    push offset arr
    call MinMax
    exit
main endp

MinMax Proc
    push ebp
    mov ebp, esp
    sub esp, 8          ; make space for 2 local variables 
    
    mov esi, [ebp + 8]  ; esi = offset arr
    
    ; find max value
    mov ecx, 9          
    mov eax, [esi]      
    mov [ebp-4], eax    ; max = first element

    find_max:
        add esi, 4
        mov eax, [esi]
        cmp eax, [ebp-4]
        jle skip_max
        mov [ebp-4], eax    ; update max
    skip_max:
        loop find_max

    mov eax, [ebp-4]
    call WriteDec       ; eax=max value
    call Crlf
    
    ; find min value
    mov ecx, 9        
    mov esi, [ebp+8]    
    mov eax, [esi]      
    mov [ebp-8], eax    ; min = first element
    
    find_min:
        add esi, 4
        mov eax, [esi]
        cmp eax, [ebp-8]
        jge skip_min
        mov [ebp-8], eax    ; update min
    skip_min:
        loop find_min

    mov eax, [ebp-8]
    call WriteDec       ; eax=min value
    call Crlf
    
    mov esp, ebp        ; restore stack pointer
    pop ebp
    ret 4               ; clean up the parameter from stack
MinMax endp

end main
```
### output:
![image](https://github.com/user-attachments/assets/11fe153d-00f6-4722-8a8c-7761c06b5dc2)

## Question 03:
### code:
```asm

```
### output:
![image](https://github.com/user-attachments/assets/25a5d051-bd4a-4939-9b02-2de8af5d9492)


## Question 04:
### code:
```asm
include Irvine32.inc

.data
    prompt1 BYTE "Enter four numbers: ",0
    notAllPrimeMsg BYTE "Not all numbers are prime",0
    largestPrimeMsg BYTE "The largest prime is: ",0
    num1 dword ?
    num2 dword ?
    num3 dword ?
    num4 dword ?
    allPrimeFlag byte 1  ; 1 = true, 0 = false

.code
main PROC
    ; Get input numbers
    mov edx, OFFSET prompt1
    call WriteString

    call ReadInt
    mov num1, eax
    call ReadInt
    mov num2, eax
    call ReadInt
    mov num3, eax
    call ReadInt
    mov num4, eax

    ; Push numbers onto stack in reverse order
    push num4
    push num3
    push num2
    push num1

    call CheckPrime
    cmp allPrimeFlag, 1
    jne NotAllPrime

    ; If all are prime, find largest
    push num4
    push num3
    push num2
    push num1
    call LargestPrime
    jmp Done

NotAllPrime:
    mov edx, OFFSET notAllPrimeMsg
    call WriteString
    call Crlf

Done:
    exit
main ENDP

CheckPrime PROC
    push ebp
    mov ebp, esp
    pushad  ; Save all registers

    ; Check each number
    mov esi, 8  ; Start at [ebp+8] (num1)
    mov ecx, 4  ; 4 numbers to check

CheckLoop:
    mov eax, [ebp+esi]
    call IsPrime
    cmp al, 0
    je NotPrimeFound
    add esi, 4  ; Move to next number
    loop CheckLoop
    jmp AllPrime

NotPrimeFound:
    mov allPrimeFlag, 0

AllPrime:
    popad
    pop ebp
    ret 16  ; Clean up 4 pushed numbers
CheckPrime ENDP

IsPrime PROC
    ; Input: EAX = number to check
    ; Output: AL = 1 if prime, 0 if not prime
    cmp eax, 1
    jle NotPrime  ; Numbers <= 1 are not prime

    mov ebx, 2    ; Start divisor at 2
    mov edi, eax  ; Save original number
    shr eax, 1    ; Only need to check up to sqrt(n), so n/2 is safe
    inc eax       ; To be sure we cover it

PrimeCheckLoop:
    cmp ebx, eax
    jae IsPrimeNum
    mov edx, 0
    mov eax, edi
    div ebx
    cmp edx, 0
    je NotPrime
    inc ebx
    mov eax, edi  ; Restore original number
    jmp PrimeCheckLoop

IsPrimeNum:
    mov al, 1
    ret

NotPrime:
    mov al, 0
    ret
IsPrime ENDP

LargestPrime PROC
    push ebp
    mov ebp, esp
    pushad

    ; Initialize with first number
    mov eax, [ebp+8]  ; num1
    mov ebx, eax      ; ebx will hold largest

    ; Compare with num2
    mov eax, [ebp+12]
    cmp eax, ebx
    jle CheckNum3
    mov ebx, eax

CheckNum3:
    mov eax, [ebp+16]
    cmp eax, ebx
    jle CheckNum4
    mov ebx, eax

CheckNum4:
    mov eax, [ebp+20]
    cmp eax, ebx
    jle DisplayResult
    mov ebx, eax

DisplayResult:
    mov edx, OFFSET largestPrimeMsg
    call WriteString
    mov eax, ebx
    call WriteDec
    call Crlf

    popad
    pop ebp
    ret 16  ; Clean up 4 pushed numbers
LargestPrime ENDP

END main
```
### output:
![image](https://github.com/user-attachments/assets/b7979745-da2c-4e26-8649-7f5d19cd542b)
![image](https://github.com/user-attachments/assets/6f67297b-68ae-4fa7-9f06-c1f315018244)


## Question 05:
### code:
```asm
include Irvine32.inc

.data
    array DWORD 5, 2, 9, 1, 7, 3, 8, 4, 6, 0   ; Test array
    arraySize DWORD 9         ; Calculate array size
    commaStr BYTE ", ",0

.code
main PROC
    ; Display original array
    mov esi, OFFSET array
    mov ecx, arraySize
    call DisplayArray

    ; Push array size and offset to stack
    push arraySize
    push OFFSET array
    call BubbleSort

    ; Display sorted array
    call Crlf
    mov esi, OFFSET array
    mov ecx, arraySize
    call DisplayArray
    call Crlf

    exit
main ENDP

; BubbleSort Procedure
; Receives: [ebp+8] = offset of array
;           [ebp+12] = size of array
; Returns: nothing (sorts array in place)
BubbleSort PROC
    push ebp
    mov ebp, esp
    pushad                  ; Save all registers

    mov esi, [ebp+8]       ; ESI = array offset
    mov ecx, [ebp+12]      ; ECX = array size
    dec ecx                ; ECX = outer loop counter (n-1)

outerLoop:
    mov edx, ecx           ; EDX = inner loop counter
    mov edi, esi           ; EDI points to first element

innerLoop:
    mov eax, [edi]         ; Load current element
    mov ebx, [edi+4]       ; Load next element
    cmp eax, ebx
    jle noSwap             ; If [edi] <= [edi+4], no swap needed

    ; Swap elements
    mov [edi], ebx
    mov [edi+4], eax

noSwap:
    add edi, 4             ; Move to next element
    dec edx
    jnz innerLoop          ; Continue inner loop

    loop outerLoop         ; Continue outer loop

    popad                  ; Restore registers
    pop ebp
    ret 8                  ; Clean stack (remove 2 parameters)
BubbleSort ENDP

; Helper procedure to display array
; Receives: ESI = array offset
;           ECX = array size
DisplayArray PROC
    pushad
    mov ebx, 0             ; Counter

displayLoop:
    mov eax, [esi + ebx*4]
    call WriteDec
    mov edx, OFFSET commaStr
    call WriteString
    inc ebx
    loop displayLoop

    popad
    ret
DisplayArray ENDP

END main
```
### output:
![image](https://github.com/user-attachments/assets/4799c00e-fbc0-4e86-8074-82b93d9552b5)
