# Level 12

## Reversing and decompressing hexdumps

### Solution
```
cat data.txt
mkdir /tmp/buddy
cp data.txt /tmp/buddy
cd /tmp/buddy
xxd -r data.txt > binary
file binary
mv binary binary.gz
gzip -d binary.gz
file binary
bzip2 -d binary
file binary.out
mv binary.out binary.gz
gzip -d binary.gz
file binary
tar -xf binary
ls
rm binary data
file data5.bin
tar -xf data5.bin
ls
file data6.bin
bzip2 -d data6.bin
file data6.bin.out
tar -xf data6.bin.out
ls
file data8.bin
mv data8.bin data8.gz
gzip -d data8.gz
ls
file data8
cat data8
ssh bandit13@bandit.labs.overthewire.org -p 2220
[wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw]
```

### References

[1] Bert (2017-05-01). [“Hexdump reverse command”](https://stackoverflow.com/a/43724277)

[2] THe Girl Who Encrypts (2020-06-17). [“</ OverTheWire > Bandit Level 12 → Level 13”](https://medium.com/@theGirlWhoEncrypts/overthewire-bandit-level-12-level-13-e5b687760d15)

This proved quite a tough nut to crack and I had to read up extensively about how hexdumps work and the various commands used for archiving and compressing from the linux terminal - `gzip`,`tar`, `bzip2` and  `xxd`. 

I first extracted the hexdump using `xxd -r` in a temporary folder I had created for my use (`/tmp/buddy`) and proceeded to read its compressing type using `file`, decompressing the files continuously according to the appropriate command, until the final ASCII text file was obtained. 

# Level 13

## Using ssh keys

### Solution
```
ls
ssh -i sshkey.private bandit14@localhost -p 2220
yes
ls
cd /etc/bandit_pass
ls -a
cat bandit14
```

### References
[1] ssh -help

I used the built-in command line documentation of `ssh` to find out that `-i` is used to append an identity file with the command, which I used to login as `bandit14` in the same machine.

# Level 14

## TCP I/O

### Solution
```
nc localhost 30000
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
exit
exit
ssh bandit15@bandit.labs.overthewire.org -p 2220
[jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt]
```

### References
[1] Hess, Joey; Woodcock, Robert. [“Linux Commands - NC”](https://www.commandlinux.com/man-page/man1/nc.1.html)

I realised that `netcat` or `nc` is used to read/write data across TCP/UDP connections and thus used it to create a TCP connection to submit the password obtained in the previous level as input.

# Level 15

## Connect using SSL encryption

### Solution
```
openssl s_client -ign_eof -connect localhost:30001
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
exit
ssh bandit16@bandit.labs.overthewire.org -p 2220
[JQttfApK4SeyHwDlI9SXGR50qclOAil1]
```

### References
[1] Kerrisk, Michael (2023-06-24). [“Ping Identity - Identity Security for the Digital Enterprise”](https://support.pingidentity.com/s/article/OpenSSL-s-client-Commands?source=post_page-----aea1b72721b0)

I used the `openssl` command to connect to the required service on `30001` via SSL encryption and submitted the password obtained in the previous level to receive the next level's password.

# Level 16

## Search for specific port and connect using RSA key

### Solution
```
nmap -p 31000-32000 -sV  localhost
openssl s_client -connect localhost:31790
JQttfApK4SeyHwDlI9SXGR50qclOAil1
mkdir /tmp/buddy
cd  /tmp/buddy
echo -----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

touch private.key
vim private.key
chmod 400 private.key
ssh -i private.key bandit17@localhost -p 2220
```

### References

I ran `a` nmap scan to find out that port `31790` was listening and thusx connected to it using the password obtained in the previous level, only to obtain the private RSA key, which I saved to a file in a temporary directory and used it as an `ssh` key to establish an `ssh` connection to the next level. I also had to change the permissions of the key to fix the `bad permissions` error. 

Since I was familiar with nmap scans and the vim editor, I did not have to refer any significant external documentation for this challenge.

# Level 17

## Obtain the only difference between two given files

### Solution
```
ls
diff passwords.new passwords.old
ssh bandit18@bandit.labs.overthewire.org -p 2220
[hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg]
```

### References

I intuitively figured out the analogous relation between diff and compareTo(), deciding to use it in the above mentioned way to obtain the password for the next level.

# Level 18

## Login using non-default shell

### Solution
```
ssh bandit18@bandit.labs.overthewire.org -p 2220 -t "/bin/sh"
ls
cat readme
exit
ssh bandit19@bandit.labs.overthewire.org -p 2220
[awhqfNnAbc1naukrpqDYcF95h7HoMTrC]
```

### References
[1] Mark (2017). ["serverfault - Choosing the shell that SSH uses?”](https://serverfault.com/questions/106722/choosing-the-shell-that-ssh-uses#:~:text=If%20you%20can't%20change,flag%20spawns%20a%20login%20shell.&text=For%20accessing%20a%20windows%20machine,powershell%22%20%2C%20or%20pwsh.))

I used a shell other than bash for logging into the system since only `.bashrc` was modified according to the question. After listing, the default linux shells available in my own system, I chose sh and logged into the remote machine using flag `-t` along with the `ssh` command to specify the shell I wanted to use, which did not automatically log me out and from there it was a simple `cat` away.

# Level 19

## Run executables using another user

### Solution
```
ls -l
./bandit20-do id
ls /etc/bandit_pass
./bandit20-do cat /etc/bandit_pass/bandit20
exit
ssh bandit20@bandit.labs.overthewire.org -p 2220
[VxCazJaVykI6W36BkBU0mJTCM8rR95XT]
```

### References
[1] Oli (2013-10-13). [“askUbuntu - What does "./” mean in linux shell?"](https://askubuntu.com/questions/358633/what-does-mean-in-linux-shell)

I tried using the binary file and noticed that the uid for bandit20 was assigned to me as well, which I then used to run the executable and obtain the password from `/etc/bandit_pass/bandit20`

# Level 20

## Connecting to a port listening using setuid

### Solution
```
echo "VxCazJaVykI6W36BkBU0mJTCM8rR95XT" | nc -lp 55555 &
./suconnect 55555
ssh bandit21@bandit.labs.overthewire.org -p 2220
[NvEJF7oVjkddltPSrdKEFOllh9V1IBcq]
```

### References
[1] Reynolds, Luke. (2021-11-01). [“LinuxConfig.org - Find setuid binaries to perform Linux server hardening”](https://linuxconfig.org/hardening-server-by-eliminating-setuid-and-setgid-binaries)

I setup a listener running in the background using `nc -lp &` on a random port `55555` and `echo`ed the password obtained in the previous level. Then it was as easy as executing the suconnect and passing the above mentioned port number which automatically read the previous password and returned the new password after verifying that they match.

# Level 21

## Cronjobs

### Solution
```
cd /etc/cron.d/
ls
cat cronjob_bandit22
cat /usr/bin/cronjob_bandit22.sh
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
exit
ssh bandit21@bandit.labs.overthewire.org -p 2220
[WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff]
```

### References
https://www.computerhope.com/unix/ucrontab.htm?source=post_page-----6cb782b4b17b--------------------------------

When I intuitively tried `base64 data.txt`, I realised that there must be an option to be used and thus, I learnt about `-decode` from the cited source and used it to decode `data.txt`.

# ---Pulkit Kumar (buddywhitman)
