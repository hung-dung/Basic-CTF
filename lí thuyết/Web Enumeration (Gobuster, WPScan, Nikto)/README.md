II. WPScan:

Giới thiệu về WPScan

Được phát hành lần đầu vào tháng 6 năm 2011, WPScan đã vượt qua thử thách của thời gian và nổi bật như một công cụ mà mọi chuyên gia kiểm thử xâm nhập nên có trong bộ công cụ của mình.

Khung WPScan có khả năng liệt kê và nghiên cứu một số loại lỗ hổng bảo mật hiện có trong các trang web WordPress - bao gồm nhưng không giới hạn ở:
```
Tiết lộ thông tin nhạy cảm (Phiên bản cài đặt Plugin & Theme cho các lỗ hổng đã được tiết lộ hoặc CVE'S)
Tìm kiếm đường dẫn (Tìm kiếm các quyền truy cập tệp bị cấu hình sai, ví dụ như wp-config.php)
Chính sách mật khẩu yếu (tấn công vét cạn mật khẩu)
Sự hiện diện của cài đặt mặc định (Đang tìm kiếm các tệp mặc định)
Kiểm tra tường lửa ứng dụng web (các plugin WAF phổ biến) 
```
Cài đặt WPScan

Rất may là WPScan đã được cài đặt sẵn trên các phiên bản mới nhất của các hệ thống kiểm thử xâm nhập như Kali Linux và Parrot. Nếu bạn đang sử dụng phiên bản Kali cũ hơn.Linux(chẳng hạn như năm 2019) ví dụ, WPScan nằm trong apt kho lưu trữ, vì vậy có thể được cài đặt bằng một lệnh đơn giản.`sudo apt update` && `sudo apt install wpscan`

<img width="1869" height="339" alt="image" src="https://github.com/user-attachments/assets/c747b5a5-c5bd-4c19-b240-4bce5d617d51" />

﻿Việc cài đặt WPScan trên các hệ điều hành khác như Ubuntu hoặc Debian đòi hỏi thêm một số bước. Mặc dù TryHackMe AttackBox đã được cài đặt sẵn WPScan, bạn vẫn có thể làm theo hướng dẫn cài đặt của nhà phát triển.(`https://github.com/wpscanteam/wpscan#install`)phù hợp với môi trường địa phương của bạn.

Giới thiệu cơ bản về cơ sở dữ liệu của WPScan

WPScan sử dụng thông tin trong cơ sở dữ liệu cục bộ làm điểm tham chiếu chính khi liệt kê các giao diện và plugin. Như chúng ta sẽ đi vào chi tiết sau, một kỹ thuật mà WPScan sử dụng khi liệt kê là tìm kiếm các giao diện và plugin phổ biến. Trước khi sử dụng WPScan, bạn nên cập nhật cơ sở dữ liệu này trước khi thực hiện bất kỳ lần quét nào.

Rất may, đây là một quy trình dễ thực hiện. Chỉ cần chạy `wpscan --update`

<img width="753" height="441" alt="image" src="https://github.com/user-attachments/assets/5330f41c-f928-4054-a4cf-8cc97a0e9f08" />

Liệt kê các chủ đề đã cài đặt

WPScan có một vài phương pháp để xác định giao diện đang hoạt động trên một cài đặt WordPress đang chạy. Về cơ bản, nó quy về một kỹ thuật mà chúng ta có thể tự thực hiện. Đơn giản là, chúng ta có thể xem các tài nguyên mà trình duyệt web tải lên và sau đó tìm vị trí của chúng trên máy chủ web. Sử dụng tab "Mạng" trong công cụ dành cho nhà phát triển của trình duyệt web, bạn có thể xem những tệp nào được tải khi bạn truy cập một trang web.

Hãy xem ảnh chụp màn hình bên dưới, chúng ta có thể thấy nhiều tài nguyên đã được tải, một số trong số đó là các tập lệnh và kiểu dáng của giao diện quyết định cách trình duyệt hiển thị trang web. URL được đánh dấu trong ảnh chụp màn hình bên dưới là: `http://redacted/wp-content/themes/twentytwentyone/assets/`

<img width="756" height="830" alt="image" src="https://github.com/user-attachments/assets/5e91450e-1cb2-46b5-9310-22fcedc6cc1d" />

Chúng ta có thể đoán khá chính xác rằng tên của giao diện hiện tại là "twentytwentyone". Sau khi kiểm tra mã nguồn của trang web, chúng ta có thể nhận thấy thêm các tham chiếu đến "twentytwentyone".

<img width="713" height="206" alt="image" src="https://github.com/user-attachments/assets/4b82990c-3bd2-43f2-b6b7-08716ea278ff" />

Tuy nhiên, chúng ta hãy sử dụng WPScan để tăng tốc quá trình này bằng cách sử dụng `--enumerate` cờ với tđối số như sau:

`wpscan --url http://cmnatics.playground/ --enumerate t `

Sau vài phút, chúng ta bắt đầu thấy một số kết quả:

<img width="1016" height="403" alt="image" src="https://github.com/user-attachments/assets/77b6b1d4-fe47-4901-a0e3-276349fea4cd" />

Ưu điểm tuyệt vời của WPScan là công cụ này cho bạn biết cách nó xác định kết quả. Trong trường hợp này, chúng ta được thông báo rằng giao diện "twentytwenty" đã được xác nhận bằng cách quét " Vị trí đã biết ". Giao diện "twentytwenty" là giao diện mặc định của WordPress cho các phiên bản WordPress năm 2020.

Liệt kê các plugin đã cài đặt

Một tính năng rất phổ biến của máy chủ web là "Liệt kê thư mục" và thường được bật mặc định. Nói một cách đơn giản, "Liệt kê thư mục" là việc liệt kê các tệp trong thư mục mà chúng ta đang điều hướng đến (giống như khi chúng ta sử dụng Windows Explorer hoặc `ls` lệnh của Linux). URL trong ngữ cảnh này rất giống với đường dẫn tệp. URL http://cmnatics.playground/a/directory. Đây thực chất là thư mục gốc đã được cấu hình của máy chủ `web/a/directory`:

<img width="692" height="57" alt="image" src="https://github.com/user-attachments/assets/ffe5a60b-d2b1-4a39-8362-bbce1597bbf2" />

"Directory Listing" xảy ra khi không có tệp nào được chỉ định để máy chủ web xử lý. Một số tệp rất phổ biến là "index.html" và "index.php". Vì các tệp này không có trong thư mục /a/, nên nội dung của chúng sẽ được hiển thị thay thế:

<img width="439" height="298" alt="image" src="https://github.com/user-attachments/assets/8e8cad01-354b-4f8c-96d5-a0395beec70c" />

WPScan có thể tận dụng tính năng này như một kỹ thuật để tìm kiếm các plugin đã được cài đặt. Vì tất cả chúng đều nằm trong thư mục /wp-content/plugins/pluginname, WPScan có thể liệt kê các plugin phổ biến/đã biết.

Trong ảnh chụp màn hình bên dưới, "easy-table-of-contents" đã được phát hiện. Tuyệt vời! Điều này có thể là một lỗ hổng bảo mật. Để xác định điều đó, chúng ta cần biết số phiên bản. May mắn thay, WordPress đã cung cấp thông tin này cho chúng ta một cách dễ dàng.

 <img width="884" height="310" alt="image" src="https://github.com/user-attachments/assets/5c68f78f-454e-4f58-9b37-f367e9556c41" />

Khi đọc tài liệu dành cho nhà phát triển của WordPress, chúng ta có thể tìm hiểu về " Tệp Readme của Plugin".(`https://developer.wordpress.org/plugins/wordpress-org/how-your-readme-txt-works/#how-the-readme-is-parsed`) "Để tìm hiểu cách WPScan xác định số phiên bản. Nói một cách đơn giản, các plugin phải có tệp "README.txt". Tệp này chứa thông tin meta như tên plugin, các phiên bản WordPress mà nó tương thích và mô tả."

<img width="964" height="381" alt="image" src="https://github.com/user-attachments/assets/34e94135-2dad-4d84-9ff5-e49ac9e46961" />

WPScan sử dụng các phương pháp bổ sung để phát hiện plugin (chẳng hạn như tìm kiếm các tham chiếu hoặc nhúng trên các trang chứa tài nguyên plugin). Chúng ta có thể sử dụng cờ với đối số như sau: --enumerate p 

`wpscan --url http://cmnatics.playground/ --enumerate p `

Chúng tôi đã chỉ ra rằng WPScan có khả năng thực hiện các cuộc tấn công vét cạn mật khẩu. Mặc dù chúng ta phải cung cấp danh sách mật khẩu như rockyou.txt , nhưng cách WPScan liệt kê người dùng lại khá đơn giản. Các trang web WordPress sử dụng tác giả cho các bài đăng. Trên thực tế, tác giả là một loại người dùng.

<img width="1138" height="705" alt="image" src="https://github.com/user-attachments/assets/0f113f17-5818-4834-9572-8c04771ccfa2" />

Và quả nhiên, tác giả này đã được WPScan của chúng tôi lựa chọn:

<img width="912" height="136" alt="image" src="https://github.com/user-attachments/assets/1620dd08-4963-4aa0-a2c3-7f2ce69c0f8e" />

Cờ "Dễ bị tổn thương"

Trong các lệnh đã thực hiện cho đến nay, chúng ta mới chỉ liệt kê WordPress để tìm ra các giao diện, plugin và người dùng hiện có. Hiện tại, chúng ta cần xem xét kết quả đầu ra và sử dụng các trang web như MITRE, NVD và CVEDetails để tra cứu tên các plugin này và số phiên bản nhằm xác định bất kỳ lỗ hổng nào.

WPScan có `v` đối số cho `--enumerate` cờ. Chúng tôi cung cấp đối số này cùng với một đối số khác (chẳng hạn như `p` dành cho plugin). Ví dụ, cú pháp của chúng tôi sẽ như sau: `wpscan --url http://cmnatics.playground/ --enumerate vp` 

Lưu ý rằng điều này yêu cầu thiết lập WPScan để sử dụng API WPVulnDB, điều này nằm ngoài phạm vi của cuộc thảo luận này. 

<img width="1025" height="81" alt="image" src="https://github.com/user-attachments/assets/afd119b7-f2ae-4ac2-b4fe-96089e67c81d" />

Thực hiện tấn công mật khẩu

Sau khi xác định được danh sách các tên người dùng khả thi trên hệ thống WordPress, chúng ta có thể sử dụng WPScan để thực hiện kỹ thuật tấn công vét cạn (brute-forcing) đối với tên người dùng đã chỉ định và danh sách mật khẩu được cung cấp. Nói một cách đơn giản, chúng ta sử dụng kết quả của việc liệt kê tên người dùng để xây dựng một lệnh như sau: `wpscan –-url http://cmnatics.playground –-passwords rockyou.txt –-usernames cmnatic`

https://assets.tryhackme.com/additional/web-enumeration-redux/password-attack.png

Điều chỉnh mức độ mạnh mẽ của WPScan (WAF)

Trừ khi có chỉ định khác, WPScan sẽ cố gắng tạo ra ít "tiếng ồn" nhất có thể. Quá nhiều yêu cầu đến máy chủ web có thể kích hoạt các hệ thống như tường lửa và cuối cùng dẫn đến việc bạn bị máy chủ chặn.

Điều này có nghĩa là một số plugin và theme có thể bị WPScan bỏ sót. May mắn thay, chúng ta có thể sử dụng các tham số như  `--plugins-detection` và cấu hình mức độ mạnh mẽ (thụ động/mạnh mẽ) để chỉ định điều này. Ví dụ: `--plugins-detection aggressive`

Tóm tắt - Bản tóm lược
```
P ->	Liệt kê các plugin	-> --enumeration p
t	-> Liệt kê các chủ đề	-> --enumeration t
u ->	Liệt kê tên người dùng	--enumerate -u
v	-> Sử dụng WPVulnDB để đối chiếu các lỗ hổng bảo mật. Ví dụ lệnh tìm kiếm các plugin dễ bị tổn thương (p)	-> --enumeration vp
aggressive ->	Đây là cấu hình độ mạnh mẽ mà WPScan sẽ sử dụng.	-> --plugins-detection aggressive
```

III. NIKTO:

Giới thiệu về Nikto
Ra mắt lần đầu vào năm 2001, Nikto đã có những bước tiến vượt bậc trong những năm qua và chứng tỏ là một công cụ quét lỗ hổng bảo mật rất phổ biến nhờ tính chất mã nguồn mở và nhiều tính năng phong phú. Nikto có khả năng thực hiện đánh giá trên tất cả các loại máy chủ web (và không phụ thuộc vào ứng dụng cụ thể như WPScan). Nikto có thể được sử dụng để phát hiện các lỗ hổng tiềm ẩn, bao gồm:
```
Tệp tin nhạy cảm
Máy chủ và chương trình lỗi thời (ví dụ: cài đặt máy chủ web dễ bị tấn công)(mở trong tab mới))
Các lỗi cấu hình phần mềm và máy chủ thường gặp (Lập chỉ mục thư mục, kịch bản CGI, bảo vệ X-SS)
```

Cài đặt Nikto
Rất may là Nikto đã được cài đặt sẵn trên các phiên bản mới nhất của các hệ thống kiểm thử xâm nhập như Kali.Linuxvà Parrot. Nếu bạn đang sử dụng phiên bản Kali cũ hơn.Linux(chẳng hạn như năm 2019) ví dụ, Nikto đang ở trong `apt` kho lưu trữ, vì vậy có thể được cài đặt bằng một lệnh đơn giản. `sudo apt update` && `sudo apt install nikto`

﻿Việc cài đặt Nikto trên các hệ điều hành khác như Ubuntu hoặc Debian đòi hỏi thêm một số bước. Mặc dù TryHackMe AttackBox đã được cài đặt sẵn Nikto, bạn vẫn có thể làm theo  hướng dẫn cài đặt của nhà phát triển.(`https://cirt.net/nikto2-docs/installation.html#id2780292`) phù hợp với môi trường địa phương của bạn.

 Quét cơ bản

Quét cơ bản nhất có thể được thực hiện bằng cách sử dụng cờ -h và cung cấp địa chỉ IP hoặc tên miền làm đối số. Loại quét này sẽ truy xuất các tiêu đề được máy chủ web hoặc ứng dụng  quảng cáo.(ví dụ: Apache2,ApacheTomcat,Jenkins hoặc JBoss) và sẽ tìm kiếm bất kỳ tập tin hoặc thư mục nhạy cảm nào (ví dụ: login.php, /admin/, v.v.)

Ví dụ minh họa như sau:`nikto -h vulnerable_ip`

<img width="1276" height="481" alt="image" src="https://github.com/user-attachments/assets/20e54c4e-53e4-4155-8b04-03f75ff8e29a" />

Hãy lưu ý rằng có một vài điều thú vị được cung cấp cho chúng ta trong ví dụ này:

Nikto đã xác định ứng dụng này là Apache Tomcat dựa trên biểu tượng favicon và sự hiện diện của `/examples/servlets/index.html`, đây là vị trí mặc định của ứng dụng Apache Tomcat.
Các phương thức HTTP " PUT " và " DELETE " có thể được thực hiện bởi các máy khách - chúng ta có thể tận dụng điều này để khai thác ứng dụng bằng cách tải lên hoặc xóa các tập tin.

Quét nhiều máy chủ và cổng

Nikto rất toàn diện ở chỗ chúng ta có thể cung cấp nhiều tham số theo cách tương tự như các công cụ như Nmap. Trên thực tế, chúng ta có thể lấy trực tiếp đầu vào từ một bản quét Nmap để quét một dải máy chủ. Bằng cách quét một mạng con, chúng ta có thể tìm kiếm các máy chủ trên toàn bộ phạm vi mạng. Chúng ta phải hướng dẫn Nmap xuất kết quả quét sang định dạng mà Nikto có thể đọc được bằng cách sử dụng `-oG` các cờ của Nmap.

Ví dụ, chúng ta có thể quét 172.16.0.0/24 (mặt nạ mạng con 255.255.255.0, cho ra 254 máy chủ khả thi) với Nmap(sử dụng cổng web mặc định là 80) và phân tích đầu ra thành Nikto như sau:`nmap -p80 172.16.0.0/24 -oG - | nikto -h -`

Không có nhiều trường hợp bạn cần dùng đến chức năng này ngoài việc đã truy cập được vào mạng. Một trường hợp phổ biến hơn nhiều là quét nhiều cổng trên một máy chủ cụ thể. Chúng ta có thể làm điều này bằng cách sử dụng `-p` cờ và cung cấp danh sách các số cổng được phân cách bằng dấu phẩy - ví dụ như sau:`nikto -h 10.10.10.1 -p 80,8000,8080`

<img width="664" height="88" alt="image" src="https://github.com/user-attachments/assets/20294ca8-e8c4-41fe-a1f9-717fc80fb3ab" />

Giới thiệu về Plugin

Các plugin giúp mở rộng hơn nữa khả năng của Nikto. Sử dụng thông tin thu thập được từ các lần quét cơ bản, chúng ta có thể chọn lựa các plugin phù hợp với mục tiêu của mình. Bạn có thể sử dụng `--list-plugins` cờ (flag) với Nikto để liệt kê các plugin hoặc xem toàn bộ danh sách ở định dạng dễ đọc hơn trực tuyến.(`https://github.com/sullo/nikto/wiki/Plugin-list`).

Một số plugin thú vị bao gồm:
```
apacheusers:	Cố gắng liệt kê người dùng xác thực HTTP của Apache.
cgi:	Hãy tìm kiếm các kịch bản CGI mà chúng ta có thể khai thác.
robots:	Phân tích tệp robots.txt, tệp này quy định những tệp/thư mục nào chúng ta có thể truy cập.
dir_traversal:	Cố gắng sử dụng tấn công duyệt thư mục (LFI) để tìm kiếm các tệp hệ thống như /etc/passwd trên Linux (http://ip_address/application.php?view=../../../../../../../etc/passwd)
```
Chúng ta có thể chỉ định plugin muốn sử dụng bằng cách dùng `-Plugin` tham số và tên của plugin đó... Ví dụ, để sử dụng plugin " apacheuser ", lệnh quét Nikto của chúng ta sẽ trông như sau: `nikto -h 10.10.10.1 -Plugin apacheuser`

<img width="907" height="57" alt="image" src="https://github.com/user-attachments/assets/05c50033-6b7b-4a30-ae84-1930aae69eec" />

Mô tả chi tiết quá trình quét của chúng tôi

Chúng ta có thể tăng độ chi tiết của quá trình quét Nikto bằng cách cung cấp các đối số sau với `-Display` cờ này. Trừ khi được chỉ định, đầu ra do Nikto đưa ra không phải là toàn bộ đầu ra, vì đôi khi nó có thể không liên quan (nhưng không phải lúc nào cũng vậy!).

```
1	-> Hiển thị bất kỳ đường dẫn chuyển hướng nào do máy chủ web cung cấp. ->	Máy chủ web có thể muốn chuyển hướng chúng ta đến một tệp hoặc thư mục cụ thể, vì vậy chúng ta cần điều chỉnh quá trình quét cho phù hợp.

2	-> Hiển thị bất kỳ cookie nào đã nhận được ->	Các ứng dụng thường sử dụng cookie như một phương tiện lưu trữ dữ liệu. Ví dụ, máy chủ web sử dụng phiên, trong đó các trang thương mại điện tử có thể lưu trữ các sản phẩm trong giỏ hàng của bạn dưới dạng cookie. Thông tin đăng nhập cũng có thể được lưu trữ trong cookie.

E -> Xuất ra bất kỳ lỗi nào -> Điều này sẽ hữu ích cho việc gỡ lỗi nếu quá trình quét không trả về kết quả như bạn mong đợi!
```

Tinh chỉnh quá trình quét để tìm kiếm lỗ hổng bảo mật

Nikto có một số loại lỗ hổng bảo mật mà chúng ta có thể chỉ định để liệt kê và kiểm tra. Danh sách sau đây không đầy đủ và chỉ bao gồm những loại mà bạn có thể thường sử dụng. Chúng ta có thể sử dụng `-Tuning` cờ và cung cấp giá trị trong quá trình quét Nikto: 
```
Tải lên tệp	-> Tìm kiếm bất kỳ thứ gì trên máy chủ web có thể cho phép chúng ta tải lên một tập tin. Điều này có thể được sử dụng để tải lên một shell đảo ngược cho một ứng dụng thực thi. -> 0

Cấu hình sai / Tệp mặc định ->	Tìm kiếm các tập tin nhạy cảm phổ biến (và không nên được truy cập, chẳng hạn như các tập tin cấu hình) trên máy chủ web. ->	2

Tiết lộ thông tin -> Thu thập thông tin về máy chủ web hoặc ứng dụng (ví dụ: số phiên bản, tiêu đề HTTP hoặc bất kỳ thông tin nào có thể hữu ích để tận dụng trong cuộc tấn công sau này). -> 3

Tiêm ->	Tìm kiếm các vị trí khả thi mà chúng ta có thể thực hiện một số loại tấn công chèn mã như XSS hoặc HTML. ->	4

Thực thi lệnh -> Hãy tìm kiếm bất cứ thứ gì cho phép chúng ta thực thi các lệnh hệ điều hành (chẳng hạn như tạo ra một shell). ->	8

Tấn công SQL Injection -> Hãy tìm kiếm các ứng dụng có tham số URL dễ bị tấn công SQL Injection.   ->	9

```

Lưu lại kết quả nghiên cứu của bạn

Thay vì phải làm việc với kết quả hiển thị trên terminal, chúng ta có thể trực tiếp xuất kết quả ra một tập tin để phân tích thêm - điều này giúp công việc của chúng ta dễ dàng hơn rất nhiều!

Nikto có khả năng chuyển đổi sang một số định dạng tệp, bao gồm:
```
Tệp văn bản
Báo cáo HTML
```
Chúng ta có thể sử dụng `-o` đối số (viết tắt của `-Output`) và cung cấp cả tên tệp và phần mở rộng tương thích. Chúng ta có thể chỉ định định dạng ( `-f` ) một cách cụ thể, nhưng Nikto đủ thông minh để sử dụng phần mở rộng mà chúng ta cung cấp trong `-o` đối số để điều chỉnh đầu ra cho phù hợp.

Ví dụ, chúng ta hãy quét một máy chủ web và xuất kết quả ra tệp "report.html": `nikto -h http://ip_address -o report.html`

<img width="769" height="187" alt="image" src="https://github.com/user-attachments/assets/91423c80-135e-4539-b6b4-ca07de0b9fd4" />

<img width="521" height="553" alt="image" src="https://github.com/user-attachments/assets/c483490b-ad6c-49de-aebe-6f7843d6a58b" />
