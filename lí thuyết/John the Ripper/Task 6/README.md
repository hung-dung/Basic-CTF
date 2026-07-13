```
┌──(kali㉿kali)-[~] <br>
└─$ echo "root:x:0:0::/root:/bin/bash" > local_passwd.txt <br>
```                                                   
┌──(kali㉿kali)-[~] <br>
└─$ nano local_shadow.txt
```
root:$6$Ha.d5nGupBm29pYr$yugXSk24ZljLTAZZagtGwpSQhb3F2DOJtnHrvk7HI2ma4GsuioHp8sm3LJiRJpKfIf7lZQ29qgtH17Q/JDpYM/:18576::::::
```

┌──(kali㉿kali)-[~] <br>
└─$ unshadow local_passwd.txt local_shadow.txt > unshadowed.txt

┌──(kali㉿kali)-[~] <br>
└─$ john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt  
```
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 128/128 AVX 2x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
1234             (root)     
1g 0:00:00:00 DONE (2026-07-13 06:19) 1.612g/s 2064p/s 2064c/s 2064C/s kucing..poohbear1
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```
