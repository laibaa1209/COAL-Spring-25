## Question 01:
### code:
```asm
include Irvine32.inc

.data
    Str1 BYTE '127&j~3#^&*#*#45^', 0

.code
main PROC
    mov esi, OFFSET Str1
    call Scan_String
    call WriteInt
    call Crlf
    call ExitProcess
main ENDP

Scan_String PROC
    mov ecx, 0

Scan_Loop:
    mov al, [esi]
    cmp al, 0
    je Not_Found
    cmp al, '#'
    je Found
    inc esi
    inc ecx
    jmp Scan_Loop

Found:
    mov eax, ecx
    ret

Not_Found:
    mov eax, -1
    ret
Scan_String ENDP

END main

```
### output:
![image](https://github.com/user-attachments/assets/733cc0f2-4596-4150-b47f-2bda29791b77)

## Question 02:
### code:
```asm
include Irvine32.inc

.data
    Str1 BYTE '127&j~3#^&*#*#45^', 0
    prompt1 BYTE "Enter a character to search: ", 0
    char BYTE ?

.code
main PROC
    mov edx, OFFSET prompt1
    call WriteString
    call ReadChar
    mov char, al
    call WriteChar
    call Crlf
    
    push OFFSET Str1
    push eax
    call Scan_String
    
    call WriteInt
    call Crlf
    
    call ExitProcess
main ENDP

Scan_String PROC
    push ebp
    mov ebp, esp
    push esi
    push ecx
    
    mov esi, [ebp+12]
    mov al, [ebp+8]
    mov ecx, 0
    
Scan_Loop:
    mov dl, [esi]
    cmp dl, 0
    je Not_Found
    cmp dl, al
    je Found
    inc esi
    inc ecx
    jmp Scan_Loop
    
Found:
    mov eax, ecx
    jmp Done
    
Not_Found:
    mov eax, -1
    
Done:
    pop ecx
    pop esi
    pop ebp
    ret 8
Scan_String ENDP

END main
```
### output:
![image](https://github.com/user-attachments/assets/00cdecc5-72c7-40a3-925d-6872a23dd107)

## Question 03:
### code:
```asm
include Irvine32.inc

.data
    Str1 BYTE "Hello", 0
    Str2 BYTE "Hello", 0
    Str3 BYTE "World", 0
    comparingMsg BYTE "Comparing: '", 0
    toMsg BYTE "' to '", 0
    equalMsg BYTE "' - Equal", 0
    notEqualMsg BYTE "' - Not Equal", 0
    newline BYTE 0dh, 0ah, 0

.code
main PROC
    ; Compare Str1 and Str2
    mov edx, OFFSET comparingMsg
    call WriteString
    mov edx, OFFSET Str1
    call WriteString
    mov edx, OFFSET toMsg
    call WriteString
    mov edx, OFFSET Str2
    call WriteString
    
    push OFFSET Str1
    push OFFSET Str2
    call IsCompare
    call DisplayResult
    
    ; Compare Str1 and Str3
    mov edx, OFFSET comparingMsg
    call WriteString
    mov edx, OFFSET Str1
    call WriteString
    mov edx, OFFSET toMsg
    call WriteString
    mov edx, OFFSET Str3
    call WriteString
    
    push OFFSET Str1
    push OFFSET Str3
    call IsCompare
    call DisplayResult
    
    call ExitProcess
main ENDP

IsCompare PROC
    push ebp
    mov ebp, esp
    push esi
    push edi
    
    mov esi, [ebp+12]
    mov edi, [ebp+8]
    
CompareLoop:
    mov al, [esi]
    mov bl, [edi]
    cmp al, bl
    jne NotEqual
    cmp al, 0
    je Equal
    inc esi
    inc edi
    jmp CompareLoop
    
Equal:
    mov eax, 1
    jmp Done
    
NotEqual:
    mov eax, 0
    
Done:
    pop edi
    pop esi
    pop ebp
    ret 8
IsCompare ENDP

DisplayResult PROC
    cmp eax, 1
    je ShowEqual
    mov edx, OFFSET notEqualMsg
    jmp PrintMsg
ShowEqual:
    mov edx, OFFSET equalMsg
PrintMsg:
    call WriteString
    mov edx, OFFSET newline
    call WriteString
    ret
DisplayResult ENDP

END main
```
### output:
![image](https://github.com/user-attachments/assets/c18415bd-c1a8-4191-8edc-2b632eda20f5)

## Question 04:
### code:
```asm
include Irvine32.inc

.data
    str1 BYTE "Hello World!", 0
    beforeMsg BYTE "Before reverse: ", 0
    afterMsg BYTE "After reverse:  ", 0
    newline BYTE 0dh, 0ah, 0

.code
main PROC
    ; Display original string
    mov edx, OFFSET beforeMsg
    call WriteString
    mov edx, OFFSET str1
    call WriteString
    mov edx, OFFSET newline
    call WriteString

    ; Reverse the string
    push OFFSET str1
    call Str_Reverse

    ; Display reversed string
    mov edx, OFFSET afterMsg
    call WriteString
    mov edx, OFFSET str1
    call WriteString
    mov edx, OFFSET newline
    call WriteString

    call ExitProcess
main ENDP

Str_Reverse PROC
    ; Input: Address of null-terminated string on stack
    push ebp
    mov ebp, esp
    push esi        ; Start pointer
    push edi        ; End pointer
    push eax        ; Temp for character swap
    push ebx        ; Temp for character swap

    mov esi, [ebp+8]    ; Get string address (start)
    mov edi, esi        ; Copy to find end

    ; Find end of string
FindEnd:
    mov al, [edi]
    cmp al, 0
    je  FoundEnd
    inc edi
    jmp FindEnd

FoundEnd:
    dec edi        ; Point to last character before null

    ; Swap characters from both ends
SwapLoop:
    cmp esi, edi    ; Check if pointers have met/crossed
    jge Done

    ; Swap [esi] and [edi]
    mov al, [esi]
    mov bl, [edi]
    mov [esi], bl
    mov [edi], al

    ; Move pointers
    inc esi
    dec edi
    jmp SwapLoop

Done:
    pop ebx
    pop eax
    pop edi
    pop esi
    pop ebp
    ret 4        ; Clean up 1 parameter (4 bytes)
Str_Reverse ENDP

END main
```
### output:
![image](https://github.com/user-attachments/assets/7c0394a4-643b-43a3-b552-e7885073cfe2)

## Question 05:
### code:
```asm
include Irvine32.inc

.data
    array DWORD 10, 20, 30, 40, 50  ; Sample array
    arraySize = ($ - array) / TYPE array
    beforeMsg BYTE "Original array: ",0
    afterMsg BYTE "Modified array: ",0
    space BYTE " ",0

.code
main PROC
    ; Display original array
    mov edx, OFFSET beforeMsg
    call WriteString
    mov ecx, arraySize
    mov esi, OFFSET array
    call DisplayArray
    call Crlf

    ; Call Load procedure
    push OFFSET array
    push arraySize
    call Load

    ; Display modified array
    mov edx, OFFSET afterMsg
    call WriteString
    mov ecx, arraySize
    mov esi, OFFSET array
    call DisplayArray
    call Crlf

    call ExitProcess
main ENDP

; Procedure to load and modify array
; Parameters:
;   [ebp+12] = offset of array
;   [ebp+8]  = number of elements (byte count)
Load PROC
    push ebp
    mov ebp, esp
    push esi        ; Array pointer
    push ecx        ; Loop counter
    push eax        ; Current element
    push ebx        ; Index

    mov esi, [ebp+12]   ; Array offset
    mov ecx, [ebp+8]    ; Number of elements
    mov ebx, 0          ; Start index at 0

ProcessArray:
    cmp ebx, ecx        ; Check if we've processed all elements
    jge Done

    ; Multiply current element by its index
    mov eax, [esi + ebx*4]  ; Get array element (DWORD = 4 bytes)
    imul eax, ebx           ; Multiply by index
    mov [esi + ebx*4], eax  ; Store back in array

    inc ebx                 ; Increment index
    jmp ProcessArray

Done:
    pop ebx
    pop eax
    pop ecx
    pop esi
    pop ebp
    ret 8       ; Clean up 8 bytes of parameters (2 DWORDs)
Load ENDP

; Helper procedure to display array
; Input: ESI = array offset, ECX = count
DisplayArray PROC
    push eax        ; Save registers
    push edx

DisplayLoop:
    mov eax, [esi]
    call WriteInt
    mov edx, OFFSET space
    call WriteString
    add esi, 4      ; Move to next DWORD
    loop DisplayLoop

    pop edx         ; Restore registers
    pop eax
    ret
DisplayArray ENDP

END main
```
### output:
![image](https://github.com/user-attachments/assets/cd54faaf-93ff-42d9-b940-7639ae235424)
