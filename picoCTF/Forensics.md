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
-how to use wireshark
-tftp protocol
-steghide
## Other incorrect methods you tried:
i tried using tcpdump but i didnt understand it and i also tried dynamitelab but didnt understand it.


## References
-https://trailofbits.github.io/ctf/forensics/
-https://www.youtube.com/watch?v=A4_DOr7Eiqo
