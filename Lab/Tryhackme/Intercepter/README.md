```
┌──(kali㉿kali)-[~]
└─$ nmap -sV -sC 10.112.158.179  
Starting Nmap 7.95 ( https://nmap.org ) at 2026-07-31 09:07 EDT
Nmap scan report for 10.112.158.179
Host is up (0.25s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 66:33:f1:61:9c:c7:fc:86:07:e3:a7:52:e2:f1:66:4f (RSA)
|   256 59:f6:61:68:66:07:8f:9c:7b:46:bb:ef:a0:0d:43:a1 (ECDSA)
|_  256 be:10:a8:85:db:96:df:04:b8:5f:f8:44:21:96:2e:2c (ED25519)
53/tcp open  domain  ISC BIND 9.16.1 (Ubuntu Linux)
| dns-nsid: 
|_  bind.version: 9.16.1-Ubuntu
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-title: MediaHub
|_http-server-header: Apache/2.4.41 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 20.62 seconds

```

