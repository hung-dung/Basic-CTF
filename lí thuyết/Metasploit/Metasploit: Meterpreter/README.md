Meterpreter là một Tải trọng hỗ trợ quá trình kiểm thử xâm nhập với nhiều thành phần có giá trị. Chương trình sẽ chạy trên hệ thống mục tiêu và hoạt động như một tác nhân trong kiến ​​trúc điều khiển và kiểm soát. Bạn sẽ tương tác với hệ điều hành và các tập tin của mục tiêu và sử dụng các lệnh chuyên biệt của Meterpreter.

Meterpreter có nhiều phiên bản khác nhau, mỗi phiên bản sẽ cung cấp các chức năng khác nhau tùy thuộc vào hệ thống mục tiêu.

Làm thế nào Meterpreter lam việc?

Chương trình  Meterpreter chạy trên hệ thống mục tiêu nhưng không được cài đặt trên đó. Nó chạy trong bộ nhớ và không ghi dữ liệu vào ổ đĩa trên hệ thống mục tiêu. Tính năng này nhằm mục đích tránh bị phát hiện trong quá trình quét virus. Theo mặc định, hầu hết phần mềm diệt virus sẽ quét các tệp mới trên ổ đĩa (ví dụ: khi bạn tải xuống một tệp từ internet). Meterpreter chạy trong bộ nhớ ( RAM - Bộ nhớ truy cập ngẫu nhiên (RAM) để tránh việc phải ghi tệp vào đĩa trên hệ thống đích (ví dụ: meterpreter.exe). Bằng cách này, Meterpreter sẽ được xem như một tiến trình chứ không phải là một tập tin trên hệ thống đích.

Meterpreter cũng nhằm mục đích tránh bị phát hiện bởi các hệ thống dựa trên mạng. (Hệ thống ngăn chặn xâm nhập) và IDS - Các giải pháp (Hệ thống phát hiện xâm nhập) bằng cách sử dụng giao tiếp mã hóa với máy chủ, nơi mà Meterpreter chạy (thường là máy tấn công của bạn). Nếu tổ chức mục tiêu không giải mã và kiểm tra lưu lượng truy cập được mã hóa (ví dụ: HTTPS) đến và đi từ mạng cục bộ, IPS Và IDS các giải pháp sẽ không thể phát hiện ra hoạt động của nó.

Trong khi Meterpreter Tính năng này được các phần mềm diệt virus lớn nhận diện, giúp tăng cường khả năng hoạt động bí mật ở một mức độ nhất định.

Ví dụ bên dưới cho thấy một máy tính Windows mục tiêu bị khai thác bằng lỗ hổng MS17-010. Bạn sẽ thấy  Meterpreter đang chạy với ID tiến trình ( PID ) của năm 1304; điều này Trường hợp của bạn sẽ khác. Chúng tôi đã sử dụng `getpid` Lệnh này trả về ID tiến trình mà Meterpreter đang chạy. ID tiến trình (hoặc mã định danh tiến trình) được hệ điều hành sử dụng để xác định các tiến trình đang chạy. Tất cả các tiến trình chạy trong Linux hoặc Windows đều có một số ID duy nhất; số này được sử dụng để tương tác với tiến trình khi cần thiết (ví dụ: nếu cần dừng tiến trình). 

```
meterpreter > getpid 
Current pid: 1304
```

Nếu chúng ta liệt kê các tiến trình đang chạy trên hệ thống mục tiêu bằng cách sử dụng `ps` Khi thực hiện lệnh này, ta thấy PID 1304 là `spoolsv.exe` chứ không phải `Meterpreter.exe` như người ta thường nghĩ. 

```
meterpreter > ps

Process List
============

 PID   PPID  Name                  Arch  Session  User                          Path
 ---   ----  ----                  ----  -------  ----                          ----
 0     0     [System Process]                                                   
 4     0     System                x64   0                                      
 396   644   LogonUI.exe           x64   1        NT AUTHORITY\SYSTEM           C:\Windows\system32\LogonUI.exe
 416   4     smss.exe              x64   0        NT AUTHORITY\SYSTEM           \SystemRoot\System32\smss.exe
 428   692   svchost.exe           x64   0        NT AUTHORITY\SYSTEM           
 548   540   csrss.exe             x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\csrss.exe
 596   540   wininit.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\wininit.exe
 604   588   csrss.exe             x64   1        NT AUTHORITY\SYSTEM           C:\Windows\system32\csrss.exe
 644   588   winlogon.exe          x64   1        NT AUTHORITY\SYSTEM           C:\Windows\system32\winlogon.exe
 692   596   services.exe          x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\services.exe
 700   692   sppsvc.exe            x64   0        NT AUTHORITY\NETWORK SERVICE  
 716   596   lsass.exe             x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\lsass.exe  1276  1304  cmd.exe               x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\cmd.exe
 1304  692   spoolsv.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\spoolsv.exe
 1340  692   svchost.exe           x64   0        NT AUTHORITY\LOCAL SERVICE    
 1388  548   conhost.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\conhost.exe
```

Ngay cả khi chúng ta tiến thêm một bước nữa và xem xét các DLL (Thư viện liên kết động) được sử dụng bởi Meterppreter quá trình ( 1304 trong trường hợp này), chúng ta vẫn sẽ không thấy bất cứ thứ gì nhảy bổ vào mình (ví dụ: meterpreter.dll) 

```
C:\Windows\system32>tasklist /m /fi "pid eq 1304"
tasklist /m /fi "pid eq 1304"

Image Name                     PID Modules                                     
========================= ======== ============================================
spoolsv.exe                   1304 ntdll.dll, kernel32.dll, KERNELBASE.dll,    
                                   msvcrt.dll, sechost.dll, RPCRT4.dll,        
                                   USER32.dll, GDI32.dll, LPK.dll, USP10.dll,  
                                   POWRPROF.dll, SETUPAPI.dll, CFGMGR32.dll,   
                                   ADVAPI32.dll, OLEAUT32.dll, ole32.dll,      
                                   DEVOBJ.dll, DNSAPI.dll, WS2_32.dll,         
                                   NSI.dll, IMM32.DLL, MSCTF.dll,              
                                   CRYPTBASE.dll, slc.dll, RpcRtRemote.dll,    
                                   secur32.dll, SSPICLI.DLL, credssp.dll,      
                                   IPHLPAPI.DLL, WINNSI.DLL, mswsock.dll,      
                                   wshtcpip.dll, wship6.dll, rasadhlp.dll,     
                                   fwpuclnt.dll, CLBCatQ.DLL, umb.dll,         
                                   ATL.DLL, WINTRUST.dll, CRYPT32.dll,         
                                   MSASN1.dll, localspl.dll, SPOOLSS.DLL,      
                                   srvcli.dll, winspool.drv,                   
                                   PrintIsolationProxy.dll, FXSMON.DLL,        
                                   tcpmon.dll, snmpapi.dll, wsnmp32.dll,       
                                   msxml6.dll, SHLWAPI.dll, usbmon.dll,        
                                   wls0wndh.dll, WSDMon.dll, wsdapi.dll,       
                                   webservices.dll, FirewallAPI.dll,           
                                   VERSION.dll, FunDisc.dll, fdPnp.dll,        
                                   winprint.dll, USERENV.dll, profapi.dll,     
                                   GPAPI.dll, dsrole.dll, win32spl.dll,        
                                   inetpp.dll, DEVRTL.dll, SPINF.dll,          
                                   CRYPTSP.dll, rsaenh.dll, WINSTA.dll,        
                                   cscapi.dll, netutils.dll, WININET.dll,      
                                   urlmon.dll, iertutil.dll, WINHTTP.dll,      
                                   webio.dll, SHELL32.dll, MPR.dll,            
                                   NETAPI32.dll, wkscli.dll, PSAPI.DLL,        
                                   WINMM.dll, dhcpcsvc6.DLL, dhcpcsvc.DLL,     
                                   apphelp.dll, NLAapi.dll, napinsp.dll,       
                                   pnrpnsp.dll, winrnr.dll                     

C:\Windows\system32>
```

Meterpreter có rất nhiều phiên bản khác nhau để bạn lựa chọn dựa trên hệ thống mục tiêu của mình.

Cách dễ nhất để nắm được thông tin về những thứ có sẵn trong là Meterpreter. Các phiên bản có thể được liệt kê bằng msfvenom, như hình bên dưới. 
Sử dụng `msfvenom --list payloads` lệnh và tìm kiếm các payload "meterpreter" (thêm `| grep meterpreter` (vào dòng lệnh), vì vậy đầu ra chỉ hiển thị những thông tin này. Bạn có thể thử lệnh này trên AttackBox. 

````
           
root@ip-10-10-186-44:~# msfvenom --list payloads | grep meterpreter
    android/meterpreter/reverse_http                    Run a meterpreter server in Android. Tunnel communication over HTTP
    android/meterpreter/reverse_https                   Run a meterpreter server in Android. Tunnel communication over HTTPS
    android/meterpreter/reverse_tcp                     Run a meterpreter server in Android. Connect back stager
    android/meterpreter_reverse_http                    Connect back to attacker and spawn a Meterpreter shell
    android/meterpreter_reverse_https                   Connect back to attacker and spawn a Meterpreter shell
    android/meterpreter_reverse_tcp                     Connect back to the attacker and spawn a Meterpreter shell
    apple_ios/aarch64/meterpreter_reverse_http          Run the Meterpreter / Mettle server payload (stageless)
    apple_ios/aarch64/meterpreter_reverse_https         Run the Meterpreter / Mettle server payload (stageless)
    apple_ios/aarch64/meterpreter_reverse_tcp           Run the Meterpreter / Mettle server payload (stageless)
    apple_ios/armle/meterpreter_reverse_http            Run the Meterpreter / Mettle server payload (stageless)
    apple_ios/armle/meterpreter_reverse_https           Run the Meterpreter / Mettle server payload (stageless)
    apple_ios/armle/meterpreter_reverse_tcp             Run the Meterpreter / Mettle server payload (stageless)
    java/meterpreter/bind_tcp                           Run a meterpreter server in Java. Listen for a connection
    java/meterpreter/reverse_http                       Run a meterpreter server in Java. Tunnel communication over HTTP
    java/meterpreter/reverse_https                      Run a meterpreter server in Java. Tunnel communication over HTTPS
    java/meterpreter/reverse_tcp                        Run a meterpreter server in Java. Connect back stager
    linux/aarch64/meterpreter/reverse_tcp               Inject the mettle server payload (staged). Connect back to the attacker
    linux/aarch64/meterpreter_reverse_http              Run the Meterpreter / Mettle server payload (stageless)
    linux/aarch64/meterpreter_reverse_https             Run the Meterpreter / Mettle server payload (stageless)
    linux/aarch64/meterpreter_reverse_tcp               Run the Meterpreter / Mettle server payload (stageless)
    linux/armbe/meterpreter_reverse_http                Run the Meterpreter / Mettle server payload (stageless)
    linux/armbe/meterpreter_reverse_https               Run the Meterpreter / Mettle server payload (stageless)
    linux/armbe/meterpreter_reverse_tcp                 Run the Meterpreter / Mettle server payload (stageless)
    linux/armle/meterpreter/bind_tcp                    Inject the mettle server payload (staged). Listen for a connection
    linux/armle/meterpreter/reverse_tcp                 Inject the mettle server payload (staged). Connect back to the attacker [...]
````
Danh sách sẽ hiển thị Meterpreter các phiên bản có sẵn cho các nền tảng sau:

Android
Hệ điều hành iOS của Apple
Java
Linux
OSX
PHP
Python
Windows 

Bạn quyết định chọn phiên bản Meterpreter nào. Việc sử dụng phương án nào chủ yếu sẽ dựa trên ba yếu tố:

    Hệ điều hành mục tiêu (Có phải là hệ điều hành mục tiêu không?) Linux (Hay là Windows? Đó có phải là thiết bị Mac không? Đó có phải là điện thoại Android không? v.v.)
    Các thành phần có sẵn trên hệ thống mục tiêu (Đã cài đặt Python chưa? Đây có phải là trang web PHP không? v.v.)
    Các loại kết nối mạng bạn có thể sử dụng với hệ thống mục tiêu (Hệ thống đó có cho phép kết nối TCP thô không? Bạn chỉ có thể sử dụng kết nối ngược HTTPS? Địa chỉ IPv6 có được giám sát ít hơn so với địa chỉ IPv4 không? v.v.)

Nếu bạn không sử dụng Meterpreter Là một payload độc lập được tạo ra bởi Msfvenom, lựa chọn của bạn cũng có thể bị hạn chế bởi lỗ hổng bảo mật. Bạn sẽ nhận thấy một số lỗ hổng bảo mật sẽ có một lựa chọn mặc định. Meterpreter tải trọng, như bạn có thể thấy trong ví dụ bên dưới với `ms17_010_eternalblue` khai thác.

 ```
msf6 > use exploit/windows/smb/ms17_010_eternalblue 
[*] Using configured payload windows/x64/meterpreter/reverse_tcp
msf6 exploit(windows/smb/ms17_010_eternalblue) >
```
Bạn cũng có thể liệt kê các tải trọng khả dụng khác bằng cách sử dụng `show payloads` lệnh với bất kỳ mô-đun nào. 
```
msf6 exploit(windows/smb/ms17_010_eternalblue) > show payloads 

Compatible Payloads
===================

   #   Name                                        Disclosure Date  Rank    Check  Description
   -   ----                                        ---------------  ----    -----  -----------
   0   generic/custom                                               manual  No     Custom Payload
   1   generic/shell_bind_tcp                                       manual  No     Generic Command Shell, Bind TCP Inline
   2   generic/shell_reverse_tcp                                    manual  No     Generic Command Shell, Reverse TCP Inline
   3   windows/x64/exec                                             manual  No     Windows x64 Execute Command
   4   windows/x64/loadlibrary                                      manual  No     Windows x64 LoadLibrary Path
   5   windows/x64/messagebox                                       manual  No     Windows MessageBox x64
   6   windows/x64/meterpreter/bind_ipv6_tcp                        manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 IPv6 Bind TCP Stager
   7   windows/x64/meterpreter/bind_ipv6_tcp_uuid                   manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 IPv6 Bind TCP Stager with UUID Support
   8   windows/x64/meterpreter/bind_named_pipe                      manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 Bind Named Pipe Stager [...]
```

