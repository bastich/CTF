# ctf-dawg

> Bastich _aka_ Lobo Bastich - 2019

<hr>
A place for CTF information, mostly related to challenges, tools and tricks to hopefully make solving these fraggin things a little easier. The idea will be to have two to three sections respectivley (example: low hanging fruit, challenging and wtf_even), per topic and/or tool.

<hr>

#### Setup / Preperation

> Ready, Set, ...

* Fire up one of your preferred search engines that is always available through out the CTF (so best in a seperate window/browser on a seperate screen if you have that setup, or as a new tab in your browser). I normally use a lower resource browser for this task example: [Midori](https://www.midori-browser.org/download/) or [Iridium](https://iridiumbrowser.de/) so you can leave it open at all times and that is it's only purpose.

* Next is main browser tab setup, this almost always consists of the following services or resources, that have come to the rescue more than I dare to count. 
  * For **crypto** related things [cryptii](https://cryptii.com/), [dcode](https://www.dcode.fr/) and [tio](https://tio.run/) this last one is amazing for esoteric languages.
  * For **payloads** and **shellcode** related things [payloadsallthethings](https://github.com/swisskyrepo/PayloadsAllTheThings), [shell-strorm](http://shell-storm.org/shellcode/)
  * For **forensic** related tasks [file headers](https://www.garykessler.net/library/file_sigs.html), [hexedit online](https://hexed.it/) this last one is normally only used for quick data inspection or identification.

* Last is app or browser tab connection to the related social media of CTF organisers or good CTF player channels, the main one that is always open is [JHDiscord](https://discordapp.com/invite/UU3WQdf) - John Hammond's discord server, also make sure you checkout his [ctf-katana](https://github.com/JohnHammond/ctf-katana) a ctf guide that this very guide is enspired by.

##### CTF Start

> First things first...

* Hit the terminal hard with mkdir -p (create parent path at the same time) to get all the section and challenges down as directories, normally under liveCTF dir.

   * > mkdir -p \<thectfname\>/\<challengesection\>, example: mkdir -p picoCTF19/crypto
   
* Same goes for the actual challenges and their descriptions (just as simple text files) plus any related files, this helps tremendeously when the system goes down (it happens way to often, just think the 100's of hackers chucking fuzzes and scrapers at the all the things ;)

   * > mkdir -p \<challengesection\>/\<challenge\>, example: mkdir -p crypto/caesar_lives
   * > download or create related files for the challenge, example: ciphertext.txt
   
* Read the rules (normally contains a flag for easy starter points)
* Connect to organisers social media (again most always contains a flag for easy points) and provides hints and tips
* Fire up your playlist [defcon-26](https://defconcommunications.bandcamp.com/album/def-con-26-the-official-soundtrack) and settle in for the long haul
<hr>

# Crypto

> Cryptographia epistolica, sive de clandestina scriptione - Erycius Puteanus (1574 - 1646)

###### `Low Hanging Fruit`

* One of the most commonly used is [base64](https://en.wikipedia.org/wiki/Base64) encoding, easily identifiable by the use of = signs as padding, these padding characters might be added to make the last encoded block contain four Base64 characters. There will normally be some sort of hint towards the encoding or cipher used, example *bastich is 64 years old but still calls his mother*

  * > bDAwayBtNCAxbSAxMzM3IEFGIQ== \<<decoded\>> l00k m4 1m 1337 AF!
  * > using linux terminal to decode echo "bDAwayBtNCAxbSAxMzM3IEFGIQ==" | base64 -d
  * > or there are 100s of decoders online like [cryptii base64-to-text](https://cryptii.com/pipes/base64-to-text)

* Decimal type encoding is another commonly used crypto type for the easy pointers, this will include **deciaml**, **hexadecimal**, **binary** and **ascii chars** to name a the most used, 100s of decoders are available online again [cryptii](https://cryptii.com/) to the rescue, examples for *l00k m4 1m 1337 AF!*:

  * > 108 48 48 107 32 109 52 32 49 109 32 49 51 51 55 32 65 70 33 - Decimal base 10 
  * > 1101100 110000 110000 1101011 100000 1101101 110100 100000 110001 1101101 100000 110001 110011 110011 110111 100000 1000001 1000110 100001 - Binary base 2
  * > 6c 30 30 6b 20 6d 34 20 31 6d 20 31 33 33 37 20 41 46 21 - Hexadecimal base 16
  * > 154 60 60 153 40 155 64 40 61 155 40 61 63 63 67 40 101 106 41 - Octal base 8
  
* Another two basic encodings used that are a bit obscure (visually) are [morse code](https://en.wikipedia.org/wiki/Morse_code) and [braille](https://en.wikipedia.org/wiki/Braille), again decoders can be found online. The best I found for morse code is [scphillips](https://morsecode.scphillips.com/translator.html) this even has the ability to do audio files. For braille you can use [dcode](https://www.dcode.fr/braille-alphabet), examples for *l00k m4 1m 1337 AF!*:

  * > ⠇⠼⠚⠼⠚⠅ ⠍⠼⠙ ⠼⠁⠍ ⠼⠁⠼⠉⠼⠉⠼⠛ ⠁⠋⠖ - braille (international)
  * > .-.. ----- ----- -.- / -- ....- / .---- -- / .---- ...-- ...-- --... / .- ..-. -.-.-- / - morse code
  
* [Keyboard shift cipher](https://www.dcode.fr/keyboard-shift-cipher) is another well used one, shifting the letters either right, left, up or down any number of times results in some rather random text, example for *l00k m4 1m 1337 AF!*:

  * > ;--l ,5 2, 2448 SG@ - shifted right once
  
* Reverse text can be an easy one to catch people out and send them down the rabbit hole, example for *l00k m4 1m 1337 AF!*:

  * > !FA7331m14mk00l - reversed and stripped
  * > easy way to reverse text with python - ```print("!FA7331m14mk00l"[::-1])```
  * > easy way to reverse text in ruby - ```puts "!FA7331m14mk00l".reverse```
  
* Substitution, caesar or atbash monoalphabetic cipher uses a single fixed substitution across the entire text resulting in a good cipher but easily reversed, the best tool for it is [quipquip](https://quipqiup.com/) or [dcode](https://www.dcode.fr/monoalphabetic-substitution) has some good options for bruteforcing the ciphertext with various options, example for *l00k m4 1m 1337 AF!*:

  * > S00Q D4 1D 1337 AY! - substitution using AZERTYUIOPQSDFGHJKLMWXCVBN
  * > oCCn p7 4p 4660 DI! - caesar shifted 3 times with \[a-z\]\[A-Z\]\[0-9\]
  * > k99i k2 Xj XYY3 6A! - decreasing shift (-1,-2,-3,-4)
  
* This brings us to ROT13 basically a caesar cipher shifting 13 times (normally shifted 5 on numbers), the shift is across teh entire text so easily deciphered using [dcode](https://www.dcode.fr/rot-13-cipher), example for *l00k m4 1m 1337 AF!*:

  * > y55x z9 6z 6882 NS! - shifted 13 times on (a-z) and 5 on (0-9)
  
