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


# VAULT-DOOR-1

**Flag:** `picoCTF{d35cr4mbl3_tH3_cH4r4cT3r5_f6daf4}`

## How you approached the challenge:
I opened the file given in the challenge, It was a java file.The code:
```bash
import java.util.*;

class VaultDoor1 {
    public static void main(String args[]) {
        VaultDoor1 vaultDoor = new VaultDoor1();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
	String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
	}
    }

    // I came up with a more secure way to check the password without putting
    // the password itself in the source code. I think this is going to be
    // UNHACKABLE!! I hope Dr. Evil agrees...
    //
    // -Minion #8728
    public boolean checkPassword(String password) {
        return password.length() == 32 &&
               password.charAt(0)  == 'd' &&
               password.charAt(29) == 'a' &&
               password.charAt(4)  == 'r' &&
               password.charAt(2)  == '5' &&
               password.charAt(23) == 'r' &&
               password.charAt(3)  == 'c' &&
               password.charAt(17) == '4' &&
               password.charAt(1)  == '3' &&
               password.charAt(7)  == 'b' &&
               password.charAt(10) == '_' &&
               password.charAt(5)  == '4' &&
               password.charAt(9)  == '3' &&
               password.charAt(11) == 't' &&
               password.charAt(15) == 'c' && 
               password.charAt(8)  == 'l' && 
               password.charAt(12) == 'H' &&
               password.charAt(20) == 'c' && 
               password.charAt(14) == '_' &&
               password.charAt(6)  == 'm' &&
               password.charAt(24) == '5' &&
               password.charAt(18) == 'r' && 
               password.charAt(13) == '3' &&
               password.charAt(19) == '4' &&
               password.charAt(21) == 'T' &&
               password.charAt(16) == 'H' &&
               password.charAt(27) == '6' &&
               password.charAt(30) == 'f' &&
               password.charAt(25) == '_' &&
               password.charAt(22) == '3' &&
               password.charAt(28) == 'd' &&
               password.charAt(26) == 'f' &&
               password.charAt(31) == '4';
    }
}
```
-----------------------------------------------------------------
I could figure out that the program was checking if the flag is correct or not.`System.out.print("Enter vault password: ");
String userInput = scanner.next();` was taking an input flag from the user.`String input = userInput.substring("picoCTF{".length(),userInput.length()-1);` was checking the format of the flag and the function `checkPassword` was checking the contents of the flag.I looked at the contents of the function `checkPassword`
it was using `charat()` so i searched `charat()` in google. The `charAt()` method returns the character at the specified index in a string.So the function is using 
the `charAt()` method to check the characters of the inputted password with the true password at different index and if all are true then the function return true.So the flag is written in the code itself.I manually wrote the code and got the flag.

![WhatsApp Image 2024-11-07 at 14 33 27_516c93b1](https://github.com/user-attachments/assets/3c92a920-fc46-43b1-9202-16cd6bcab513)


## What you learned through solving this challenge:
1. chatAT() method 

## Other incorrect methods you tried:
- no incorrect methods

## References
- https://www.w3schools.com/java/ref_string_charat.asp

# VAULT-DOOR-3

**Flag:** `picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_79958f}`

## How you approached the challenge:
I opened the file given in the challenge, It was a java file.The code:
```bash
import java.util.*;

class VaultDoor3 {
    public static void main(String args[]) {
        VaultDoor3 vaultDoor = new VaultDoor3();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // Our security monitoring team has noticed some intrusions on some of the
    // less secure doors. Dr. Evil has asked me specifically to build a stronger
    // vault door to protect his Doomsday plans. I just *know* this door will
    // keep all of those nosy agents out of our business. Mwa ha!
    //
    // -Minion #2671
    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm18g947_u_4_m9r54f");
    }
}
```
I could figure out that the program was checking if the flag is correct or not but in this program the function was first encrypting the input and then comparing it with 
`jU5t_a_sna_3lpm18g947_u_4_m9r54f`.`System.out.print("Enter vault password: "); String userInput = scanner.next();` is taking an input from the user for the flag.
The `checkPasword` function was first encrypting the input and then comparing it with `jU5t_a_sna_3lpm18g947_u_4_m9r54f`.the encryption is 
```bash
char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
```
So i wrote a code in c to decrypt the encrypted string `jU5t_a_sna_3lpm18g947_u_4_m9r54f`
### code
```bash
#include<stdio.h>
int main(){
    int i=0;
    char string[]="jU5t_a_sna_3lpm18g947_u_4_m9r54f";
    char ans[100]="";
    for (i=0; i<8; i++) {
            ans[i]=string[i];
        }
        for (i=8 ; i<16; i++) {
            ans[23-i]=string[i];
        }
        for (i=16; i<32; i+=2) {
            ans[46-i]=string[i];
        }
        for (i=31; i>=17; i-=2) {
            ans[i]=string[i];
        }
    for (i=0;i<33;i++){
        printf("%c",ans[i]);

    }
    return 0;
}
```
### output 
`jU5t_a_s1mpl3_an4gr4m_4_u_79958f`

![image](https://github.com/user-attachments/assets/d36fad81-9373-4ef9-a986-b55cf2e65c36)


## What you learned through solving this challenge:
1. charAT()

## Other incorrect methods you tried:
- i tried to decrypt it manually and it was only half right 

## References
no references 



