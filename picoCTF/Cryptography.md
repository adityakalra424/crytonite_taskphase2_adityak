# C3

**Flag:** `flag`

## How you approached the challenge
I downloaded the file in the given challenge,Then i opened the encoder file in vs code. To decode cipher text,I wrote a python code to decode the cipher text 
```bash
import sys
chars = "DLSeGAGDgBNJDQJDCFSFnRBIDjgHoDFCFtHDgJpiHtGDmMAQFnRBJKkBAsTMrsPSDDnEFCFtIbEDtDCIbFCFtHTJDKerFldbFObFCFtLBFkBAAAPFnRBJGEkerFlcPgKkImHnIlATJDKbTbFOkdNnsgbnJRMFnRBNAFkBAAAbrcbTKAkOgFpOgFpOpkBAAAAAAAiClFGIPFnRBaKliCgClFGtIBAAAAAAAOgGEkImHnIl"


lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"

out = ""

prev = 0
for char in chars:
  cur = lookup2.index(char)
  ch1= lookup1[(cur + prev) % 40]
  out += ch1
  prev = lookup1.index(ch1)

print(out)

```
The ouput:
```bash
#asciiorder
#fortychars
#selfinput
#pythontwo

from fileinput import input
for line in input():
    chars += line
b = 1 / 1

for i in range(len(chars)):
    if i == b * b * b:
        print chars[i] #prints
        b += 1 / 1
```
Then i got stuck here for a few min(**hours) and then i wacthed the walkthrough video because i couldnt figure it out.then i told me about the selfinput 
and it said pythontwo so i downloaded python two and then i went to the terminal and wrote cat convertout.py | python2 convertout.py 
and i got ` a d l i b s `

## What you learned through solving this challenge:
1. python 

## Other incorrect methods you tried:
i was just stuck after the first output didnt do anything. and as for the decryption of the cipher text and the code i wrote, it took be multiple tries to get it write

## References
1. https://www.youtube.com/watch?v=yxQXi_w-PnY

# Custom encryption

**Flag:** `picoCTF{custom_d2cr0pt6d_e4530597}`

## How you approached the challenge:
I downloaded the two files given in the challenge. I opened the encoder in vs code and the encoder code was
the code:
``` bash
from random import randint
import sys


def generator(g, x, p):
    return pow(g, x) % p


def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(((ord(char) * key*311)))
    return cipher


def is_prime(p):
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    if v > 1:
        return False
    else:
        return True


def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text


def test(plain_text, text_key):
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers")
        return
    a = randint(p-10, p)
    b = randint(g-10, g)
    print(f"a = {a}")
    print(f"b = {b}")
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        return
    semi_cipher = dynamic_xor_encrypt(plain_text, text_key)
    cipher = encrypt(semi_cipher, shared_key)
    print(f'cipher is: {cipher}')


if __name__ == "__main__":
    message = sys.argv[1]
    test(message, "trudeau")
```
so i had to reverse the `encrypt` function and then reverse the `dynamic_xor_encrypt` function to get the flag.So i wrote a code to dcrypt the ciphertext
the code:
```bash
def generator(g, x, p):
    return pow(g, x) % p


p = 97
g = 31
a = 97
b = 22
u = generator(g, a, p)
v = generator(g, b, p)
key = generator(v, a, p)
b_key = generator(u, b, p)
shared_key = None
if key == b_key:
 shared_key = key
else:
  print("Invalid key")
print(key)
output=[151146, 1158786, 1276344, 1360314, 1427490, 1377108, 1074816, 1074816, 386262, 705348, 0, 1393902, 352674, 83970, 1141992, 0, 369468, 1444284, 16794, 1041228, 403056, 453438, 100764, 100764, 285498, 100764, 436644, 856494, 537408, 822906, 436644, 117558, 201528, 285498]

semi_cipher = []
for num in output:
    semi_cipher.append(int((num/ key)/311))
  
print(semi_cipher)
semi=""
for num in semi_cipher:
  semi+= chr(num)
  
print(semi)
flag = ""
text_key="trudeau"
key_length = len(text_key)
for i, char in enumerate(semi):
  key_char = text_key[i % key_length]
  dencrypted_char = chr(ord(char) ^ ord(key_char))
  flag += dencrypted_char
  
print(flag)
```
the output:
`}7950354e_d6tp0rc2d_motsuc{FTCocip`
```bash
semi_cipher = []
for num in output:
    semi_cipher.append(int((num/ key)/311))
```
this was the decryption of the encrypt function and then i copy pasted the `dynamic_xor_encrypt` function in the hopes that it will give me some flag as it used
`xor` and if u `xor` an `xor` u get the intials value and it did give me the flag but just in reverse.


## What you learned through solving this challenge:
1. xor

## Other incorrect methods you tried:
none

## References
none
