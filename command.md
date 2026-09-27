# MOV
Dùng để di chuyển dữ liệu giữa các thanh ghi

Thanh ghi thì có kích thước nhỏ những tốc độ thực thi nhanh. Bộ nhớ thì kích thước lớn hơn nhưng tốc độ thực thi chậm

## Load dữ liệu từ một vùng nhớ
1. Lấy giá trị tại một địa chỉ ô nhớ
~~~
  Address │ Contents
+────────────────────+
│ 31337   │ 42       │
+────────────────────+
~~~

Để lấy được giá trị tại địa chỉ `0x31337`, ta làm như sau
~~~asm
mov rdi, [31337]
~~~

Dấu `[]` có ý nghĩa như việc giải tham chiếu giống con trỏ trong C

2. Trong trường hợp các thanh ghi đang trỏ đến ô nhớ chứa giá trị cần lấy
~~~
    Address │ Contents
  +────────────────────+
┌▸│ 133700  │ 42       │
│ +────────────────────+
│
└────────────────────────┐
                         │
   Register │ Contents   │
  +────────────────────+ │
  │ rax     │ 133700   │─┘
  +────────────────────+
~~~

Bây giờ để lấy giá trị `42`, ta lm như sau
~~~asm
mov rdi, [rax]
~~~

3. Tự giải tham chiếu
~~~
  Address │ Contents
+────────────────────+
│ 133700  │     ?    │
+────────────────────+
~~~

~~~asm
mov [133700], 42    -> Ghi giá trị 42 vào ô nhớ có địa chỉ 0x133700
mov rax, 0x133700   -> Ghi địa chỉ của ô nhớ vào trong rax
mov rax, [0x133700] -> Giải tham chiếu: giá trị 42 sẽ được lưu trữ trong rax
~~~

4. Giải tham chiếu với `offset`
~~~
    Address │ Contents
  +────────────────────+
┌▸│ 133700  │    50    │
│ │ 133701  │    42    │
│ │ 133702  │    99    │
│ │ 133703  │    14    │
│ +────────────────────+
│
└────────────────────────┐
                         │
   Register │ Contents   │
  +────────────────────+ │
  │ rdi     │ 133700   │─┘
  +────────────────────+
~~~

Nếu ta muốn lấy giá trị 99 để ghi vào thanh ghi `rax`

~~~asm
mov rax, [rdi + 2]
~~~

5. Lưu trữ địa chỉ trong các ô nhớ
~~~
  Address │ Contents
+────────────────────+
│ 133700  │ 42       │
+────────────────────+
         ...
+────────────────────+
│ 123400  │ 133700   │
+────────────────────+
~~~

Làm thế nào để lấy giá trị `42` ghi vào trong thanh ghi rax?
~~~asm
mov rdi, 0x123400 ; rdi lúc này chứa giá trị 0x123400
mov rdi, [rdi]    ; 
mov rax, [rdi]
~~~