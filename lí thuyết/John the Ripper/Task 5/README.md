                                                                         
┌──(kali㉿kali)-[~] <br>
└─$ echo "5460C85BD858A11475115D2DD3A82333" > hash.txt
                                                                            
┌──(kali㉿kali)-[~] <br>
└─$ john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
Using default input encoding: UTF-8
Loaded 1 password hash (NT [MD4 128/128 AVX 4x3])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
mushroom         (?)     
1g 0:00:00:00 DONE (2026-07-13 05:53) 100.0g/s 307200p/s 307200c/s 307200C/s lance..dangerous
Use the "--show --format=NT" options to display all of the cracked passwords reliably
Session completed. 
```
