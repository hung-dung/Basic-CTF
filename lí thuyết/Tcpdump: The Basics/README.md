Phần này giới thiệu một số đối số dòng lệnh cơ bản để sử dụng Tcpdump. Công cụ Tcpdump và `libpcap` thư viện của nó được viết bằng C và C++ và được phát hành cho các hệ thống giống Unix vào cuối những năm 1980 hoặc đầu những năm 1990. Do đó, chúng rất ổn định và cung cấp tốc độ tối ưu. `libpcap` Thư viện này là nền tảng cho nhiều công cụ mạng khác hiện nay. Hơn nữa, nó đã được chuyển đổi sang MS Windows dưới dạng `winpcap`.

Bạn có thể chạy `tcpdump` mà không cần cung cấp bất kỳ tham số nào; tuy nhiên, điều này chỉ hữu ích để kiểm tra xem bạn đã cài đặt nó hay chưa! Trong bất kỳ tình huống thực tế nào, chúng ta phải chỉ rõ cần lắng nghe cái gì, ghi ở đâu và hiển thị các gói dữ liệu như thế nào.

Chỉ định giao diện mạng

Việc đầu tiên cần quyết định là chọn giao diện mạng nào để lắng nghe bằng cách sử dụng lệnh `-i INTERFACE`. Bạn có thể chọn lắng nghe trên tất cả các giao diện khả dụng bằng cách sử dụng lệnh `-i any` hoặc bạn có thể chỉ định một giao diện mà bạn muốn lắng nghe, chẳng hạn như `-i eth0`.

Một lệnh như `ip address show` (hoặc chỉ đơn giản là `ip a s`) sẽ liệt kê các giao diện mạng khả dụng. Trong cửa sổ terminal bên dưới, chúng ta thấy một card mạng, `ens5`, ngoài địa chỉ loopback.

```
user@TryHackMe$ ip a s
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
[...]
2: ens5: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP group default qlen 1000
[...]
```

Lưu các gói dữ liệu đã thu được

Trong nhiều trường hợp, bạn nên kiểm tra lại các gói dữ liệu đã thu được sau đó. Điều này có thể được thực hiện bằng cách lưu vào một tệp bằng lệnh `-w FILE`. Phần mở rộng tệp thường được đặt là `.pcap`. Các gói dữ liệu đã lưu có thể được kiểm tra sau này bằng một chương trình khác, chẳng hạn như Wireshark. Bạn sẽ không thấy các gói dữ liệu cuộn khi chọn `-w` tùy chọn này.

Đọc các gói dữ liệu đã được thu thập từ một tệp

Bạn có thể sử dụng Tcpdump để đọc các gói tin từ một tệp bằng cách sử dụng lệnh này `-r FILE`. Điều này rất hữu ích để tìm hiểu về hành vi của giao thức. Bạn có thể thu thập lưu lượng mạng trong một khung thời gian phù hợp để kiểm tra một giao thức cụ thể, sau đó đọc tệp đã thu thập trong khi áp dụng các bộ lọc để hiển thị các gói tin mà bạn quan tâm. Hơn nữa, đó có thể là một tệp thu thập gói tin chứa thông tin về một cuộc tấn công mạng đã xảy ra, và bạn kiểm tra nó để phân tích cuộc tấn công đó.

Giới hạn số lượng gói tin được thu thập

Bạn có thể chỉ định số lượng gói tin cần thu thập bằng cách sử dụng tham số count `-c COUNT`. Nếu không chỉ định số lượng, quá trình thu thập gói tin sẽ tiếp tục cho đến khi bạn ngắt nó, ví dụ như bằng cách nhấn tổ hợp phím CTRL-C. Tùy thuộc vào mục tiêu của bạn, bạn chỉ cần một số lượng gói tin giới hạn.

Phân giải địa chỉ IP và số cổng.

Tcpdump sẽ phân giải địa chỉ IP và in ra tên miền thân thiện nếu có thể. Để tránh thực hiện các tra cứu DNS như vậy, bạn có thể sử dụng `-n` đối số. Tương tự, nếu bạn không muốn phân giải số cổng, chẳng hạn như `80` được phân giải thành http, bạn có thể sử dụng `-nn` để dừng cả việc tra cứu DNS và số cổng. Hãy xem ví dụ sau được hiển thị trong cửa sổ terminal bên dưới. Chúng ta đã bắt và hiển thị năm gói tin mà không phân giải địa chỉ IP.

```
user@TryHackMe$ sudo tcpdump -i ens5 -c 5 -n
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on ens5, link-type EN10MB (Ethernet), capture size 262144 bytes
08:55:18.989213 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 2888580014:2888580210, ack 771262362, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 196
08:55:18.989446 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 196:424, ack 1, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 228
08:55:18.989576 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 424:620, ack 1, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 196
08:55:18.989839 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 620:816, ack 1, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 196
08:55:18.989958 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 816:1012, ack 1, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 196
5 packets captured
6 packets received by filter
0 packets dropped by kernel
```

Tạo ra đầu ra chi tiết hơn

Nếu bạn muốn in thêm chi tiết về các gói tin, bạn có thể sử dụng `-v` để tạo ra đầu ra chi tiết hơn một chút. Theo trang hướng dẫn sử dụng Tcpdump (`man tcpdump`), việc thêm `-v` sẽ in ra "thời gian tồn tại, định danh, tổng chiều dài và các tùy chọn trong một gói IP" cùng với các kiểm tra khác. sẽ `-vv` tạo ra đầu ra chi tiết hơn; `-vvv` sẽ cung cấp nhiều chi tiết hơn nữa; hãy kiểm tra trang hướng dẫn để biết chi tiết.

Tóm tắt và ví dụ:

tcpdump -i INTERFACE	Thu thập các gói dữ liệu trên một giao diện mạng cụ thể.
tcpdump -w FILE	Ghi các gói dữ liệu đã bắt được vào một tệp.
tcpdump -r FILE	Đọc các gói dữ liệu đã được thu thập từ một tệp.
tcpdump -c COUNT	Thu thập một số lượng gói tin cụ thể
tcpdump -n	Không phân giải địa chỉ IP
tcpdump -nn	Không phân giải địa chỉ IP và không phân giải số giao thức.
tcpdump -v	Hiển thị chi tiết; mức độ chi tiết có thể được tăng lên bằng cách sử dụng `-vv` và `-vvv`

Hãy xem xét các ví dụ sau:

`tcpdump -i eth0 -c 50 -v` Chương trình thu thập và hiển thị 50 gói dữ liệu bằng cách lắng nghe trên `eth0` giao diện, là giao diện Ethernet có dây, và hiển thị chúng một cách chi tiết.
`tcpdump -i wlo1 -w data.pcap` Chương trình thu thập các gói dữ liệu bằng cách lắng nghe trên `wlo1` giao diện (giao diện WiFi) và ghi các gói dữ liệu đó vào `data.pcap`. Quá trình này sẽ tiếp tục cho đến khi người dùng ngắt quá trình thu thập bằng cách nhấn CTRL-C.
`tcpdump -i any -nn` Thu thập các gói dữ liệu trên tất cả các giao diện và hiển thị chúng trên màn hình mà không cần phân giải tên miền hoặc giao thức

Mặc dù bạn có thể chạy `tcpdump` mà không cần cung cấp bất kỳ biểu thức lọc nào, nhưng điều này sẽ không hữu ích. Giống như trong một buổi gặp gỡ xã giao, bạn không cố gắng lắng nghe tất cả mọi người cùng một lúc; bạn sẽ tập trung chú ý vào một người hoặc một cuộc trò chuyện cụ thể hơn. Xét đến số lượng gói tin mà card mạng của chúng ta nhận được, việc xem xét mọi thứ cùng một lúc là không thể; chúng ta cần phải cụ thể và thu thập những gì chúng ta quan tâm để kiểm tra.

Lọc theo máy chủ

Giả sử bạn chỉ quan tâm đến các gói IP được trao đổi với máy in mạng hoặc máy chủ trò chơi cụ thể. Bạn có thể dễ dàng giới hạn các gói được thu thập chỉ đến máy chủ này bằng cách sử dụng `host IP` hoặc `host HOSTNAME`. Trong cửa sổ terminal bên dưới, chúng ta thu thập tất cả các gói được trao đổi với `example.com` và lưu chúng vào `http.pcap`. Điều quan trọng cần lưu ý là việc thu thập gói yêu cầu bạn phải đăng nhập với tư cách người dùng `root` hoặc để sử dụng `sudo`.

```
user@TryHackMe$ sudo tcpdump host example.com -w http.pcap
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
16:49:02.482295 IP 192.168.139.132.49480 > 93.184.215.14.http: Flags [S], seq 3330895816, win 32120, options [mss 1460,sackOK,TS val 621343956 ecr 0,nop,wscale 7], length 0
16:49:02.635087 IP 93.184.215.14.http > 192.168.139.132.49480: Flags [S.], seq 2231582859, ack 3330895817, win 64240, options [mss 1460], length 0
16:49:02.635125 IP 192.168.139.132.49480 > 93.184.215.14.http: Flags [.], ack 1, win 32120, length 0
16:49:02.635491 IP 192.168.139.132.49480 > 93.184.215.14.http: Flags [P.], seq 1:131, ack 1, win 32120, length 130: HTTP: GET / HTTP/1.1
16:49:02.635580 IP 93.184.215.14.http > 192.168.139.132.49480: Flags [.], ack 131, win 64240, length 0
[...]
^C
13 packets captured
25 packets received by filter
0 packets dropped by kernel
```

Nếu bạn muốn giới hạn các gói tin chỉ đến từ một địa chỉ IP hoặc tên máy chủ cụ thể, bạn phải sử dụng`src host IP` hoặc `src host HOSTNAME`. Tương tự, bạn có thể giới hạn các gói tin chỉ được gửi đến một đích cụ thể bằng cách sử dụng `dst host IP` hoặc `dst host HOSTNAME`.

Lọc theo cổng

Nếu bạn muốn thu thập toàn bộ lưu lượng DNS, bạn có thể giới hạn các gói được thu thập chỉ trong phạm vi `port 53`. Hãy nhớ rằng DNS Mặc định sử dụng cổng 53 cho cả UDP và TCP. Trong ví dụ sau, chúng ta có thể thấy tất cả các cổng đó DNS Các truy vấn được đọc bởi card mạng của chúng tôi. Thiết bị đầu cuối bên dưới hiển thị hai DNS`Các truy vấn: truy vấn đầu tiên yêu cầu địa chỉ IPv4 được sử dụng bởi example.org, trong khi truy vấn thứ hai yêu cầu địa chỉ IPv6 liên kết với example.org.

```
user@TryHackMe$ sudo tcpdump -i ens5 port 53 -n
[sudo] password for strategos: 
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
17:26:33.591670 IP 192.168.139.132.47902 > 192.168.139.2.53: 47108+ A? example.org. (29)
17:26:33.591717 IP 192.168.139.132.47902 > 192.168.139.2.53: 5+ AAAA? example.org. (29)
17:26:33.593324 IP 192.168.139.2.53 > 192.168.139.132.47902: 47108 1/0/0 A 93.184.215.14 (45)
17:26:33.593325 IP 192.168.139.2.53 > 192.168.139.132.47902: 5 1/0/0 AAAA 2606:2800:21f:cb07:6820:80da:af6b:8b2c (57)
[...]
^C
12 packets captured
12 packets received by filter
0 packets dropped by kernel
```

Trong ví dụ trên, chúng ta đã thu thập tất cả các gói tin được gửi đến hoặc từ một số cổng cụ thể. Bạn có thể giới hạn các gói tin chỉ đến những gói tin từ một số cổng nguồn cụ thể hoặc đến một số cổng đích cụ thể bằng cách sử dụng các tham số tương ứng là `src port PORT_NUMBER` và `dst port PORT_NUMBER`.

Lọc theo giao thức

Loại lọc cuối cùng mà chúng ta sẽ đề cập đến là lọc theo giao thức. Bạn có thể giới hạn việc thu thập gói tin của mình theo một giao thức cụ thể; ví dụ bao gồm: ip, ip6, udp, tcp, và icmp. Trong ví dụ bên dưới, chúng ta giới hạn việc thu thập gói tin của mình chỉ ở các gói ICMP. Chúng ta có thể thấy một yêu cầu và phản hồi ICMP echo, đây có thể là dấu hiệu cho thấy ai đó đang chạy ping lệnh. Ngoài ra còn có một thông báo ICMP time exceeded; điều này có thể do chạy `traceroute` lệnh (như đã giải thích trong phần Kiến thức cơ bản về mạng ).

```
user@TryHackMe$ sudo tcpdump -i ens5 icmp -n
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
18:11:00.624681 IP 192.168.139.132 > 93.184.215.14: ICMP echo request, id 47038, seq 1, length 64
18:11:00.781482 IP 93.184.215.14 > 192.168.139.132: ICMP echo reply, id 47038, seq 1, length 64
18:11:04.168792 IP 192.168.139.2 > 192.168.139.132: ICMP time exceeded in-transit, length 68
18:11:04.168815 IP 192.168.139.2 > 192.168.139.132: ICMP time exceeded in-transit, length 68
[...]
18:11:14.857188 IP 93.184.215.14 > 192.168.139.132: ICMP 93.184.215.14 udp port 33495 unreachable, length 68
^C
52 packets captured
52 packets received by filter
0 packets dropped by kernel
```

Toán tử logic

Ba toán tử logic có thể hữu ích:

`and`: Bắt giữ các gói tin khi cả hai điều kiện đều đúng. Ví dụ, `tcpdump host 1.1.1.1 and tcp` bắt giữ `tcp` lưu lượng truy cập có `host 1.1.1.1`.
`or`: Bắt giữ các gói tin khi một trong hai điều kiện sau đúng. Ví dụ: `tcpdump udp or icmp` bắt giữ UDP hoặc lưu lượng ICMP.
`not`: Bắt giữ các gói tin khi điều kiện không đúng. Ví dụ: `tcpdump not tcp` bắt giữ tất cả các gói tin ngoại trừ TCP phân đoạn; chúng tôi dự kiến ​​sẽ tìm thấy các gói UDP, ICMP và ARP trong số các kết quả.

Tóm tắt và ví dụ

`tcpdump host IP` hoặc `tcpdump host HOSTNAME` :Lọc các gói tin theo địa chỉ IP hoặc tên máy chủ.
tcpdump src host IPhoặc	Lọc các gói tin theo máy chủ nguồn cụ thể
`tcpdump dst host IP`	Lọc các gói tin theo máy chủ đích cụ thể
`tcpdump port PORT_NUMBER`	Lọc các gói tin theo số cổng.
`tcpdump src port PORT_NUMBER`	Lọc các gói tin theo số cổng nguồn được chỉ định.
`tcpdump dst port PORT_NUMBER`	Lọc các gói tin theo số cổng đích được chỉ định.
`tcpdump PROTOCOL`	Lọc các gói dữ liệu theo giao thức; ví dụ bao gồm ip, ip6, và icmp

Hãy xem xét các ví dụ sau:

`tcpdump -i any tcp port 22` Nó lắng nghe trên tất cả các giao diện và bắt giữ tcp các gói tin đến hoặc đi từ đó port 22, ví dụ như lưu lượng SSH.
`tcpdump -i wlo1 udp port 123` Nó lắng nghe trên card mạng WiFi và lọc udp lưu lượng truy cập đến port 123 Giao thức Thời gian Mạng (NTP).
`tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap` Lệnh này sẽ lắng nghe trên eth0giao diện Ethernet có dây và lọc lưu lượng truy cập được trao đổi với example.comgiao diện sử dụng tcp và port 443. Nói cách khác, lệnh này đang lọc lưu lượng HTTPS liên quan đến example.com.

Đối với các câu hỏi trong bài tập này, chúng ta sẽ đọc các gói tin đã được ghi lại từ `traffic.pcap` tệp. Như đã đề cập trước đó, chúng ta sử dụng `-r FILE` tệp ghi lại gói tin để đọc dữ liệu. Để kiểm tra điều này, hãy thử lệnh `tcpdump -r traffic.pcap -c 5 -n`; nó sẽ hiển thị năm gói tin đầu tiên trong tệp mà không cần tra cứu địa chỉ IP.

Hãy nhớ rằng bạn có thể đếm số dòng bằng cách chuyển hướng đầu ra thông qua `wc` lệnh. Trong cửa sổ terminal bên dưới, chúng ta có thể thấy có 910 gói tin với địa chỉ IP nguồn được đặt là 192.168.124.1. Xin lưu ý rằng chúng ta thêm vào `-n` để tránh sự chậm trễ không cần thiết khi cố gắng phân giải địa chỉ IP. Trong ví dụ bên dưới, chúng ta không sử dụng `sudo` vì việc đọc từ tệp ghi lại gói tin không yêu cầu `root đặc quyền.

```
user@TryHackMe$ tcpdump -r traffic.pcap src host 192.168.124.1 -n | wc
reading from file traffic.pcap, link-type EN10MB (Ethernet)
    910   17415  140616
```

Có rất nhiều cách khác để lọc gói dữ liệu. Xét cho cùng, trong bất kỳ tình huống thực tế nào, chúng ta đều cần lọc qua hàng nghìn hoặc thậm chí hàng triệu gói dữ liệu. Việc có thể xác định chính xác các gói dữ liệu cần hiển thị là điều không thể thiếu. Ví dụ, chúng ta có thể giới hạn các gói dữ liệu được hiển thị chỉ bao gồm những gói có độ dài nhỏ hơn hoặc lớn hơn một độ dài nhất định:

`greater LENGTH` Lọc các gói tin có độ dài lớn hơn hoặc bằng độ dài được chỉ định.
`less LENGTH` Lọc các gói tin có độ dài nhỏ hơn hoặc bằng độ dài được chỉ định.

Chúng tôi khuyên bạn nên kiểm tra `pcap-filter` trang hướng dẫn bằng cách thực hiện lệnh `man pcap-filter`; tuy nhiên, trong buổi thảo luận này, chúng ta sẽ tập trung vào một tùy chọn nâng cao cho phép bạn lọc gói tin dựa trên các cờ TCP. Hiểu rõ các cờ TCP sẽ giúp bạn dễ dàng xây dựng kiến ​​thức và nắm vững các kỹ thuật lọc nâng cao hơn.

Byte tiêu đề

Mục đích của phần này là để có thể lọc các gói tin dựa trên nội dung của một byte tiêu đề. Hãy xem xét các giao thức sau: ARP, Ethernet, ICMP, IP, TCP và UDP. Đây chỉ là một vài giao thức mạng mà chúng ta đã nghiên cứu. Làm thế nào chúng ta có thể hướng dẫn Tcpdump lọc các gói tin dựa trên nội dung của các byte tiêu đề giao thức? (Chúng ta sẽ không đi sâu vào chi tiết về tiêu đề của từng giao thức vì điều này nằm ngoài phạm vi của phần này; thay vào đó, chúng ta sẽ tập trung vào các cờ TCP.)

Sử dụng pcap-filter, Tcpdump cho phép bạn tham chiếu đến nội dung của bất kỳ byte nào trong phần tiêu đề bằng cú pháp sau `proto[expr:size]`, trong đó:

`proto` : ký hiệu này đề cập đến giao thức. Ví dụ, arp, ether, icmp, ip, ip6, tcp, và udpđề cập đến ARP, Ethernet, ICMP, IPv4, IPv6, TCP vàUDPtương ứng.
`expr` : Biểu thị độ lệch byte, trong đó 0 đề cập đến byte đầu tiên.
`size` : Tham số này cho biết số byte mà chúng ta quan tâm, có thể là một, hai hoặc bốn. Tham số này là tùy chọn và mặc định là một.

Để hiểu rõ hơn điều này, hãy xem xét hai ví dụ sau từ trang hướng dẫn sử dụng pcap-filter (và đừng lo lắng nếu bạn thấy chúng khó hiểu):

`ether[0] & 1 != 0` : Hàm này lấy byte đầu tiên trong tiêu đề Ethernet và số thập phân 1 (tức là 0000 0001 trong hệ nhị phân) và áp dụng phép &toán AND (phép toán nhị phân). Nó sẽ trả về true nếu kết quả không bằng 0 (tức là 0000 0000). Mục đích của bộ lọc này là để hiển thị các gói tin được gửi đến địa chỉ multicast. Địa chỉ Ethernet multicast là một địa chỉ cụ thể xác định một nhóm thiết bị dự định nhận cùng một dữ liệu.
`ip[0] & 0xf != 5` Hàm này lấy byte đầu tiên trong tiêu đề IP và so sánh nó với số thập lục phân F (tức là 0000 1111 trong hệ nhị phân). Nó sẽ trả về true nếu kết quả không bằng số (thập phân) 5 (tức là 0000 0101 trong hệ nhị phân). Mục đích của bộ lọc này là để bắt tất cả các gói IP có tùy chọn.

Đừng lo lắng nếu bạn thấy hai ví dụ trên phức tạp. Chúng tôi đưa chúng vào để bạn biết bạn có thể đạt được điều gì; tuy nhiên, việc hiểu đầy đủ các ví dụ trên không cần thiết để hoàn thành nhiệm vụ này. Thay vào đó, chúng ta sẽ tập trung vào việc lọc các gói TCP dựa trên các cờ TCP đã thiết lập.

Bạn có thể sử dụng `tcp[tcpflags]` để chỉ TCP trường cờ. Sau đây TCP Có sẵn các lá cờ để so sánh với:
```
tcp-syn TCPSYN (Đồng bộ hóa)
tcp-ack TCPACK (Xác nhận)
tcp-fin TCPFIN (Kết thúc)
tcp-rst TCPRST (Đặt lại)
tcp-push TCP Push
```

Dựa trên những điều đã nêu ở trên, ta có thể viết:

`tcpdump "tcp[tcpflags] == tcp-syn"` để bắt giữ TCP các gói tin chỉ có cờ SYN (Đồng bộ hóa) được đặt, trong khi tất cả các cờ khác đều không được đặt.
`tcpdump "tcp[tcpflags] & tcp-syn != 0"` để bắt giữ TCP các gói tin có ít nhất cờ SYN (Đồng bộ hóa) được thiết lập.
`tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0"` để bắt giữ TCP các gói tin có ít nhất cờ SYN (Đồng bộ hóa) hoặc ACK (Xác nhận) được thiết lập.

Tcpdump là một chương trình mạnh mẽ với nhiều tùy chọn để tùy chỉnh cách in và hiển thị các gói tin. Chúng tôi đã chọn đề cập đến năm tùy chọn sau:

`-q`: Xuất nhanh; in thông tin gói tin ngắn gọn
`-e`: In tiêu đề cấp liên kết
`-A`: Hiển thị dữ liệu gói tin dưới dạng ASCII
`-xx`:Hiển thị dữ liệu gói tin ở định dạng thập lục phân, được gọi là hex.
`-X`: Hiển thị tiêu đề và dữ liệu gói tin ở dạng thập lục phân và ASCII.

Để minh họa cách các tùy chọn trên tác động đến đầu ra, trước tiên chúng ta sẽ hiển thị hai gói tin đã được thu thập mà không sử dụng bất kỳ đối số bổ sung nào.

