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
