HASH: 2e728dd31fb5949bc39cac5a9f066498

```
Possible Hashs:
[+] MD5
[+] Domain Cached Credentials - MD4(MD4(($pass)).(strtolower($username)))
```

┌──(kali㉿kali)-[~] <br>
└─$ echo "2e728dd31fb5949bc39cac5a9f066498" > hash.txt
                                                                            
┌──(kali㉿kali)-[~] <br>
└─$ cat hash.txt 
2e728dd31fb5949bc39cac5a9f066498

┌──(kali㉿kali)-[~] <br>
└─$ john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

```
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-MD5 [MD5 128/128 AVX 4x3])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
biscuit          (?)     
1g 0:00:00:00 DONE (2026-07-13 05:13) 100.0g/s 268800p/s 268800c/s 268800C/s shamrock..nugget
Use the "--show --format=Raw-MD5" options to display all of the cracked passwords reliably
Session completed.
```
