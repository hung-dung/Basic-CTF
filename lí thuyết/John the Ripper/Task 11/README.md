┌──(kali㉿kali)-[~] <br>
└─$ ssh2john id_rsa.txt >id_rsa_hash.txt
                                                                                                                    
┌──(kali㉿kali)-[~] <br>
└─$ john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
```
Using default input encoding: UTF-8
Loaded 1 password hash (SSH, SSH private key [RSA/DSA/EC/OPENSSH 32/64])
Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=Bcrypt/AES]) is 0 for all loaded hashes
Cost 2 (iteration count) is 1 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
mango            (id_rsa.txt)     
1g 0:00:00:00 DONE (2026-07-14 00:07) 100.0g/s 432000p/s 432000c/s 432000C/s mango..doodles
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```
