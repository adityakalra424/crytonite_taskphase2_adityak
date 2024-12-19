# Forbidden Paths

**Flag:** `picoCTF{7h3_p47h_70_5ucc355_6db46514}`

## How you approached the challenge:
I first opened the website, then i typed `/flag.txt` and it said `Not Authorized` then i typed `/usr/share/nginx/html/flag.txt` but it still said `Not authorized`
When i typed `flag.txt` it said ` the file does not exist` but the challenge said the file exists in `/usr/share/nginx/html`, then i thought for some time 
and felt that the name of the challenge `forbidden paths` was similar to the `pwn.college` challenges where u had to get to a file without using the absolute path
and the challenge also mentioned absolute paths so i types `../../../../flag.txt1` where `..` lets u access the previous directories and then i got the flag.

![image](https://github.com/user-attachments/assets/6460223f-0069-41db-a142-3f9100f563b3)

## What you learned through solving this challenge:

- Absolute paths 
- A challenge can be anything so think about everything 

## Other incorrect methods you tried:
 - i typed `/usr/share/nginx/html/flag.txt`
 - i typed `flag.txt`
   

## References
 - pwn.college

# Cookies

**Flag:** `picoCTF{3v3ry1_l0v3s_c00k135_064663be}`

How you approached the challenge:

The challenge itself suggested that it had to do something with cookies in the website, so i went to the site, there was a search box, if i typed random things 
it gave me ` That doesn't appear to be a valid cookie.` and i checked the cookies in the website by right clicking then going into inspect and the applications
then storage and the cookies and the value of the cookie was `-1`, then i saw `snickerdoodle` on the search bar so i typed it and then
i got `That is a cookie! Not very special though...` but this time the value of the cookie changed to `0` so i started changing the value of the cookie and refreshed 
the website and i got a new cookie name but it said `That is a cookie! Not very special though...` so i had to find a special cookie but i didnt know its value 
so i typed the value of the cookie in the website as `50` and it gave me ` That doesn't appear to be a valid cookie.` so that meant that it had a range or it didnt 
but i assumed it had a range that i typed `45 40 30 25` in the value of the cookie and `25` gave me a valid cookie but not a special one. I got the upper limit
that was `28` and then i brute forced it, i manually tried every value from 1 to 28 till i got the special cookie, the value of ` 18 `. 

![image](https://github.com/user-attachments/assets/65269818-eca1-43dc-81e5-d3600103e073)


## What you learned through solving this challenge:
1.cookies

## Other incorrect methods you tried:
no 

## References
- i learned about cookies in the oasis so i dont remember the references 
# SOAP

**Flag:** `picoCTF{XML_3xtern@l_3nt1t1ty_e5f02dbf}`

## How you approached the challenge:
I used the hint.Then i searched for `xml external entity injection` and i went to a site `https://portswigger.net/web-security/xxe` I learned about the `xml` and 
differenct types of xml.Then i found the `Exploiting XXE to retrieve files`   where i studied about how to retrieve the` /etc/passwd file` by submitting the an  XXE payload and the challenge also said `Can you read the /etc/passwd file?`.The xxe payload was 
```bash
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck><productId>&xxe;</productId></stockCheck>
```
Then i went on the site and left clicked,went to inspect and the networks and then clicked on the details options under the picoctf panel which send a post request 
then i right clicked on that request and clicked ` edit and resend ` and i changed the payload to the one mentioned above with some changes 
the new payload which i sent :
```bash
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<data><ID>&xxe;</ID></data>
```
and then i clicked on the response page and i got the flag.
![image](https://github.com/user-attachments/assets/78f03982-7446-4b79-a90d-3b8f70a71170)


## What you learned through solving this challenge:

1. xxe (xml external entity injection 

## Other incorrect methods you tried:
1. I tried this challenge at the beginning of the tp and could not do it so i left this challenge.This time i could do the challenge in the first try but before
i tried the same thing and i could not get a response and i even installed burp suite and tried to capture the network packet sent and tried to send my own payload
but couldnt get a response but now i got it and i dont know why . I also saw video on how to send a network packet on burp suit and in a firefox brower when i first tried this challenge

## References
- https://portswigger.net/web-security/xxe

# PcapPoisoning

**Flag:** `picoCTF{P64P_4N4L7S1S_SU55355FUL_fc4e803f}`

## How you approached the challenge:
I first downloaded the file given in the challenge and i was a pcap file (packet capture) so i opened wireshark and opened the file there.Then i was going throught the traffic and then i saw a transmission from a different source and destination and its payload was readable and it was the flag.
![image](https://github.com/user-attachments/assets/1edf9ce7-58d0-4f6a-a91f-7fa6efa2804e)

## What you learned through solving this challenge:
1. wireshark
## Other incorrect methods you tried:
none

## References
no references
