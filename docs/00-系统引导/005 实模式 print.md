# 实模式 print

- ah: 0x0e
- al: 字符
- int 0x10

```s
[org 0x7c00]

mov ax, 3
int 0x10

mov ax, 0
mov ds, ax
mov es, ax
mov ss, ax
mov sp, 0x7c00

mov si, booting
call print

; 阻塞
jmp $

print:
    mov ah, 0x0e
.next:
    mov al, [si]
    cmp al, 0
    jz .done
    int 0x10
    inc si
    jmp .next
.done:
    ret

booting:
    db "Booting TuringOS...", 10, 13, 0; \n\r

times 510 - ($ - $$) db 0

db 0x55, 0xaa
```
