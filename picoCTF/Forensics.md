# Trivial Flag Transfer Protocol

**Flag:** `picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}`

## How you approached the challenge:
I downloaded the file given in the challenge. The file was a `pcapng` file. I then went on `https://trailofbits.github.io/ctf/forensics/`(one of the resources given)
and then went onto the pca file analysis.From there i got to know about wireshark.Then i downloaded wireshark.Imported the `pcapng` file in the wireshark.Then i observed
that it was using the ` TFTP` protocol.Then i search `TFTP` protocol and the packet structure of the protocol where of type read request, write request, data, ack and error.
There were some `write` request in a `instructions.txt` file and a `plan` file and there was some `data transfer` then i went on youtube and search how to use wireshark 
in picoctf and i came across a video `Intro to Wireshark (PicoCTF 2022 #17 'packets-primer')` He explained about the wireshark and how wireshark has option to export the 
objects that are being transferred so i exported the objects where i got `instructions.txt`, `plan` , `program.deb`, `picture1.bmp`,`picture2.bmp`,`picture3.bmp`.
The instructions.txt had some string as well and the plan file but it was encryted so i went to dcode and used the shift encrytion to decrypt the string.
The instruction.txt contain was `TFTP DOESNT ENCRYPT OUR TRAFFIC SO WE MUST DISGUISE OUR FLAG TRANSFER.FIGURE OUT AWAY TO HIDE THE FLAG AND I WILL CHECK BACK FOR THE PLAN`
the plan file contain was `I USED THE PROGRAMAND HID IT WITH-DUEDILIGENCE.CHECK OUT THE PHOTOS`.My guess is the flag is hidden in the pictures given but i had one more
file which was the program which they used `program.deb`.Then i search what was a `deb `file and how to access it,Then i used `ar x program.deb` to extract the file
it contained three files `control.tar.gz` `data.tr.gz` and debian-binary and then i opened the dat.tr.gz file and got to know that the program used to hide the flag was
`steghide` and i downloaded steghide and learned how to use it then i typed `steghide extract -sf picture1.bmp` then it asked me for a passphrase if i didnt have then 
i searched and searched and searched forever the two `control.tar.gz` `data.tr.gz` file and still got nothing then i looked at message `WITH-DUEDILIGENCE` so the passphrase
was `DUEDILIGENCE` i used it on the first image and then the second image but got nothing but then the third image had the `flag.txt` file which had the file 
## What you learned through solving this challenge:
1. how to use wireshark,
2. tftp protocol,
3. steghide
## Other incorrect methods you tried:
i tried using tcpdump but i didnt understand it and i also tried dynamitelab but didnt understand it.


## References
 1. https://trailofbits.github.io/ctf/forensics/
 2. https://www.youtube.com/watch?v=A4_DOr7Eiqo

# m00nwalk

**Flag:** `picoCTF{beep_boop_im_in_space}`

## How you approached the challenge:
I downloaded the file given in the challenge, it was a `wav` file.Then i went to `https://trailofbits.github.io/ctf/forensics/`  and i went to the video and audio file analysis where it talked about exiftool and audacity.so i downloaded `audacity` and imported the file but i got nothing new and i also installed mediainfo to get more info about the file.Then i read the hints,`How did pictures from the moon landing get sent back to Earth?` I search it and and then i search `in which format did the pictures from the moon landing get send back to earth `i found that it was `sstv` system.Then `i search how to convert sstv wav and rx` and i found rxsstv which then i installed it but the program was to convert wav to image and not the other way around. Then i search `sstv decoder` and then i got a github repo `https://github.com/colaclanth/sstv` i followed the instruction in the repo and then i installed the decoder and the used the decoder to decode the `wav` file. It then gave me a image `output.png`
![result](https://github.com/user-attachments/assets/c047b711-8b08-4d29-86ca-15594326c713)
`the image was rotated 180degree initially` 

## What you learned through solving this challenge:
 1. sstv system
 2. how to download tools from github
 3. tookkit is important 
## Other incorrect methods you tried:
 1. i tried the exiftool
 2. i tried audacity 

## References
 1. https://trailofbits.github.io/ctf/forensics/
 2. https://github.com/colaclanth/sstv
 3. https://en.wikipedia.org/wiki/Slow-scan_television

# PcapPoisoning

**Flag:** `picoCTF{P64P_4N4L7S1S_SU55355FUL_fc4e803f}`

## How you approached the challenge:
I first downloaded the file given in the challenge and it was a` pcap file (packet capture)` so i opened wireshark and opened the file there.Then i went throught the traffic and then i saw a transmission from a different source and destination and its payload was readable and it was the flag.
![image](https://github.com/user-attachments/assets/1edf9ce7-58d0-4f6a-a91f-7fa6efa2804e)

## What you learned through solving this challenge:
1. wireshark
## Other incorrect methods you tried:
none

## References
no references

# hideme

**Flag:** `picoCTF{Hiddinng_An_imag3_within_@n_ima9e_cda72af0}`

## How you approached the challenge:
I first tried steghide but it said the format is not avaiable and i used a online steg but the site stopped working after i uploaded the image  then i used a hex editor and found some strings like ` secret/flag` and then i went to the terminal and typed ` strings flag.png | grep flag` and i found `secret/flag.png` so that was some info. i used exiftool and it said ` Trailer data after PNG IEND chunk` so some data is stored in the image. Then i search in google how to extract files from png and how to extract hidden files from png and tools to extract hidden files from png.Then i said something about binwalk and then i installed binwalk using `sudo apt install binwalk` and then i extracted the hidden file in the flag.png which was another image named `flag.png` 

![flag](https://github.com/user-attachments/assets/5bd3bdfb-a5a6-4023-ad9e-a5b48cefaf6f)

## What you learned through solving this challenge:

1. U can hid a lot of things in things
2. binwalk tool 

## Other incorrect methods you tried:
- i tried to convert the png to jpg so that i could use steghide but i didnt know the passphrase 

## References
1. https://stackoverflow.com/questions/36530643/use-binwalk-to-extract-all-files


# Matryoshka doll

**Flag:** `picoCTF{bf6acf878dcbd752f4721e41b1b1b66b}`

## How you approached the challenge:
`Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another.` Matryoshka dolls are placed inside one another.The challenge gave me 
a jpg file, then i used `file` command and it said it was a `png` file so i manually converted the format in the file manager and then i used bin walk to extract the hidden data where i got `_2_c.jpg` which was again a `png` file so i manually converted the format in the file manager and then i used binwalk to extract the hidden data from the image from  where i got `_3_c.jpg` file  which was again a `png` file so i manually converted the format in the file manager and then i used binwalk to extract the hidden data from the imagewhere i got `_4_c.jpg` file which was again a `png` file so i manually converted the format in the file manager and then i used binwalk to extract the hidden data from the image  where i got a `flag.txt` file .The content of the file `flag.txt` are `p i c o C T F { b f 6 a c f 8 7 8 d c b d 7 5 2 f 4 7 2 1 e 4 1 b 1 b 1 b 6 6 b }` and it was the flag.
## What you learned through solving this challenge:

1. binwalk 

## Other incorrect methods you tried:
- none

## References
- none

# extensions

**Flag:** `picoCTF{now_you_know_about_extensions}`

## How you approached the challenge:
I downloaded the file and it was a txt file so i opened it,but the header was of a png file so i manually changed the extension of the file in the file manager 
and then opened the file and i got the flag.
<img width="849" alt="flag (2)" src="https://github.com/user-attachments/assets/6812329a-9f47-43e8-b950-fb5da88c3854" />

## What you learned through solving this challenge:
1. extensions

## Other incorrect methods you tried:
none

## References
none
# So meta 

**Flag:** `picoCTF{s0_m3ta_eb36bf44}`

## How you approached the challenge:
I downloaded the file given in the challenge and it was png file.I took the hint and it said meta data so i used `exiftool` to display the metadata of the `png` file and i got the flag in the artist section.
![image](https://github.com/user-attachments/assets/a5f44bd8-86c1-435a-ad00-ce3084e96608)


## What you learned through solving this challenge:

1. exiftool

## Other incorrect methods you tried:
none

## References
none

# Lookey here

**Flag:** `picoCTF{gr3p_15_@w3s0m3_58f5c024}`

## How you approached the challenge:
I downloaded the file from the challenge,it was a `txt` file.I opened the file in the notepad and then i pressed control+f and search pico and i got the flag.
other way was to go in the terminal and type `strings anthem.flag.txt | grep pico` and i got the same result 
![image](https://github.com/user-attachments/assets/b33109bf-fc7d-42fe-b5f2-5d2f86571397)

## What you learned through solving this challenge:

1. grep

## Other incorrect methods you tried:
none
## References
1. i learnt about the grep and strings command from the previous challenges,I probably just searched `how to print the strings in a file` and `how to search for a
   word in the stack of strings` in google at the time.
# What Lies Within

**Flag:** `picoCTF{h1d1ng_1n_th3_b1t5}`

## How you approached the challenge:
I downloaded the file,Then i used the `exiftool` and then the` binwalk` and then `strings` command and the i put it in `hex` editor and still got nothing, then i took the hint and searched image decoder and then i when to a site `https://stylesuxx.github.io/steganography/` and decoded the image and then i got the flag

References
1. https://stylesuxx.github.io/steganography/

# Packets Primer

**Flag:** `picoCTF{p4ck37_5h4rk_b9d53765}`

## How you approached the challenge:
I downloaded the file and it was `pcap` file so i opened the file in wireshark and then i scrolled through the packets and got the flag in one of the packets payload
![image](https://github.com/user-attachments/assets/ad9c265f-3311-4757-ae47-98eb5abbe98e)

## What you learned through solving this challenge:
1. wireshark
2. pcap

## Other incorrect methods you tried:
none

## References
none
