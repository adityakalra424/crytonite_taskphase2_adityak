# `DISCLAIMER`
I COULDNT SOLVE ANY CHALLENGES IN THE NITECTF COMPETITION
##  Backtrack from misc 
Kenji is a nice guy who lives in Tokyo. He is in a dilemma. In 2017, he was late to an important meeting and is now facing repercussions. To defend himself, he needs to prove that it was not his fault. His evidence? The train he boarded that day, traveling between Omotesandō and Suitengumae, was delayed. However, his boss is not providing the specific details of the accusation. Kenji vividly remembers one key fact: the train was around 61 minutes late.
Help him uncover the exact date of the incident and the start time of the delay. Justice for Kenji!
Flag Format: nite{time_date} Example: nite{13:00_3January}
### Till where i reached 
I searched for the line that connected the two stations and i got the hanzomon line from that.Then i got to know about the delay certificates of the trains that get
delayed and then i went on the site of `tokyometro.jp` but the website had the info of approximately the last month and then i got stuck for a while and then a
teammate solved the challenge.
### Solution 
After going to the `tokyometro.jp`,The question asks for the information which dates back to 2017.
As no other information is publicly available for 2017, we can go to the `Wayback Machine Archive`, copy the Hanzomon Delay Certificate link and paste it.
### learning 
`The wayback machine archive `: it is a digital archive of the World Wide Web 
## flight risk from rev 
### till where i reached 
i couldnt solve a thing in this challenge
### solution 
i had to decompile the game using `Il2cppdumper` and look for `TerrainGenerator.cs` and ` Missile.cs` and then open the `GameAssembly.dll` then on IDA and 
patch `TerrainGenerator` class to set heights to 0 and then modify the `Missile` class to `nop` calls to SpawnMissile function.
### learning 
i learned about `Il2cppdumper`:Il2cppDumper is a tool used for dumping and analyzing IL2CPP-compiled games and applications,IL2CPP is a technology developed by Unity, a popular game engine
i learned how to solve a challenge where a game is involved,i had to change the code of the game for me to get the flag

