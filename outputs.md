# LAB 03:
### Question 01:
```asm
include irvine32.inc

.data
	val1 SWORD ?
	val2 SBYTE -11
.code
main PROC
	mov EAX, 0
	mov Al, val2
	call writeint

	exit
main ENDP
END main
```

### Question 02:
```asm
include irvine32.inc

.data
	val3 SDWORD -2147483648
.code
main PROC
	mov EAX, val3
	call writeint

	exit
main ENDP
END main
```

### Question 03:
```asm
include irvine32.inc

.data
	val4 WORD 2, 4, 8
```

### Question 04:
```asm
include irvine32.inc

.data
	string BYTE "olive green"0
	A WORD 12
	B WORD 2
	C WORD 13
	D WORD 8
	E WORD 4
```

### Question 05:
```asm
include irvine32.inc

.data
	a DWORD 11h
	b DWORD 10h
	g DWORD 30h
	d DWORD 40h
.code
main PROC
	mov EAX, a
	add EAX, b

	mov ebx, a
	sub ebx, b

	sub eax, ebx

	add eax, g
	add eax, d

	mov ebx, eax

	call WriteInt
	

	exit
main ENDP
END main
```

# Question 06:
```asm
include irvine32.inc

.data

	a DWORD 00010001b
	b DWORD 00010000b
	g DWORD 00110000b
	d DWORD 01000000b
.code
main PROC
	mov EAX, a
	add EAX, b

	mov ebx, a
	sub ebx, b

	sub eax, ebx

	add eax, g
	add eax, d

	mov ebx, eax

	call WriteInt
	

	exit
main ENDP
END main

```

# Question 07:
```asm
include irvine32.inc

.data
	val4 wARRAY 10, 20, 30
```

# Question 08:
```asm
include irvine32.inc

.data
	dArray DWORD 50 dup(?)
```

# Question 09:
```asm
include irvine32.inc

.data
	string BYTE 500 dup("TEST")
```

# Question 10:
```asm
include irvine32.inc

.data
	bArray BYTE 20 dup(0)
```
