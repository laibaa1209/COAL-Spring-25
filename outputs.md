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
