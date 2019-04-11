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
* [fractan](https://github.com/DennisMitchell/ffi) - FFI is an interpreter for the Turing tarpit FRACTRAN
	* > (3^72*5^101*7^108*11^108*13^111*17^44*19^32*23^87*29^111*31^114*37^108*41^100*43^33)/2! - translates to Hello World!
* [grass](http://www.blue.sky.or.jp/grass/) - is based on lambda calculus, not Turing machine (brainfuck) and is very easily slipped in to ascii art.
	* > 　　　　_, ._
　（　・ω・）　んも〜
　　○=｛=｝〇,
　 　|:::::::::＼, ', ´
､､､､し ､､､((（.＠）ｗｖｗｗＷＷｗｖｗｗＷｗｗｖｗｗｗｗＷＷＷｗｗＷｗ
* [hspal](https://esolangs.org/wiki/Hexadecimal_Stacking_Pseudo-Assembly_Language) - Data is stored as 16-bit unsigned integers in up to 256 unbounded-capacity stacks and a single register.
	* > 20002140000020006440000020006C40000020007240000020006F40000020005740000020002040000020002C40000020006F40000020006C40000020006C400000200065400000200048400000140000
* [hodor](https://github.com/hummingbirdtech/hodor) - esolang programming made simple by repeating hodor over and over again in various permetations.
	* > hodor.hod("Hhodor? Hodor!? Hodor!? o,", "Hooodorrhodor orHodor!? d!"); - translates as Hello World!
* [incident](https://esolangs.org/wiki/Incident) - created to challenge programmers,writing anything at all in incident is extremely challenging at least until you have mastered the esolang.
	* > A1.A2.A3,A4.A5,A6,A7;A8;B1;B2,B3.B4,B5;B6.B7.B8;C1,C2.C3;C4.C5,C6;C7,:C8.D1;D2,D3.D4,D5.D6;D7.D8,E1;E2;E3;E4,E5,E6.E7,E8.F1;F2.F3.F4,F5.F6;:F7.F8;G1,G2;G3,G4;G5.G6.G7.G8;H1.H2;H3.H4.H5.H6,H7;H8;I1,I2.I3;I4,I5.:I6,I7.I8,J1;J2,J3,J4,J5;J6;J7.J8;K1;K2;K3;K4,K5,K6;K7.K8,L1;L2,L3;L4,:L5;L6;L7,L8,M1.M2.M3.M4,M5,M6,M7,M8,N1.N2;N3,N4.N5;N6,N7.N8,Z4;a1,a1.:Z3.A1,a1;a2,a2,A1,A2.a2,a3.a3.A2,A3,a3.a5,a5,A3;A5.a5,a6,a6.A5;A6.a6.:a8.a8.A6;A8.a8;b2,b2.A8;B2.b2,b4.b4,B2,B4;b4.b5;b5;B4;B5;b5.b8.b8,B5.:B8.b8.c1;c1,B8,C1;c1,c2,c2;C1;C2,c2.c5,c5;C2,C5,c5.c8.c8,C5;C8;c8,d1;:d1.C8,D1;d1.d2;d2.D1.D2.d2.d5,d5,D2.D5.d5.d8,d8;D5;D8.d8,e5.e5.D8;E5,:e5,e8,e8,E5,E8;e8,f1.f1.E8.F1;f1;f2,f2;F1.F2.f2;f5.f5;F2;F5,f5;f7;f7.:F5,F7,f7;f8.f8;F7.F8,f8,g1;g1.F8;G1.g1,g2;g2.G1,G2,g2,g3;g3;G2,G3;g3,:g4,g4.G3;G4.g4.g5.g5,G4,G5.g5;g7;g7.G5;G7,g7,g8;g8.G7,G8;g8;h4.h4,G8;:H4,h4;h8,h8,H4.H8,h8.i5.i5;H8;I5;i5.i8;i8.I5,I8,i8.j1;j1;I8,J1;j1.j3.:j3;J1,J3;j3;j4,j4.J3,J4.j4,j8,j8.J4;J8,j8.k1.k1.J8.K1,k1,k2.k2;K1,K2;:k2.k5;k5;K2,K5.k5,k8;k8,K5.K8,k8;l1,l1;K8;L1;l1,Z1;Z2;Z2,Z3.Z2;Z1.Z1,:l2;l2;L1;L2,l2;l4.l4.L2.L4;l4.l5.l5.L4;L5;l5.l8.l8,L5.L8;l8;m2;m2.L8;:M2.m2,m3,m3,M2,M3,m3;m4.m4.M3;M4.m4,m5.m5.M4,M5,m5;m7,m7.M5.M7;m7.m8.:m8,M7,M8,m8,n1;n1.M8,N1;n1.n3,n3;N1;N3,n3.n5,n5;N3,N5;n5,n6.n6.N5.N6.:n6,n7;n7;N6.N7;n7.n8,n8;N7,N8;n8,a4,a4;Z3;A4,a4;a7.a7.A4.A7;a7,b1.b1;:A7;B1,b1;b3;b3,B1,B3.b3,b6.b6;B3;B6,b6;b7;b7,B6,B7,b7;c3,c3.B7,C3,c3.:c4.c4,C3,C4.c4;c6.c6,C4,C6.c6;c7,c7;C6.C7,c7.d3;d3.C7,D3,d3;d4;d4.D3,:D4,d4;d6,d6,D4,D6.d6;d7,d7,D6,D7.d7,e1,e1;D7,E1.e1,e2,e2;E1;E2,e2.e3;:e3,E2,E3,e3.e4;e4.E3.E4;e4,e6;e6;E4,E6,e6.e7.e7;E6.E7.e7,f3,f3.E7,F3;:f3.f4;f4,F3;F4,f4;f6;f6.F4.F6,f6,g6.g6;F6.G6.g6.h1;h1;G6;H1,h1.h2;h2.:H1;H2,h2.h3,h3,H2,H3,h3.h5.h5;H3,H5;h5;h6;h6;H5.H6.h6,h7.h7.H6,H7.h7;:i1,i1,H7.I1,i1.i2;i2;I1;I2,i2,i3.i3,I2,I3.i3;i4;i4;I3,I4,i4.i6,i6,I4.:I6,i6.i7.i7,I6;I7;i7.j2;j2;I7.J2;j2,j5;j5.J2.J5;j5.j6,j6.J5,J6,j6;j7;:j7;J6,J7.j7;k3,k3;J7.K3.k3.k4.k4,K3.K4;k4,k6;k6,K4.K6;k6,k7.k7;K6,K7.:k7,l3.l3.K7;L3;l3.l6;l6,L3;L6,l6;l7,l7,L6;L7.l7,m1.m1,L7;M1;m1,m6;m6,:M1;M6,m6;n2;n2;M6,N2,n2;n4.n4,N2;N4,n4.N8.N4,Z4,Z4 - translates to Hello World!
* [intercal](http://www.catb.org/~esr/intercal/) - Designed very early one May morning in 1972 by two hackers who are still trying to live it down. Initially implemented on an IBM 360 running batch SPITBOL. **Funniest esolang ever!**
	* > DO,1<-#14 DO,1SUB#1<-#238 DO,1SUB#2<-#108 DO,1SUB#3<-#112 PLEASE DO,1SUB#4<-#256 DO,1SUB#5<-#64 DO,1SUB#6<-#194 PLEASE DO,1SUB#7<-#48 DO,1SUB#8<-#26 DO,1SUB#9<-#244 PLEASE DO,1SUB#10<-#168 DO,1SUB#11<-#24 DO,1SUB#12<-#16 PLEASE DO,1SUB#13<-#162 DO,1SUB#14<-#52 DO READ OUT,1 DO GIVE UP - translates to Hello World!
* [jelly](https://github.com/DennisMitchell/jellylanguage) - golfing esolang based off programming language called J.
	*  > “3ḅaė;œ» - translates to Hello World!
* [kavod](https://github.com/ConorOBrien-Foxx/kavod) - turing tarpit esolang using memory stacks, which are represented by integers.
	* > 72#101#108#108#111#44#32#87#111#114#108#100#33# -translates to Hello World!
* [labyrinth](https://github.com/m-ender/labyrinth) - 2D esolang where the sorce code represents a maze navigated with instruction pointers.
	* > 72.10:1.:8:..:):1:.#2#4..:1..4.:8.0.33.@ - translates to Hello World!
* [locksmith](https://github.com/ConorOBrien-Foxx/Locksmith) - numeric esolang is all this can be described as.
	* > 070271901007101719010071087190100710871901017101719040471903027190807719010171017190101710471901007108719010071007190303719 - translates to Hello World!
* [machinecode](https://github.com/aaronryank/MachineCode) - native processor instructions esolang.
	* > 4889f8c60748c6470165c647036cc647026cc647046fc647052cc6470620c6470757c647086fc6470972c6470a6cc6470b64c6470c21c6470d00c3
sbrk()
s - translates to Hello World!
* [malbolge](https://www.lscheffer.com/malbolge.shtml) - designed to be the most difficult esolang possible with it's mod 94 locations in memory and are self modifying.
	* > ('&%:9]!~}|z2Vxwv-,POqponl\$Hjihf|B@@>,=<M:9&7Y#VV2TSn.Oe*c;(I&%$#"mCBA?zxxv*Pb8`qo42mZF.{Iy*@dD'<;_?!\}}|z2VxSSQ - translates to Hello World!
*  [monkeys](https://esolangs.org/wiki/Monkeys) - esolang completely based on the interactions of monkeys.
	* > 1 MARK
1 LEARN
1 YELL
1 BACK - translates to CAT
* [my](https://bitbucket.org/zacharyjtaylor/my-language) - designed for math-oriented golfing (AKA, IO sucks). It uses a stack-based postfix reversed order syntaxless approach.
	* > 27á'←1Aá'←8Aá'2×←1Bá'←44á'←2Ġ'←78á'←1Bá'←4Bá'←8Aá'←AȦ'←33á'←
* [no](https://github.com/cairdcoinheringaahing/Uno-No) - jsut No
	* > NOOOOOOOOOOOOOOO?Noooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo!Nooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo!Noooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo!Noooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo!Nooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo!Noooooooooooooooooooooooooooooooooooooooooooo!Noooooooooooooooooooooooooooooooo!Nooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo!Nooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo!Noooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo!Noooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo!Noooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo!Nooooooooooooooooooooooooooooooooo
NOOOOOOOO?yes - translates to Hello World!
* [numberwang](https://esolangs.org/wiki/Numberwang_\(brainfuck_derivative\)) - based on brainfuck except all commands are based on numbers.
	* > 69696969696969693696969623673363316969696968359533059595636969663633563583193 - translates to Hello World!
* [obcode](https://esolangs.org/wiki/ObCode) - object orientated, stack based, turing complete esolang.
	* > ((())(()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()())(()()())(())(()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()())(()()())(())(()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()())(()()())(())(()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()())(()()())(())(()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()())(()()())(())(()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()())(()()())(())(()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()())(()()())(())(()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()())(()()())(())(()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()())(()()())(())(()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()())(()()())(())(()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()())(()()())(())(()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()())(()()())(())(()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()()())(()()())) - translates to Hello World!
* [oOo code](https://esolangs.org/wiki/OOo_CODE) - based on brainfuck but using the way millennials troll using upper and lower case chars to draw attention tho themselves.
	* > OooOoooooOooooooooOoOoOoOoOoOooooOoOooOOooOooOooooOOooooOOooooOOooooooooooooOOooOoOOooooooOooOooOOooooOoOOoOOoOOoOOoOOoOOOoooooooOooOOoOOoooooooOOooooOoOOOoooOooOOOoooOooOOOooooooooooOOoOoOOoOOoOOOoooOooOOOoooOooOOooOOooooooooooOoOOOo - translates to Hello World!
* [ook](https://esolangs.org/wiki/ook!) - orangutan based esolang based on brainfuck, there is also a shorthand version showcased in example 2
	* > Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook.
Ook. Ook. Ook. Ook. Ook! Ook? Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook.
Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook! Ook! Ook? Ook! Ook? Ook.
Ook! Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook.
Ook. Ook. Ook! Ook? Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook?
Ook! Ook! Ook? Ook! Ook? Ook. Ook. Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook.
Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook! Ook. Ook. Ook. Ook. Ook.
Ook. Ook. Ook! Ook. Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook.
Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook? Ook? Ook. Ook. Ook.
Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook! Ook! Ook? Ook! Ook? Ook. Ook! Ook.
Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook.
Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook? Ook? Ook. Ook. Ook.
Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook.
Ook. Ook? Ook! Ook! Ook? Ook! Ook? Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook.
Ook? Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook.
Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook.
Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook!
Ook! Ook. Ook. Ook? Ook. Ook? Ook. Ook. Ook! Ook.

* Example 2 shorthand version (no Ook):
	*> \....................!?.?...?.......?...............?....................?.?.?.?.!!?!.?.?.?....!..?..!...............!.!.......!.?.?.....!..?..............................!..?!.......!.!!!!!!!!!!!!!.!!!!!!!!!!!!!!!!!.?.?...!.
* [piet](http://www.dangermouse.net/esoteric/piet.html) - abstract art looking esolang that uses 20 distinct colour blocks to to generate an image.
	* > ![piet - hi.png](https://raw.githubusercontent.com/cincodenada/bertnase_npiet/master/examples/hi.png)   

* [prelude](https://esolangs.org/wiki/Prelude) - esolang that is an ascii version of [fugue](https://esolangs.org/wiki/Fugue) using voice parts as their own stack.
	* > 92480969393782833909095806(^+^+^^+++!) - translates to Hello World!
