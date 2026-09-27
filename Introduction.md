Lập trình assembly yêu cầu ta thao tác với những thanh ghi của CPU (những thanh ghi có kích thước nhỏ nhưng tốc độ xử lí cực nhanh được tích hợp sẵn trong CPU). Tùy vào kiến trúc của CPU mà sẽ có những thanh ghi thao tác khác nhau

Những thanh ghi được sử dụng trong CPU x86-64
1. General Purpose Registers
- RAX
- RBX
- RCX
- RDX

2. Index Registers
- RSI, RDI
- RBP - Base poitner
- RSP - Stack Pointer

3. Integer Registers
- R8, R9, R10, R11, R12, R13, R14, R15
4. Instruction pointer
- RIP - Instruction pointer -> thanh ghi này sẽ lưu trữ địa chỉ của lệnh tiếp theo mà CPU sẽ thực thi

Mỗi thanh ghi có thể được chia làm nhiều thanh ghi có kích thước nhỏ hơn (`8bit`, `16bit`, `32bit`)

 s. No | 64 bit machine | 32 bit machine | 16 bit machine | 8 bit machine
 ----- | -------------- | -------------- | -------------- | -------------
 1     | RAX            | EAX            | AX             | AL
 2     | RBX            | EBX            | BX             | BL
 3     | RCX            | ECX            | CX             | CL
 4     | RDX            | EDX            | DX             | DL
 5     | RDI            | EDI            | DI             | DIL
 6     | RSI            | ESI            | SI             | SIL
 7     | RBP            | EBP            | BP             | BPL
 8     | RSP            | ESP            | SP             | SPL
 9     | R8             | R8D            | R8W            | R8B
 10    | R9             | R9D            | R9W            | R9B
 11    | R10            | R10D           | R10W           | R10B
 12    | R11            | R11D           | R11W           | R11B
 13    | R12            | R12D           | R12W           | R12B
 14    | R13            | R13D           | R13W           | R13B
 15    | R14            | R14D           | R14W           | R14B
 16    | R15            | R15D           | R15W           | R15B
 17    | RIP            | EIP            | IP             | (Varies)


 ## Viết một chương trình asm theo cú pháp của intel
 Khai báo các tiên xử lý như sau

Ví dụ
 ```asm
 // main.s
 .intel_syntax noprefix
 .global _start
 _start:
    mov rdi, 0x0
    mov rax, 60
    syscall
 ```

 Cách biên dịch và liên kết cơ bản
 ~~~
 as main.s -o main.o
 ld main.o -o main
 ~~~