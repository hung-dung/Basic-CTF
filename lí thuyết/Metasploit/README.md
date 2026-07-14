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
