# buffer overflow 0

**Flag:** `picoCTF{ov3rfl0ws_ar3nt_that_bad_ef01832d}`

## How you approached the challenge:
I downloaded the source code 
```bash
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <signal.h>

#define FLAGSIZE_MAX 64

char flag[FLAGSIZE_MAX];

void sigsegv_handler(int sig) {
  printf("%s\n", flag);
  fflush(stdout);
  exit(1);
}

void vuln(char *input){
  char buf2[16];
  strcpy(buf2, input);
}

int main(int argc, char **argv){
  
  FILE *f = fopen("flag.txt","r");
  if (f == NULL) {
    printf("%s %s", "Please create 'flag.txt' in this directory with your",
                    "own debugging flag.\n");
    exit(0);
  }
  
  fgets(flag,FLAGSIZE_MAX,f);
  signal(SIGSEGV, sigsegv_handler); // Set up signal handler
  
  gid_t gid = getegid();
  setresgid(gid, gid, gid);


  printf("Input: ");
  fflush(stdout);
  char buf1[100];
  gets(buf1); 
  vuln(buf1);
  printf("The program will exit now\n");
  return 0;
}
```
then i took the hints and then i typed `man gets` in the terminal and then went to the bugs section where it said that the gets functions `gets() will continue to  store  characters  past
the  end  of the buffer` and so looking at the code all i needed to do was to overflow the stack and get a segentation error and the code will print out 
the flag.The function that will get me my flag is `void sigsegv_handler(int sig)`.The size of the buf is given as 16 and the gets function will read any input i give so  
that will cause a segmentation error and the code will give me the flag.

## What you learned through solving this challenge:

1. buffer overflow( still need to learn a lot more)

## Other incorrect methods you tried:

## References
1. https://www.youtube.com/watch?v=sLsgSC6ViS8
i did look at the video which explained the challenge on how the code was printing out the flag but only after getting the flag.

# format string 0

**Flag:** `picoCTF{7h3_cu570m3r_15_n3v3r_SEGFAULT_dc0f36c4}`

## How you approached the challenge:
I looked at the hints and then i search what is format specifier and then i searched `format string vulnerability` and went to a site and learned about it.Then 
i downloaded the source code,and opened it in vs code,
```bash
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <signal.h>
#include <unistd.h>
#include <sys/types.h>

#define BUFSIZE 32
#define FLAGSIZE 64

char flag[FLAGSIZE];

void sigsegv_handler(int sig) {
    printf("\n%s\n", flag);
    fflush(stdout);
    exit(1);
}

int on_menu(char *burger, char *menu[], int count) {
    for (int i = 0; i < count; i++) {
        if (strcmp(burger, menu[i]) == 0)
            return 1;
    }
    return 0;
}

void serve_patrick();

void serve_bob();


int main(int argc, char **argv){
    FILE *f = fopen("flag.txt", "r");
    if (f == NULL) {
        printf("%s %s", "Please create 'flag.txt' in this directory with your",
                        "own debugging flag.\n");
        exit(0);
    }

    fgets(flag, FLAGSIZE, f);
    signal(SIGSEGV, sigsegv_handler);

    gid_t gid = getegid();
    setresgid(gid, gid, gid);

    serve_patrick();
  
    return 0;
}

void serve_patrick() {
    printf("%s %s\n%s\n%s %s\n%s",
            "Welcome to our newly-opened burger place Pico 'n Patty!",
            "Can you help the picky customers find their favorite burger?",
            "Here comes the first customer Patrick who wants a giant bite.",
            "Please choose from the following burgers:",
            "Breakf@st_Burger, Gr%114d_Cheese, Bac0n_D3luxe",
            "Enter your recommendation: ");
    fflush(stdout);

    char choice1[BUFSIZE];
    scanf("%s", choice1);
    char *menu1[3] = {"Breakf@st_Burger", "Gr%114d_Cheese", "Bac0n_D3luxe"};
    if (!on_menu(choice1, menu1, 3)) {
        printf("%s", "There is no such burger yet!\n");
        fflush(stdout);
    } else {
        int count = printf(choice1);
        if (count > 2 * BUFSIZE) {
            serve_bob();
        } else {
            printf("%s\n%s\n",
                    "Patrick is still hungry!",
                    "Try to serve him something of larger size!");
            fflush(stdout);
        }
    }
}

void serve_bob() {
    printf("\n%s %s\n%s %s\n%s %s\n%s",
            "Good job! Patrick is happy!",
            "Now can you serve the second customer?",
            "Sponge Bob wants something outrageous that would break the shop",
            "(better be served quick before the shop owner kicks you out!)",
            "Please choose from the following burgers:",
            "Pe%to_Portobello, $outhwest_Burger, Cla%sic_Che%s%steak",
            "Enter your recommendation: ");
    fflush(stdout);

    char choice2[BUFSIZE];
    scanf("%s", choice2);
    char *menu2[3] = {"Pe%to_Portobello", "$outhwest_Burger", "Cla%sic_Che%s%steak"};
    if (!on_menu(choice2, menu2, 3)) {
        printf("%s", "There is no such burger yet!\n");
        fflush(stdout);
    } else {
        printf(choice2);
        fflush(stdout);
    }
}
```
I could get the flag by causing a seg fault but the challenge was of format string vuln.So then i started looking for format specifiers which i got in menu2[],
`Cla%sic_Che%s%steak` but it is in `serve_bob` function and to reach that i need to use the` serve_patric` function, the else statement, so start typeing the name of the burgers and then i when into `serve_bob` function when i typed `Gr%114d_Cheese` and then i typed `Cla%sic_Che%s%steak` and then i got the flag.

## What you learned through solving this challenge:

1. format string vuln

## Other incorrect methods you tried:
- no 

References

- [reference 1](https://www.geeksforgeeks.org/format-specifiers-in-c/)
- [reference 2](https://owasp.org/www-community/attacks/Format_string_attack)
- 
