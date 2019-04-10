


# ctf-dawg

> Bastich _aka_ Lobo Bastich - 2019

<hr>
A place for CTF information, mostly related to challenges, tools and tricks to hopefully make solving these fraggin things a little easier. The idea will be to have two to three sections respectivley (example: low hanging fruit, challenging and wtf_even), per topic and/or tool. This could change at anytime...

<hr>

#### Setup / Preperation

> Ready, Set, ...

* Fire up one of your preferred search engines that is always available through out the CTF (so best in a seperate window/browser on a seperate screen if you have that setup, or as a new tab in your browser). I normally use a lower resource browser for this task example: [Midori](https://www.midori-browser.org/download/) or [Iridium](https://iridiumbrowser.de/) so you can leave it open at all times and that is it's only purpose.

* Next is main browser tab setup, this almost always consists of the following services or resources, that have come to the rescue more than I dare to count. 
	* For **crypto** related things [cryptii](https://cryptii.com/), [dcode](https://www.dcode.fr/) and [tio](https://tio.run/) this last one is amazing for esoteric languages.
	* For **payloads** and **shellcode** related things [payloadsallthethings](https://github.com/swisskyrepo/PayloadsAllTheThings), [shell-strorm](http://shell-storm.org/shellcode/)
	* For **forensic** related tasks [file headers](https://www.garykessler.net/library/file_sigs.html), [hexedit online](https://hexed.it/) this last one is normally only used for quick data inspection or identification.
	* For **pwn** and **reversing** related things, if you don't have a debugger/disassembler for some reaaon the [online disassembler](https://onlinedisassembler.com) is an awesome tool or there is also [online gdb](https://www.onlinegdb.com/) for debugging etc.

* Last is app or browser tab connection to the related social media of CTF organisers or good CTF player channels, the main one that is always open is [JHDiscord](https://discordapp.com/invite/UU3WQdf) - John Hammond's discord server, also make sure you checkout his [ctf-katana](https://github.com/JohnHammond/ctf-katana) a ctf guide that this very guide is enspired by.

##### CTF Start

> First things first...

* Hit the terminal hard with mkdir -p (create parent path at the same time) to get all the section and challenges down as directories, normally under liveCTF dir.

	* > mkdir -p \<thectfname\>/\<challengesection\>, example: mkdir -p picoCTF19/crypto
   
* Same goes for the actual challenges and their descriptions (just as simple text files) plus any related files, this helps tremendeously when the system goes down (it happens way to often, just think of the 100's of hackers chucking fuzzers and scrapers at all of the things ;)

	* > mkdir -p \<challengesection\>/\<challenge\>, example: mkdir -p crypto/caesar_lives
	* > download or create related files for the challenge, example: ciphertext.txt
   
* Read the rules (normally contains a flag for easy starter points)
* Connect to organisers social media (again most always contains a flag for easy points) and provides hints and tips
* Fire up your playlist, example [defcon-26](https://defconcommunications.bandcamp.com/album/def-con-26-the-official-soundtrack) and settle in for the long haul
<hr>

# Crypto

> Cryptographia epistolica, sive de clandestina scriptione - Erycius Puteanus (1574 - 1646)

###### `Low Hanging Fruit`

* One of the most commonly used is [base64](https://en.wikipedia.org/wiki/Base64) encoding, easily identifiable by the use of the = (equal) sign as padding, these padding characters might be added to make the last encoded block contain four Base64 characters. The encoded text is also produced using \[a-s,A-Z,0-9\] only and could not contain the padding =  if the encoded text matches the 4 byte encoding rule. There will normally be some sort of hint towards the encoding or cipher used, example *bastich is 64 years old but still calls his mother*

	* > bDAwayBtNCAxbSAxMzM3IEFGIQ== \<<decoded\>> l00k m4 1m 1337 AF!
	* > using linux terminal to decode echo -n bDAwayBtNCAxbSAxMzM3IEFGIQ== | base64 -d
	* > or there are 100s of encoders/decoders online like [cryptii base64-to-text](https://cryptii.com/pipes/base64-to-text)

* If base64 don't work try [base32](https://en.wikipedia.org/wiki/Base32) or [base85/ascii85](https://en.wikipedia.org/wiki/Ascii85) although the encoded text will look different from the base64 text, as seen below using the examples for *l00k m4 1m 1337 AF!*:
	
	* > NQYDA2ZANU2CAMLNEAYTGMZXEBAUMII= \<<decoded\>> l00k m4 1m 1337 AF! - base32 encoded
	* > CbRPY+DiqX0l8$f1G^s45t3! \<<decoded\>> l00k m4 1m 1337 AF! - base85/ascii85 encoded
<hr>	

**NB:** Don't be fooled by the aes-128-cbc-hmac-sha1 cipher, as it looks just like base64 encoded text - MNb8BzccxHIVhuJ414jkikhPGtwyR2If3KOj5aKe1yE=  --- *l00k m4 1m 1337 AF!* ciphered with private key \[sameasbase64\].
<hr>

* Decimal type encoding is another commonly used crypto type for the easy pointers, this will include **deciaml**, **hexadecimal**, **binary** and **ascii chars** to name a the most used, 100s of decoders are available online again [cryptii](https://cryptii.com/) to the rescue, examples for *l00k m4 1m 1337 AF!*:

	* > 108 48 48 107 32 109 52 32 49 109 32 49 51 51 55 32 65 70 33 - Decimal base 10 
	* > 1101100 110000 110000 1101011 100000 1101101 110100 100000 110001 1101101 100000 110001 110011 110011 110111 100000 1000001 1000110 100001 - Binary base 2
	* > 6c 30 30 6b 20 6d 34 20 31 6d 20 31 33 33 37 20 41 46 21 - Hexadecimal base 16
	* > 154 60 60 153 40 155 64 40 61 155 40 61 63 63 67 40 101 106 41 - Octal base 8
  
* Another two encodings, that are commonly used but a bit obscure (visually) are [morse code](https://en.wikipedia.org/wiki/Morse_code) and [braille](https://en.wikipedia.org/wiki/Braille), again decoders can be found online. The best I found for morse code is [scphillips](https://morsecode.scphillips.com/translator.html) this even has the ability to do audio files. For braille you can use [dcode](https://www.dcode.fr/braille-alphabet), examples for *l00k m4 1m 1337 AF!*:

	* > ⠇⠼⠚⠼⠚⠅ ⠍⠼⠙ ⠼⠁⠍ ⠼⠁⠼⠉⠼⠉⠼⠛ ⠁⠋⠖ - braille (international)
	* > .-.. ----- ----- -.- / -- ....- / .---- -- / .---- ...-- ...-- --... / .- ..-. -.-.-- / - morse code
  
* [Keyboard shift cipher](https://www.dcode.fr/keyboard-shift-cipher) is another well used one, shifting the letters either right, left, up or down any number of times results in some rather random text, example for *l00k m4 1m 1337 AF!*:

	* > ;--l ,5 2, 2448 SG@ - shifted right once
  
* Reverse text can be an easy one to catch people out and send them down the rabbit hole, example for *l00k m4 1m 1337 AF!*:

	* > !FA7331m14mk00l - reversed and stripped
	* > easy way to reverse text with python - ```print("!FA7331m14mk00l"[::-1])```
	* > easy way to reverse text in ruby - ```puts "!FA7331m14mk00l".reverse```
  
* Substitution, Caesar or Atbash monoalphabetic cipher uses a single fixed substitution across the entire text resulting in a good cipher but easily reversed, the best tool for it is [quipquip](https://quipqiup.com/) or [dcode](https://www.dcode.fr/monoalphabetic-substitution) has some good options for bruteforcing the ciphertext with various options, example for *l00k m4 1m 1337 AF!*:

	* > S00Q D4 1D 1337 AY! - substitution using AZERTYUIOPQSDFGHJKLMWXCVBN
	* > oCCn p7 4p 4660 DI! - caesar shifted 3 times with \[a-z\]\[A-Z\]\[0-9\]
	* > k99i k2 Xj XYY3 6A! - decreasing shift (-1,-2,-3,-4)
  
* This brings us to ROT13 basically a Caesar cipher shifting 13 times (normally shifted 5 on numbers), the shift is across the entire text so easily deciphered using [dcode](https://www.dcode.fr/rot-13-cipher), example for *l00k m4 1m 1337 AF!*:

	* > y55x z9 6z 6882 NS! - shifted 13 times on (a-z) and 5 on (0-9)
	
* Then there is of course [ROT47](https://rot47.net/), same as ROT13 but has the addition to scramb basic letters, numbers and common symbols rather than just the standard alphabet.

	* > =__\< \>c \`\> \`bbf puP - rot47 encoded l00k m4 1m 1337 AF!
  
###### `Challenging`

* [Vigenere Cipher](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher), cipher encrypting text using a series of Caesar ciphers, based on the letters of a defined keyword. It is a form of polyalphabetic substitution a whole new game change from the simple monoalphabetic substitution, [cryptii](https://cryptii.com/pipes/vigenere-cipher) is a good start or [dcode](https://www.dcode.fr/vigenere-cipher), example for *l00k m4 1m 1337 AF!*:

	* > m0R4 u6 8n 1KLE CM! - ciphered with \[A-Z\]\[0-9\] variant, key = bastich (repeating)
  
* [Enigma machine](https://en.wikipedia.org/wiki/Enigma_machine), this only just does not make the wtf_even group, purley for the fact that we have computers to help solve the cipher. Even with all the computing power in the world it is still mostly a manual task for CTF, unless you have access to some supercomputers and can code like a beast. It does work better on longer text and no numbers so here is the example for look ma im leet AF!*7:

	* > pgrr kx aa ztzp cd!inca lf ac cgtg jt!otsy th ta dgud or!jaxj vd oi rsyk bp!sqpb et qy ktrb kx!ydne so jx mzsd fl!eamb zj bs ozca lq! - Enigma M3, reflector = UKW B, rotor1 = \[VI,1,1\], rotor2 = \[I,17,1\], rotor3 = \[III,12,1\], plugboard = bq cr di ej kw mt os px uz gh, foreign chars = include - decoder [cryptii](https://cryptii.com/pipes/enigma-machine)
  
* [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) ECB (Electronic Codebook) is best described as the BSQLi of the crypto world, in that you can bruteforce the key it being the first generation of AES. CBC (Cipher Blocker Chaining) is an advanced form of block cipher encryption, and that is in the wtf_even section below. ECB example for *l00k m4 1m 1337 AF!* encryption/decryption at [devglan](https://www.devglan.com/online-tools/aes-encryption-decryption)

	* > 53FF897C204A5E841B64BC516F98BDF09DA7DC32A38AE6521EE78A00E34815CB - ECB 128bit / using plaintext secret key = bastich (repeating to 16)
  
###### `wtf_even`

* [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) CBC (Cipher Blocker Chaining) is an advanced form of block cipher encryption that uses two keys and each cipher block is dependent on all the data blocks being used up to that point, read the wiki link for a more indepth and better explanation. CBC example for *l00k m4 1m 1337 AF!* encryption/decryption at [devglan](https://www.devglan.com/online-tools/aes-encryption-decryption)

	* > D5A9BD786FD06E7347639750699CF718E3BB3668A5608C45E9E6201DD6147585 - CBC 256bit / IV key = !l00km41m1337AF!, secret key = bastichbastichbastichbastichbast (32)

<hr>

## Crypto - Esoteric Languages	

> Restricted to or intended for an enlightened or initiated minority, esp because of abstruseness or obscurity - British meaning (Collins English Dictionary)

* By far the best and most comprehensive tools for esoteric languages has to be [Try It Online](https://tio.run/#) with the ability to interpret over a 637 languages, it remains at the top as a CTF tool.

* Some of the more commonly used [esolangs](https://esolangs.org/wiki/Language_list) in CTFs :
* [2DFuck](https://gitlab.com/TheWastl/2DFuck) - Often mistaken for a muted version of morse code
	* > .!.!..!.!....!..!..!.!.!.!.!..!.!..!...!..!.!..!...!..!.!....!..!.!.!..!....!.!......!.!.!.!.!...!.!..!.!....!.!...!..!.!..!..!.!..!...!..!..!.!....!.!....!. - translates to Hello World!
* [3var](https://esolangs.org/wiki/3var) - esolang inspired by Deadfish, makes use of 3 variables, 2 for accumelators and the other for results. Identifiable by the heavy use of i and d and P :
	* > iisssaa/>emaa->e#aamam->e#dddddddddddddddddddddddddPiiiiiiiiiiiiiiiiiiiiiiiiiiiiiPiiiiiiiPPiiiPriissaa*>iiiiiiiiiiiiPriisaamaaaa*>Priisssaa/>emaa->e#aamam->e#ddddddddddPiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiddddddddPiiiPddddddPddddddddPriissaa*>iP - translates to Hello World!
* [;#+](https://github.com/ConorOBrien-Foxx/shp)  - shp is the same as ;# (semicolon hash) but Turing complete, meaning it has a one-to-one comparision to brainfuck
	* > ;;;;;;;;;~++++++++>#<+++;;:>#<+-;;>#<#<-;;;>#<-+++++++;;;;-:>#<-+;;;#::<;;;-++#:<#<;;;#-<;;;#<+;;#-:<-+;;# - translates to Hello World!
* [Beatnik](https://esolangs.org/wiki/Beatnik) - a stack based esolang, where the words are scored according to the scrabble board which in turn determines the operation for the stack.
	* > K QQQQQQQG ZD XO K QQJA KD ZD XO K KG KD ZD ZD ZD XO XO K B KD ZD XO K QQQQF ZD ZD XO K QQQD XO K A Z KD XO ZD XO K B KD XO ZD XO K J Z XO K QQQB XO - translate to Hello World!
* [brainfuck](https://esolangs.org/wiki/Brainfuck) - probably the most famous and popular esolang used in CTF world, orginally created to make the smallest possible compiler on Amiga OS (only 240 bytes, Holy Fuck!) 
	* > --<-<<+[+[<+>--->->->-<<<]>]<<--.<++++++.<<-..<<.<+.>>.>>.<<<.+++.>>.>>-.<<<+. - translates to Hello World!
* [commentator](https://github.com/cairdcoinheringaahing/Commentator) - designed to fit well with polygots using common comment characters.
	* > \                                                                        /*#                                                                                                     /*#                                                                                                            /*#                                                                                                            /*#                                                                                                               /*#                                            /*#                                /*#                                                                                       /*#                                                                                                               /*#                                                                                                                  /*#                                                                                                            /*#                                                                                                    /*#                                 /*# - translates to Hello World!
* [cow](https://bigzaphod.github.io/COW/)  -  designed with bovine in mind and the fact they have such a limited vocab, it seemed the most logical way to communicate.
	* > MOo MOo MOo moO MOo moO MOo moO moO MoO moO MoO moO moO MoO MOO MoO MoO MoO MoO MOO moO MoO MoO MoO MOO moO MoO MoO MoO MoO moO MOo MOo moO MoO MoO MoO mOo mOo mOo MOo moo mOo MOo moo mOo MoO MoO MoO moo moO moO moO Moo moO MOo MOo moO MOo Moo moO Moo Moo MoO moO MoO MoO MoO MoO moO MoO MoO MoO Moo MoO moO MOo MOo moO MOO moO MOo Moo mOo mOo moo - translates to Hello World!
* [cubically](https://github.com/aaronryank/cubically) - esolang based on the Rubik's cube
	* > +53@6+1F2L2+0@6L2F2U3R3F1L1+2@66L3F3R1U1B3+0@6:4U1R1+00@6-000@6+50000@6+000000@6+2-000000@6-5+4000@6-00@6/0+00@6:0+0/0+00@6
* [deadfish~](https://esolangs.org/wiki/Deadfish~) - Super-set of the Deadfish esolang that contains implementations of more than 65 different programing languages including Basic, C, C++ and C#
	* > iisiiiisiiiiiiiiciiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiciii{c}dddddddddcdddddddciiiiiiiiiicdddddddc
Horrrrrrrrrrible , o , w - translates to Hello World!
* [emojifuck](https://github.com/Romulus10/emotif___) - emojified version of brainfuck 
	* > 😂😂😂😂😂😂😂😂🌚🔥😂😂😂😂🌚🔥😂😂🔥😂😂😂🔥😂😂😂🔥😂💯💯💯💯💩🐸🔥😂🔥😂🔥💩🔥🔥😂🌚💯🐸💯💩🐸🔥🔥💞🔥💩💩💩💞😂😂😂😂😂😂😂💞💞😂😂😂💞🔥🔥💞💯💩💞💯💞😂😂😂💞💩💩💩💩💩💩💞💩💩💩💩💩💩💩💩💞🔥🔥😂💞🔥😂😂💞 -translates to Hello World! 
* [eta](http://www.miketaylor.org.uk/tech/eta/doc/) - esolang to resemble natural latin based languages
	* > NINENAHAENATOENAAAENATSENTNOENIIENSAENATSENATOENATOENAHOENTOAEOOOOOOOOOOOOO - translates to Hello World!
* [explode](https://github.com/stestoltz/Explode) -  esolang based on WIP tape, meaning that every access attempt has its access index modulated by the length of the tape, so you cannot attempt to read outside the tape.
	* > @1_0+E 
@1_0+17 
@1_0+1e 
@1_0+1e 
@1_0+1h 
@1_0+c

	* >@1_0+T 
@1_0+1h 
@1_0+1k 
@1_0+1e 
@1_0+16 
@1_0+1 - translates to Hello World!	  	  	

* [forked](https://github.com/aaronryank/Forked) - stack based two-dimensional esolang, triangulated and wriiten around the fork command.
	* > 89*@AA*i@7+@@3+@P4B*@C'!F+!U@3+@6'@8'@3B*!& - translates to Hello World!



