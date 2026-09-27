Trong kiến trúc x86-84, thanh ghi `rax` được sử dụng cho mục đích chung có độ rộng là 64 bit

Công dụng của thanh ghi rax:
- Nơi chứa giá trị trả về của một hàm 
- Thực hiện các phép tính toán
- Trong linux x86-64, trước khi gọi syscall ta cần phải truyền syscall number tương ứng vào thanh ghi rax

Ví dụ:
```asm
mov rax, 60 ; syscall exit
syscall 
```

Có thể tìm hiểu thêm về các syscall khác ở đây: https://blog.rchapman.org/posts/Linux_System_Call_Table_for_x86_64/

Để ghi dữ liệu vào thanh ghi ta sẽ dùng lệnh `mov`

Ví dụ:
```asm
mov rax, 0x10; Di chuyển giá trị 0x10 vào trong rax
```