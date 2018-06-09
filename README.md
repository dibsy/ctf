# ctf

This is where I store CTF writeups I've made. 

## Pwn

#### ROP Chain
+ x64: bkp16/pwn/simple-calc Basic ROP Chain, syscall to execve("/bin/sh", NULL, NULL), Weird method of writing data to memeory
+ x32: defconquals16/pwn/feedme ROP Chain syscall to execve("/bin/sh", NULL, NULL), brute force stack canary, stripped elf
#### Heap
+ x86: bkp16/pwn/cookbook Use After Free, House of Power exploit, expand heap into libc, write over free hook with system address, call free with pointer to "/bin/sh", libc and heap address leaks, reversing structs
+ x64: 0ctf/pwn/babyheap Heap Overflow, Chunk Consolidation and fastbin duplication into libc, oneshot
+ x64: RCTF/pwn/babyheap One Null Byte Overflow, chunk consolidation, double free, libc file
+ x64: asis18quals/pwn/cat Use After Free, creating format string bug, format string. got/plt addresses
+ x64: Hitcon16/pwn/SleepyHolder Double Free, fastin duplication consolidation, unsafe unlink, overwrite got address, infoleak
+ x86: hack.lu14/pwn/oreo House of Spirit, heap overflow for libc infoleak, allocate heap chunk with malloc to bss
#### Return 2 System
+ x86: TUCTF/guestbook  Infoleak, PIE, strcpy
+ x64: AsisFinals2017/Mary_Morton fmt_string Stack Canary Infoleak, "cat flag" string at static address
##### Return 2 libc
+ x64: AsisFinals2017/Mrs._Hudson Call Scanf, scan in shellcode into memory, call shellcode
#### Faking Inputs
+ x64: bkp16/pwn/complex-calc pass false pointer to free and not crash, pointer is to bss

## Reverse Engineering (RE)

#### Dynamic Analysis
+ x64: bkp16/re/jit Use gdb to reverse obfuscated program, read breakpoints on input
+ x86: other/re/movfuscated Side Channel Attack on Movfuscated program, obfuscation where elf only uses mov instructions
#### Static Analysis
+ x64: bkp16/re/unholy ruby, python, x64 shared library, xtea encryption/decryption/identification z3
+ x86: defcon-quals-2018/elf-crumble x86, opcodes, patching, common x86 knowledge
+ x64: RCTF/re/sign strings
#### Static and Dynamic Analysis
+ x86: RCTF/re/babyre figure out what's important/what's not, one to one function for each character
+ x86: Asis18Quals/re/babyc Movfuscation, Demovfuscator, program obfuscation
#### Code Review
+ asis18quals/re/warmup:  Cleaning up code, editing source code

## Non-Challenges Pwn
#### Heap
+ shellphish_how2heap/first_fit: Block reuse after free
+ shellphish_how2heap/fastbin_dup: Double Free to return same pointer twice
+ shellphish_how2heap/fastbin_dup_into_stack: Double Free to return same ptr twice, use that to return return stack ptr from malloc
+ shellphish_how2heap/fastbin_dup_consolidate: Double free to same ptr twice, allocate large chunk in between to move ptr out of fastbin list to pass malloc() check
+ shellphish_how2heap/unsafe_unlink:  Alter metadata of a chunk, into chunk before that one create a fake chunk, get an arbitrary write over an address that you know
+ shellphish_how2heap/house-of-spirit:  Overwrite a pointer, and write to integers to region you conttrol to create fake chunk, free overwritten pointer, have malloc return pointer to the region you wrote integers to
+ shellphish_how2heap/single_null_byte_overflow:  Allocate a heap chunk that overlaps with another heap chunk, by causing a heap consolidation using a single null byte overflow.
+ shellphish_how2heap/house-of-spirit:  Get malloc to return a pointer to the stack, by creating fake chunks on the stack, and overwriting freed heap small bin `bk` pointer to second fake stackc chunk.
+ shellphish_how2heap/overlapping_chunks: Get malloc to return a freed chunk (unsorted bin) that overlaps with another chunk, by overwriting the size value of the freed chunk
