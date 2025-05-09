## Tasks 1-5:
### code:
```asm
include Irvine32.inc

.data
    ; Task 1 variables
    task1_msg BYTE "Task 1: EAX * 21 (EAX=5)",0
    task1_eax DWORD 5
    task1_result DWORD ?

    ; Task 2 variables
    task2_msg BYTE "Task 2: Expand -128 in AX to EAX",0
    task2_result DWORD ?

    ; Task 3 variables
    task3_msg BYTE "Task 3: Shift lowest bit of AX to highest bit of BX",0
    task3_ax WORD 0B001h  ; Binary 0000001100000001
    task3_bx WORD 0
    task3_result_bx WORD ?
    task3_shrd_result WORD ?

    ; Task 4 variables
    task4_msg BYTE "Task 4: val1 = (val2 / val3) * (val1 / val2)",0
    val1 SDWORD 20
    val2 SDWORD 5
    val3 SDWORD 2
    task4_result SDWORD ?

    ; Task 5 variables
    task5_msg BYTE "Task 5: 64-bit Addition",0
    num1 QWORD 123456789ABCDEF0h
    num2 QWORD 0FEDCBA9876543210h
    sum QWORD ?

.code
main PROC
    ; Task 1: Multiply EAX by 21
    mov edx, OFFSET task1_msg
    call WriteString
    call Crlf

    mov eax, task1_eax
    mov ebx, eax    ; Save original value
    shl eax, 4      ; EAX * 16
    shl ebx, 2      ; EBX * 4
    add eax, ebx    ; Add (EAX*16 + EAX*4)
    add eax, task1_eax ; Add original EAX
    mov task1_result, eax

    mov edx, OFFSET task1_msg
    call WriteString
    call Crlf
    mov eax, task1_result
    call WriteDec
    call Crlf
    call Crlf

    ; Task 2: Move -128 into AX and expand to EAX
    mov edx, OFFSET task2_msg
    call WriteString
    call Crlf

    mov ax, -128
    movsx eax, ax   ; Sign extend AX to EAX
    mov task2_result, eax

    mov eax, task2_result
    call WriteInt
    call Crlf
    call Crlf

    ; Task 3: Shift lowest bit of AX into highest bit of BX
    mov edx, OFFSET task3_msg
    call WriteString
    call Crlf

    ; Without SHRD
    mov ax, task3_ax
    mov bx, 0
    shr ax, 1       ; Move lowest bit to CF
    rcl bx, 1       ; Rotate CF into highest bit
    mov task3_result_bx, bx

    ; With SHRD
    mov ax, task3_ax
    mov bx, 0
    shrd bx, ax, 1  ; Shift right double
    mov task3_shrd_result, bx

    movzx eax, task3_result_bx
    call WriteBin
    call Crlf
    movzx eax, task3_shrd_result
    call WriteBin
    call Crlf
    call Crlf

    ; Task 4: Implement C++ expression
    mov edx, OFFSET task4_msg
    call WriteString
    call Crlf

    ; val1 = (val2 / val3) * (val1 / val2)
    mov eax, val2
    cdq
    idiv val3       ; EAX = val2 / val3
    mov ebx, eax    ; Save first quotient

    mov eax, val1
    cdq
    idiv val2       ; EAX = val1 / val2

    imul ebx        ; EAX = (val2/val3) * (val1/val2)
    mov task4_result, eax

    mov eax, task4_result
    call WriteInt
    call Crlf
    call Crlf

    ; Task 5: 64-bit Addition
    mov edx, OFFSET task5_msg
    call WriteString
    call Crlf

    ; Push parameters and call Extended_Add
    push OFFSET sum
    push OFFSET num2
    push OFFSET num1
    call Extended_Add

    ; Display results
    mov edx, OFFSET num1
    mov ecx, 2
    call DisplayQword

    mov edx, OFFSET num2
    mov ecx, 2
    call DisplayQword

    mov edx, OFFSET sum
    mov ecx, 2
    call DisplayQword

    call Crlf
    call WaitMsg
    call ExitProcess
main ENDP

; Task 5 Procedure: 64-bit Addition
Extended_Add PROC
    push ebp
    mov ebp, esp
    pushad

    mov esi, [ebp+8]    ; First number
    mov edi, [ebp+12]   ; Second number
    mov ebx, [ebp+16]   ; Result

    ; Add low dwords
    mov eax, [esi]
    add eax, [edi]
    mov [ebx], eax

    ; Add high dwords with carry
    mov eax, [esi+4]
    adc eax, [edi+4]
    mov [ebx+4], eax

    popad
    pop ebp
    ret 12
Extended_Add ENDP

; Helper to display 64-bit numbers
DisplayQword PROC
    mov eax, [edx+4]
    call WriteHex
    mov eax, [edx]
    call WriteHex
    call Crlf
    ret
DisplayQword ENDP

END main
```
### output:
![image](https://github.com/user-attachments/assets/c39483f6-4278-485a-89d5-5a8373fa3626)


