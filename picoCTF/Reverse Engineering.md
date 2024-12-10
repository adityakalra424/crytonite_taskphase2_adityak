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

# Vault Door 4

**Flag:** `picoCTF{jU5t_4_bUnCh_0f_bYt3s_f4a8cd8f7e}`

## How you approached the challenge:
I opened the file given in the challenge, It was a java file.The code:
``` bash
import java.util.*;

class VaultDoor4 {
    public static void main(String args[]) {
        VaultDoor4 vaultDoor = new VaultDoor4();
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

    // I made myself dizzy converting all of these numbers into different bases,
    // so I just *know* that this vault will be impenetrable. This will make Dr.
    // Evil like me better than all of the other minions--especially Minion
    // #5620--I just know it!
    //
    //  .:::.   .:::.
    // :::::::.:::::::
    // :::::::::::::::
    // ':::::::::::::'
    //   ':::::::::'
    //     ':::::'
    //       ':'
    // -Minion #7781
    public boolean checkPassword(String password) {
        byte[] passBytes = password.getBytes();
        byte[] myBytes = {
            106 , 85  , 53  , 116 , 95  , 52  , 95  , 98  ,
            0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f,
            0142, 0131, 0164, 063 , 0163, 0137, 0146, 064 ,
            'a' , '8' , 'c' , 'd' , '8' , 'f' , '7' , 'e' ,
        };
        for (int i=0; i<32; i++) {
            if (passBytes[i] != myBytes[i]) {
                return false;
            }
        }
        return true;
    }
}
```
so the code is checking for the correct flag. The function `checkPassword` in the code checks if the the inputted answers is the correct flag. 
checkPassword function :
``` bash
public boolean checkPassword(String password) {
        byte[] passBytes = password.getBytes();
        byte[] myBytes = {
            106 , 85  , 53  , 116 , 95  , 52  , 95  , 98  ,
            0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f,
            0142, 0131, 0164, 063 , 0163, 0137, 0146, 064 ,
            'a' , '8' , 'c' , 'd' , '8' , 'f' , '7' , 'e' ,
        };
        for (int i=0; i<32; i++) {
            if (passBytes[i] != myBytes[i]) {
                return false;
            }
        }
        return true;
    }
```
what the function does is it takes each character from the input in the `passBytes`  using `byte[] passBytes = password.getBytes();` where the input is `password` and compares is with `myBytes` using a `for` loop so i just had to convert the `myBytes` to get the answer/flag. The first line of myBytes is decimal, the second line of myBytes is hexadecimal, the third line of myBytes is octal and the last line of myBytes is just characters. I converted each unit of myBytes into character to get the flag.

## What you learned through solving this challenge:
1. hexadecimal conversions
2. octal conversions
3. decimal conversions

## Other incorrect methods you tried:
- no 

## References
no references


# ARMssembly 0

**Flag:** `picoCTF{e5c69cd8}`

## How you approached the challenge:
I downloaded the file `chall.s` from the challenge.It consisted a assembly code, i started learning assembly language but it was taking some time. then i went on 
`ctf101.org` and then i went in the `reverse-engineering` section where i learned about assembly/machine code and disassemblers and debuggers and decompliers. 
`Decompilers do the impossible and reverse compiled code back into psuedocode/code.`.I got to know that i could convert the assembly code into some other language 
like `c`. So i searched for assembly language convertor and i got ` coderconvert.ai`  where i converted the aseembly code to `c` language.
Using the site i converted the assembly language into `c` language. The converted code:
``` bash
#include <stdio.h>
#include <stdlib.h>

int func1(int a, int b) {
    if (b <= a) {
        return a;
    } else {
        return b;
    }
}

int main(int argc, char *argv[]) {
    int num1, num2, result;

    if (argc < 3) {
        printf("Usage: %s <num1> <num2>\n", argv[0]);
        return 1;
    }

    num1 = atoi(argv[1]);
    num2 = atoi(argv[2]);

    result = func1(num1, num2);
    printf("Result: %d\n", result);

    return 0;
}

```
In this code, i could see that the code is simply comparing the two arguments using the `func1` fucntion and returning the bigger number.So between the two argument given in the challenge, the bigger number was `3854998744`. Then i converted it into hexadecimal as intructed in the challenge which was `e5c69cd8`
and i got the flag.

## What you learned through solving this challenge:
1. little bit of assembly(not the whole assembly)

## References

- ctf101.org
- https://www.youtube.com/watch?v=gfmRrPjnEw4 ( youtube video where i was learning assembly)
- https://www.codeconvert.ai/assembly-to-c-converter (  site where i converted the code )


# ARMssembly 1

**Flag:** `picoCTF{0000005a}`

How you approached the challenge:
I downloaded the file `chall.s` from the challenge.It consisted a assembly code,Using` codecovert.ai `i converted the assembly language into `c` language. The converted code:
```bash
#include <stdio.h>
#include <stdlib.h>

int func(int a) {
    int stack[8]; // Simulating stack allocation
    stack[3] = a; // str w0, [sp, 12]
    stack[4] = 68; // str w0, [sp, 16]
    stack[5] = 2; // str w0, [sp, 20]
    stack[6] = 3; // str w0, [sp, 24]

    stack[7] = stack[5] << stack[4]; // lsl w0, w1, w0
    stack[7] = stack[7] / stack[6]; // sdiv w0, w1, w0
    stack[7] = stack[7] - stack[3]; // sub w0, w1, w0

    return stack[7]; // return value
}

int main(int argc, char *argv[]) {
    int input;
    if (argc > 1) {
        input = atoi(argv[1]); // Convert string to integer
    } else {
        return 1; // No input provided
    }

    int result = func(input);
    if (result == 0) {
        puts("You win!");
    } else {
        puts("You Lose :(");
    }

    return 0;
}#include <stdio.h>
#include <stdlib.h>

int func(int a) {
    int stack[8]; // Simulating stack allocation
    stack[3] = a; // str w0, [sp, 12]
    stack[4] = 68; // str w0, [sp, 16]
    stack[5] = 2; // str w0, [sp, 20]
    stack[6] = 3; // str w0, [sp, 24]

    stack[7] = stack[5] << stack[4]; // lsl w0, w1, w0
    stack[7] = stack[7] / stack[6]; // sdiv w0, w1, w0
    stack[7] = stack[7] - stack[3]; // sub w0, w1, w0

    return stack[7]; // return value
}

int main(int argc, char *argv[]) {
    int input;
    if (argc > 1) {
        input = atoi(argv[1]); // Convert string to integer
    } else {
        return 1; // No input provided
    }

    int result = func(input);
    if (result == 0) {
        puts("You win!");
    } else {
        puts("You Lose :(");
    }

    return 0;
}
```
The challenge asks me to win.Looking at the code, if i want to win, then i must get the `result` as `0`.To do so i need to look as the function `func` 
function `func`:
``` bash
int func(int a) {
    int stack[8]; // Simulating stack allocation
    stack[3] = a; // str w0, [sp, 12]
    stack[4] = 68; // str w0, [sp, 16]
    stack[5] = 2; // str w0, [sp, 20]
    stack[6] = 3; // str w0, [sp, 24]

    stack[7] = stack[5] << stack[4]; // lsl w0, w1, w0
    stack[7] = stack[7] / stack[6]; // sdiv w0, w1, w0
    stack[7] = stack[7] - stack[3]; // sub w0, w1, w0

    return stack[7]; // return value
}
```
The challenge gave us three varible `68 , 2, 3 ` and the function returns the `stack[7]` value, so i just had to choose a value of `a` such that the value of `stack[7]` becomes `0` so that i can get a `win`. First the stack[7] is `stack[7] = stack[5] << stack[4];` where `<<` is a shift operator.But the correct code should be `stack[7] = stack[4] << stack[5]` which is `68 << 2` which is `272`( how i got it was 68 << 2 gave me an error in the c compiler and then i converted the  assembly code into python which said 68 << 2 ) then the stack[7] is  `stack[7] = stack[7] / stack[6];` which is `272/3` which is `90` (int) so then 
stack[3] which the value we need to find needs to satisfy `stack[7] = stack[7] - stack[3];` so that value of `stack[3]=a `is` 90 `.Then i converted 90 into hexadecimal which was `5a`. and i got the flag.

## Other incorrect methods you tried:
- i tried picoCTF{5a} but the format was given in the challenge which was picoCTF{xxxxxxxx} so the flag was picoCTF{0000005a}
## References
same as the ARMassembly 0 

