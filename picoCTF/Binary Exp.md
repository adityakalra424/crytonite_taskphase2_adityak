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
