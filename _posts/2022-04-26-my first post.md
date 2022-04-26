---
published: false
---
# Welcome to jmp internal 

So i would like to start by stating the purpose of this blog. In here i will posts about reverse engineering and exploit developement, and i can share also my ctf writeup here.

so let's begin with our [first challenge](https://challenges.re/1/)

## THE CHALLENGE


### THE TASK
What does this code do? The function has 4 arguments and it is compiled by GCC for Linux x64 ABI (i.e., arguments are passed in registers).
```asm
f:
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

### SOLUTION: 

**Step1 : understanding the question?**

	The function has **4 arguments** == take 4 args + return address
    compiled by GCC for Linux x64 ABI == 64bit abi
    
**Step2 : find resources  online** 
	
[x64 assembly cheat sheet](https://cs.brown.edu/courses/cs033/docs/guides/x64_cheatsheet.pdf)
    
[asm pdf](http://www.lacl.fr/tan/asm)

[abi x64  resource](https://web.archive.org/web/20160801075146/http://www.x86-64.org/documentation/abi.pdf)
    
**Step3 : understand the code using the resouurce**
	
understatunding f:
  	
```asm
    f:
       0:                   mov    r8,rdi 	# copy rdi (destination) to r8 
       3:                   push   rbx 		#  puch the value from rbx to the stack
       4:                   mov    rdi,rsi 	# copy the rsi (source) to rdi (destination)
       7:                   mov    rbx,rdx  # copy the value from rdx to rbx 
       a:                   mov    rsi,r8 	# copy the value from r8 to rsi (source)
       d:                   xor    rdx,rdx 	# set rdx to 0
```

finding more resource

[Registers purpose](http://6.s081.scripts.mit.edu/sp18/x86-64-architecture-guide.html)


understaunding start:
```
begin:
  10:                   lods   rax,QWORD PTR ds:[rsi]
  12:                   div    rbx
  15:                   stos   QWORD PTR es:[rdi],rax
  17:                   loop   begin
  19:                   pop    rbx
  1a:                   mov    rax,rdx
  1d:                   ret
```



        
