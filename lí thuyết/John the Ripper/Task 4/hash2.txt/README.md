HASH: 1A732667F3917C0F4AA98BB13011B9090C6F8065
```
Possible Hashs:
[+] SHA-1
[+] MySQL5 - SHA-1(SHA-1($pass))
```

┌──(kali㉿kali)-[~] <br>
└─$ echo "1A732667F3917C0F4AA98BB13011B9090C6F8065" > hash.txt
                                                                            
┌──(kali㉿kali)-[~] <br>
└─$ cat hash.txt
```
1A732667F3917C0F4AA98BB13011B9090C6F8065
```

┌──(kali㉿kali)-[~]  <br>
└─$ john --format=raw-sha1 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-SHA1 [SHA1 128/128 AVX 4x])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
kangeroo         (?)     
1g 0:00:00:00 DONE (2026-07-13 05:15) 50.00g/s 5857Kp/s 5857Kc/s 5857KC/s kanon..kalvin1
Use the "--show --format=Raw-SHA1" options to display all of the cracked passwords reliably
Session completed. 
```
