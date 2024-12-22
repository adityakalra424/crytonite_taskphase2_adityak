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
Then i got stuck here for a few min(**hours) and then i watched the walkthrough video because i couldnt figure it out.then it told me about the selfinput 
and it said pythontwo so i downloaded python two and then i went to the terminal and wrote `cat convertout.py | python2 convertout.py `
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
so i had to reverse the `encrypt` function and then reverse the `dynamic_xor_encrypt` function to get the flag.So i wrote a code to decrypt the ciphertext
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

# Mini RSA

**Flag:** `picoCTF{e_sh0u1d_b3_lArg3r_6e2e6bda}`

## How you approached the challenge:
I went through the hints and then i researched about rsa and then i started searching for a formula for the rsa and after few hours i got a website
`https://crypto.stackexchange.com/questions/6770/cracking-an-rsa-with-no-padding-and-very-small-e/6771#6771` 
Normally to get the plaintext i could just compute n^(1/3) but the challenge said that it had some padding in the m^e such that it is slightly larger than n 
so now the formula for the plain text will be ![image](https://github.com/user-attachments/assets/5d6206ec-aaf5-4096-82fc-3ef12ab40c3f)
then i searched cube root python and went to this site 
`https://stackoverflow.com/questions/28014241/how-to-find-cube-root-using-python`
and i found the math.cbrt()
then i wrote a python program to solve the challenge but it had a error saying that the number is too big for math.cbrt() so i went to google and searched for 
`how to find the nth root of a large number python` and i got this `https://riptutorial.com/python/example/8751/computing-large-integer-roots` 
and then i changed the code and know i need to find pico from all the intergers and print it so i first tried to convert the integers to strings but i couldnt 
and then i tried to convert the integers to hex and that was successfull using `format()` function, now i just needed to search pico in hex and print that hex value in strings.so i went on google and searched `how to convert hex to string in python` and i got `bytes.fromhex()` function and i used that and then i got the flag.letssgoooo.
the code:
``` bash
def nth_root(x, n):
    # Start with some reasonable bounds around the nth root.
    upper_bound = 1
    while upper_bound ** n <= x:
        upper_bound *= 2
    lower_bound = upper_bound // 2
    # Keep searching for a better result as long as the bounds make sense.
    while lower_bound < upper_bound:
        mid = (lower_bound + upper_bound) // 2
        mid_nth = mid ** n
        if lower_bound < mid and mid_nth < x:
            lower_bound = mid
        elif upper_bound > mid and mid_nth > x:
            upper_bound = mid
        else:
            # Found perfect nth root.
            return mid
    return mid + 1
n=1615765684321463054078226051959887884233678317734892901740763321135213636796075462401950274602405095138589898087428337758445013281488966866073355710771864671726991918706558071231266976427184673800225254531695928541272546385146495736420261815693810544589811104967829354461491178200126099661909654163542661541699404839644035177445092988952614918424317082380174383819025585076206641993479326576180793544321194357018916215113009742654408597083724508169216182008449693917227497813165444372201517541788989925461711067825681947947471001390843774746442699739386923285801022685451221261010798837646928092277556198145662924691803032880040492762442561497760689933601781401617086600593482127465655390841361154025890679757514060456103104199255917164678161972735858939464790960448345988941481499050248673128656508055285037090026439683847266536283160142071643015434813473463469733112182328678706702116054036618277506997666534567846763938692335069955755244438415377933440029498378955355877502743215305768814857864433151287
c=1220012318588871886132524757898884422174534558055593713309088304910273991073554732659977133980685370899257850121970812405700793710546674062154237544840177616746805668666317481140872605653768484867292138139949076102907399831998827567645230986345455915692863094364797526497302082734955903755050638155202890599808146956044568639690002921620304969196755223769438221859424275683828638207433071955615349052424040706261639770492033970498727183446507482899334169592311953247661557664109356372049286283480939368007035616954029177541731719684026988849403756133033533171081378815289443019437298879607294287249591634702823432448559878065453908423094452047188125358790554039587941488937855941604809869090304206028751113018999782990033393577325766685647733181521675994939066814158759362046052998582186178682593597175186539419118605277037256659707217066953121398700583644564201414551200278389319378027058801216150663695102005048597466358061508725332471930736629781191567057009302022382219283560795941554288119544255055962

for i in range(5000):
    st = ("{:x}".format(nth_root(c+i*n,3)))
    if "7069636f" in st:
        print(st)
        byte_string = bytes.fromhex(st)
        result = byte_string.decode("utf-8")
        print(result)
```

## What you learned through solving this challenge:
1. RSA
2. int to hex using format
3. hex to string using bytes.fromhex() function


## Other incorrect methods you tried:
1. i tried the rsa online decoder, i knew it wont work because this challenege had some padding but i still tried it 

References
1. https://crypto.stackexchange.com/questions/6770/cracking-an-rsa-with-no-padding-and-very-small-e/6771#6771
2. https://riptutorial.com/python/example/8751/computing-large-integer-roots
3. wikipedia 
