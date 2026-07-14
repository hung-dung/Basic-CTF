┌──(kali㉿kali)-[~/Downloads] <br>
└─$ zip2john secure.zip > hash.txt
```
ver 1.0 efh 5455 efh 7875 secure.zip/zippy/flag.txt PKZIP Encr: 2b chk, TS_chk, cmplen=38, decmplen=26, crc=849AB5A6 ts=B689 cs=b689 type=0
```
┌──(kali㉿kali)-[~/Downloads]  <br>
└─$ cat hash.txt     
```
secure.zip/zippy/flag.txt:$pkzip$1*2*2*0*26*1a*849ab5a6*0*48*0*26*b689*964fa5a31f8cefe8e6b3456b578d66a08489def78128450ccf07c28dfa6c197fd148f696e3a2*$/pkzip$:zippy/flag.txt:secure.zip::secure.zip
```
┌──(kali㉿kali)-[~/Downloads] <br>
└─$ john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt  
```
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
pass123          (secure.zip/zippy/flag.txt)     
1g 0:00:00:00 DONE (2026-07-13 23:31) 100.0g/s 819200p/s 819200c/s 819200C/s 123456..whitetiger
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```
┌──(kali㉿kali)-[~/Downloads] <br>
└─$ unzip secure.zip
```
Archive:  secure.zip
[secure.zip] zippy/flag.txt password: 
 extracting: zippy/flag.txt          
```
┌──(kali㉿kali)-[~/Downloads] <br>
└─$ cat zippy/flag.txt
```
THM{w3ll_d0n3_h4sh_r0y4l}
```
