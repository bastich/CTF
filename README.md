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
* Fire up your [playlist-defcon-26](https://defconcommunications.bandcamp.com/album/def-con-26-the-official-soundtrack) and settle in for the long haul
<hr>

# Crypto

> Cryptographia epistolica, sive de clandestina scriptione - Erycius Puteanus (1574 - 1646)

###### `Low Hanging Fruit`

* 
