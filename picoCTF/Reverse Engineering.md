# GDB BABY STEP 1 
**Flag:** `picoCTF{549698}`
## How you approached the challenge:
I watched the `what is a ctf` video mentioned in the task, then i watched other video about ctf in general where the person talked about not being shy in taking hints, so i took both the hints at the same time.The first hint talked about `GDB debugger`
and the second hint talked about `main` as a symbol which can be used with the `GDB debugger` which didnt made any sense at that moment.Then I downloaded the file mentioned in the challenge.i could not open the file so i was very confused for some time.
Then i started searching about `GDB debugger` and `GDB debugger commands`.I couldn't get anything related to the challenge, but then i searched `disassemble gdb` because the challenge said to disassemble the file given.This lead me to a site in which
there where `gdb debugger disassemble commands` where in the examples i could see `eax` which was mentioned in the challenge. Then i went on youtube to learn how to use `GDB` then i watched 2-3 video, then i opened the terminal and i `cd` to the 
`downloads` because that is where my downloaded file was and then i typed `gdb` but i hadnt installed `gdb` so i installed it and then i typed `gbd debugger0_a` where `debugger0_a` was the name of the file given in the challenge.Then i typed 
`disassemble debugger0_a` but that didnt do anything then i typed `disassemble eax` but that didnt do anything then i typed `disassemble main` which did something. then i understood that it dumped the assembly code of the function `main` and the 2nd hint
was  about using `main` as an argument for the `gdb command`.then i found `eax` and infront of it a hexdecimal number which then i converted into decimal which was the flag.The challenge mentioned that the flag will be the content of `eax` register .
``` bash

aditya@pop-os:~$ cd ~/Dowloads
bash: cd: /home/aditya/Dowloads: No such file or directory
aditya@pop-os:~$ cd ~/Downloads
aditya@pop-os:~/Downloads$ gdb debugger0_a
GNU gdb (Ubuntu 12.1-0ubuntu1~22.04.2) 12.1
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debugger0_a...
(No debugging symbols found in debugger0_a)
(gdb) disassemble debugger0_a
No symbol table is loaded.  Use the "file" command.
(gdb) disassemble eax
No symbol table is loaded.  Use the "file" command.
(gdb) disassemble main 
Dump of assembler code for function main:
   0x0000000000001129 <+0>:	endbr64 
   0x000000000000112d <+4>:	push   %rbp
   0x000000000000112e <+5>:	mov    %rsp,%rbp
   0x0000000000001131 <+8>:	mov    %edi,-0x4(%rbp)
   0x0000000000001134 <+11>:	mov    %rsi,-0x10(%rbp)
   0x0000000000001138 <+15>:	mov    $0x86342,%eax
   0x000000000000113d <+20>:	pop    %rbp
   0x000000000000113e <+21>:	ret    
End of assembler dump.
(gdb) quit 
```
## What you learned through solving this challenge:
- gdb (gnu debugger)
- disassemble command
- few commands in gdb
## Other incorrect methods you tried:
- i was lucky that i got the correct method in the first try 
## References
- https://www.youtube.com/watch?v=8ev9ZX9J45A
- https://www.youtube.com/watch?v=P07NH5F-t3s
- https://www.geeksforgeeks.org/gdb-command-in-linux-with-examples/
- https://www.tutorialspoint.com/gnu_debugger/gdb_commands.htm
- https://visualgdb.com/gdbreference/commands/disassemble
- https://www.youtube.com/watch?v=qzkp3bf_E44
- https://www.youtube.com/watch?v=Dq8l1_-QgAc
## Remark
i have more things to learn from this challenge like the disassemble command and the use of gdb,i will update my report when i learn those.


