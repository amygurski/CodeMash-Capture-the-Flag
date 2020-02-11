# CodeMash 2020 Capture the flag
I participated in the capture the flag challenge at CodeMash 2020. 

A Capture The Flag competition is a technological puzzle game played online, that requires research to capture the flags and learn about technology. By doing these challenges, I learned a lot and it enhances my CodeMash experience because it brought me together with some cool people there who also enjoy a challenge.

For a brief while, I was on the top 10 list, and I really like how my curve - the yellow one - is "gradual" - it shows how I was struggling and learning for each one (whereas others wizzed through them!). I'm so excited to bring what I learned to next years' CTF!

![Leaderboard](https://github.com/amygurski/CodeMash-Capture-the-Flag/blob/master/img/ctf%20leaderboard.PNG)

# Write-up for solutions

### ACCESS CONTROL
 
### We got the password dump (100)
**Getting started**
These were the passwords:
97b6b44323b5e0748e84c198025a772d
b49add72074b0ba72357b068035b4676
a37a67d2cd38a3ac9ea27b1215002b99
4259eb9ea37f3ba630d82ac7dd50e44b

I started with Google, big surprise, and stumbled on a [password hash cracker](https://crackstation.net/). Pasting them in identified them as MD5 type and gave the result.

**What I learned**
The term "password hash" and I found the Wikipedia page on [MD5](https://en.wikipedia.org/wiki/MD5) to be an interesting read.

**Solution**
cm20-rev3-rs1n-gpwd

### BINARY ANALYSIS

### Need more coffee!!! (100)
**Getting Started**
The file just said "RunMe" with no extension, so I used this website to check the extension:
[CheckFileType](http://checkfiletype.com/)

This identified it as a: File Type: compiled Java class data, version 52.0.

I added the .class extension. This enabled me to run it using Bash by typing "java RunMe"

**What I learned** 
The file identifier tool and running Java class files.

**Solution**
cm20-cafe-babe

### ENCODING

### All your base are belong to us! (100)

Hint: **Y20yMC00bGwteTB1ci1iNDUzLTRyMy1iM2wwbjYtNzAtdTU=**

**Getting started** 
The first thing to figure out was that the Flags start with cm20. I used an online tool and was decoding different formats and it all looked like gibberish. 

**What I learned**
How to recognize Base64. Base64 is lengths of 4 characters. Every character is in the sets A-Z, a-z, 0-9, +, / except for padding at the end which is 0, 1 or 2 "=" characters. Since this ends with an = and doesn't have any other alphanumeric chars it seemed like a good thing to check. Used this [Base64 Decoder](https://www.base64decode.org/).

**Solution** 
cm20-4ll-y0ur-b453-4r3-b3l0n6-70-u5

### These soundex exactly the same (100)
Hint: **Their he'll pare; There heal pair; They're heel pear**

**Getting started** 
Since it said "soundex" rather than "sound", I figured that was a clue.

**What I learned**
Soundex is a SQL expression. The SOUNDEX() function accepts a string and converts it to a four-character code based on how the string sounds when it is spoken. This was perfect since I knew I needed 3x 4 digit codes, and each expression "sounds the same" so each 1st word should have an identical "soundex code". Using this website [Try SQL Server](https://www.w3schools.com/sql/trysqlserver.asp?filename=trysql_func_sqlserver_soundex), I was able to put in "Their", "heal", and "pair" to get the solution.

**Solution** 
cm20-T600-H400-P600

### All your base belong to us - level 2 (300)
**Getting Started**
After the level 1 challenge, I was ready for Base64! Decoding it I saw the file started with PNG. I found a [Base64 to PNG converter](https://onlinepngtools.com/convert-base64-to-png) and sure enough a flag was on the image.

![All your bases 2 Flag](https://github.com/amygurski/CodeMash-Capture-the-Flag/blob/master/img/all-your-bases-2-result.png)

### All your base belong to us - level 2 (300)
**Getting Started**
This was also recognizable as base 64, but more challenging. The end of the file had "fish". Removing it allowed it to the Base64 decoded. However, the result was still Base 64 and it still had "fish" at the end. I kept decoding and removed fish anytime fish was at the end. After 42 times (!!!!) it decoded down to just the flag. 

**What I learned**
At this point, I am pretty comfortable recognizing Base64. It was just a case of believing I was on the right track to do it 42 times!!! Also, it clearly would have been better to write a script to do it!

**Solution**
cm20-7h4nk5-f0r-4ll-7h3-f15h

### ENCRYPTION

### Where's the Bacon (100)
Hint: **CCCMCCMCMM20-CCCCMCCCCCCCCMCCMMCMCMMCC-MCCMCCCCCCMCCCMMCCMCCCMCCMCCCM-CCCCMCCMCCMCCMCMCCMCCCMCCMCCCC-CCCCCMCCMC-CCCMCCMMCMCCCMMCCMCCCMCMMCCCCCMCCCMCCMMM**

**Getting started** 
OK, I didn't know the bacon cipher was a thing. Thanks google.

**What I learned**  
The decoding website is great. I could just say that the first letter was C and the 2nd was M and it deciphered it: [DCode Bacon Cipher](https://www.dcode.fr/bacon-cipher). This was also nice for summarizing how it works: [Bacon Cipher explanation](https://github.com/mathiasbynens/bacon-cipher)

**Solution** 
CM20-BACON-TASTES-BETTER-AT-CODEMASH

### What is missing? (200)
**Getting started**
This one was an HTML file with a poem. I was comfortable with looking at HTML source code so I got on the right track quickly:
![Bacon Poem](https://github.com/amygurski/CodeMash-Capture-the-Flag/blob/master/img/whatismissingpoem.PNG)

**What I learned**
The trick here was realizing Francis Bacon was a clue, which seems so obvious now. Then knowing the Bacon cipher is 2 letters, I could see that it was the HTML tags for Bold and Italic. Copying those into the same [DCode Bacon Cipher](https://www.dcode.fr/bacon-cipher) did the trick.

### MOBILE

### Why did you do this to us, iOS?
**Getting started**
I messed around with this one a bit before I looked at it in VS Code and found these lines in info.PLIST:
 <key>Flag</key>
 <string>13 23 92 90 87 21 93 35 95 87 29 30 90 28 87 14 91 24 11 87 26 22 29 30</string>
 Knowing it started with CM20, I was able to work out that I needed to add 54 or subtract 42 to get the hexidecimal number:
 67 77 50 48 45 75 51 89 53 45 83 84 48 82 45 68 49 78 65 45 80 76 83 84
 
**What I learned**
ASCII to char conversions. At first, I started by looking at ASCII tables and figuring out the pattern. Once I had done the shift, this tool did the rest of the work: [Decimal to ASCII](https://onlineasciitools.com/convert-decimal-to-ascii)

**Solution**
CM20-K3Y5-ST0R-D1NA-PLST

##On Site Challenge

### You are going to need a broom (1000)
**Getting started**
Thankfully there was a reference to a scytale. There was also a mysterious broom propped in the corner of the boardgame room near the strip of paper. Wrapping it around the broom, it was clean the numbers lined up-ish. I wrote them down and messed with them til around midnight to no avail. The next morning, the broom was gone! I told Bill Sempf and he located it and made a note that it was for CodeMash. Some more careful wrapping of the hint around the broom revealed the answer.

**What I learned**
This was the start of being more social with the CTF. I wound up working on it with someone and we got SO close. This one was in Hex Code:
63 6d 32 30 2d 
69 73 65 65 2d 79 6f 75 66 2d 6f 75 6e 64
Putting it into a Hex to ASCII converter yielded the results: [Hex to ASCII converter](https://www.rapidtables.com/convert/number/hex-to-ascii.html)

**Solution**
cm20-isee-youf-ound
