HASH: D7F4D3CCEE7ACD3DD7FAD3AC2BE2AAE9C44F4E9B7FB802D73136D4C53920140A
```
Possible Hashs:
[+] SHA-256
[+] Haval-256
```

┌──(kali㉿kali)-[~] <br>
└─$ echo "D7F4D3CCEE7ACD3DD7FAD3AC2BE2AAE9C44F4E9B7FB802D73136D4C53920140A" > hash.txt
                                                                            
┌──(kali㉿kali)-[~] <br>
└─$ john --format=raw-sha256 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt      
```
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-SHA256 [SHA256 128/128 AVX 4x])
Warning: poor OpenMP scalability for this hash type, consider --fork=4
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
microphone       (?)     
1g 0:00:00:00 DONE (2026-07-13 05:16) 100.0g/s 9830Kp/s 9830Kc/s 9830KC/s ryanscott..Donovan
Use the "--show --format=Raw-SHA256" options to display all of the cracked passwords reliably
Session completed
```
 
