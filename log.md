# CodeMash 2020 Capture the flag
# Write-up for solutions

### 100 POINT CHALLENGES

### 1. All your base are belong to us! 
**Y20yMC00bGwteTB1ci1iNDUzLTRyMy1iM2wwbjYtNzAtdTU=**

**Getting started** 
The first thing to figure out was that the Flags start with cm20. I used an online tool and was decoding different formats and it all looked like gibberish. 

**What I learned**  
How to recognize Base64. Base64 is lengths of 4 characters. Every character is in the sets A-Z, a-z, 0-9, +, / except for padding at the end which is 0, 1 or 2 "=" characters. Since this ends with an = and doesn't have any other alphanumeric chars it seemed like a good thing to check. Used this [Base64 Decoder](https://www.base64decode.org/).

**Solution** 
cm20-4ll-y0ur-b453-4r3-b3l0n6-70-u5

### 2. These soundex exactly the same
**Their he'll pare; There heal pair; They're heel pear**
The key format for this challenge is cm20-xxxx-xxxx-xxxx

**Getting started** 
Since it said "soundex" rather than "sound", I figured that was a clue.

**What I learned**
Soundex is a SQL expression. The SOUNDEX() function accepts a string and converts it to a four-character code based on how the string sounds when it is spoken. This was perfect since I knew I needed 3x 4 digit codes, and each expression "sounds the same" so each 1st word should have an identical "soundex code". Using this website [Try SQL Server](https://www.w3schools.com/sql/trysqlserver.asp?filename=trysql_func_sqlserver_soundex), I was able to put in "Their", "heal", and "pair" to get the solution.

**Solution** 
cm20-T600-H400-P600

### 3. Where's the Bacon
**CCCMCCMCMM20-CCCCMCCCCCCCCMCCMMCMCMMCC-MCCMCCCCCCMCCCMMCCMCCCMCCMCCCM-CCCCMCCMCCMCCMCMCCMCCCMCCMCCCC-CCCCCMCCMC-CCCMCCMMCMCCCMMCCMCCCMCMMCCCCCMCCCMCCMMM**

**Getting started** 
OK, I didn't know the bacon cipher was a thing. Thanks google.

**What I learned**  
This decoding website is great. I could just say that the first letter was C and the 2nd was M and it deciphered it: [DCode Bacon Cipher](https://www.dcode.fr/bacon-cipher). This was also nice for summarizing how it works: [Bacon Cipher explanation](https://github.com/mathiasbynens/bacon-cipher)

**Solution** 
CM20-BACON-TASTES-BETTER-AT-CODEMASH
