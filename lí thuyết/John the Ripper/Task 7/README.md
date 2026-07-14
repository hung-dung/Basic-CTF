chay file `hash-id.py` de xac dinh loai bam <br>

┌──(kali㉿kali)-[~] <br>
└─$ python3 hash-id.py 

```
HASH: 7bf6d9bb82bed1302f331fc6b816aada

Possible Hashs:
[+] MD5
[+] Domain Cached Credentials - MD4(MD4(($pass)).(strtolower($username)))
````

┌──(kali㉿kali)-[~] <br>
└─$ echo "Joker:7bf6d9bb82bed1302f331fc6b816aada"> hash.txt

┌──(kali㉿kali)-[~] <br>
└─$ john --single --format=raw-md5 hash.txt

```
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-MD5 [MD5 128/128 AVX 4x3])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
Warning: Only 2 candidates buffered for the current salt, minimum 12 needed for performance.
Jok3r            (Joker)     
1g 0:00:00:00 DONE (2026-07-13 22:40) 100.0g/s 19600p/s 19600c/s 19600C/s j0ker..J0k3r
Use the "--show --format=Raw-MD5" options to display all of the cracked passwords reliably
Session completed. 
```
