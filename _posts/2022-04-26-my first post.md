---
published: false
---
# Welcome to jmp internal 

So i would like to start by stating the purpose of this blog. In here i will posts about reverse engineering and exploit developement, and i can share also my ctf writeup here.

so let's begin with our [first challenge](https://challenges.re/1/)

## the challenge


### task
What does this code do? The function has 4 arguments and it is compiled by GCC for Linux x64 ABI (i.e., arguments are passed in registers).
```asm
<f>:
   0:                   mov    r8,rdi
   3:                   push   rbx
   4:                   mov    rdi,rsi
   7:                   mov    rbx,rdx
   a:                   mov    rsi,r8
   d:                   xor    rdx,rdx

begin:
  10:                   lods   rax,QWORD PTR ds:[rsi]
  12:                   div    rbx
  15:                   stos   QWORD PTR es:[rdi],rax
  17:                   loop   begin
  19:                   pop    rbx
  1a:                   mov    rax,rdx
  1d:                   ret
```


