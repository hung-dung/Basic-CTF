┌──(kali㉿kali)-[~] <br>
└─$ rar2john secure.rar > rar.txt
                                                                                          
┌──(kali㉿kali)-[~] <br>
└─$ cat rar.txt    
```
secure.rar:$rar5$16$b7b0ffc959b2bc55ffb712fc0293159b$15$4f7de6eb8d17078f4b3c0ce650de32ff$8$ebd10bb79dbfb9f8
```                                                                                                             
┌──(kali㉿kali)-[~] <br>
└─$ john --wordlist=/usr/share/wordlists/rockyou.txt rar.txt 
```
Using default input encoding: UTF-8
Loaded 1 password hash (RAR5 [PBKDF2-SHA256 128/128 AVX 4x])
Cost 1 (iteration count) is 32768 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
password         (secure.rar)     
1g 0:00:00:00 DONE (2026-07-13 23:44) 7.692g/s 492.3p/s 492.3c/s 492.3C/s 123456..charlie
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```
┌──(kali㉿kali)-[~] <br>
└─$ unrar x secure.rar 
```
UNRAR 7.23 freeware      Copyright (c) 1993-2026 Alexander Roshal

Enter password (will not be echoed) for secure.rar: 

Extracting from secure.rar

Extracting  flag.txt                                                  OK 
All OK
```                                                                                                                  
┌──(kali㉿kali)-[~] <br>
└─$ cat flag.txt
```
THM{r4r_4rch1ve5_th15_t1m3}
```
