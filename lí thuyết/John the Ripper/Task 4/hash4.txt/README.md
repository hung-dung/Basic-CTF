HASH: c5a60cc6bbba781c601c5402755ae1044bbf45b78d1183cbf2ca1c865b6c792cf3c6b87791344986c8a832a0f9ca8d0b4afd3d9421a149d57075e1b4e93f90bf
```
Possible Hashs:
[+] SHA-512
[+] Whirlpool
```

┌──(kali㉿kali)-[~] <br>
└─$ echo "c5a60cc6bbba781c601c5402755ae1044bbf45b78d1183cbf2ca1c865b6c792cf3c6b87791344986c8a832a0f9ca8d0b4afd3d9421a149d57075e1b4e93f90bf" > hash.txt

┌──(kali㉿kali)-[~]<br>
└─$ john --format=whirlpool --wordlist=/usr/share/wordlists/rockyou.txt hash.txt   
```
Using default input encoding: UTF-8
Loaded 1 password hash (whirlpool [WHIRLPOOL 32/64])
Warning: poor OpenMP scalability for this hash type, consider --fork=4
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
colossal         (?)     
1g 0:00:00:00 DONE (2026-07-13 05:19) 8.333g/s 5666Kp/s 5666Kc/s 5666KC/s davita1..chata74
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```                    

