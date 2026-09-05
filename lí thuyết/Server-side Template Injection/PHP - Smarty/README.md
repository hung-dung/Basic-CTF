Smarty là một công cụ tạo mẫu mạnh mẽ dành cho...PHP Điều này cho phép các nhà phát triển tách biệt phần trình bày khỏi logic nghiệp vụ, cải thiện khả năng bảo trì và mở rộng ứng dụng. Tuy nhiên, khả năng thực thi các hàm PHP trong các mẫu có thể khiến ứng dụng dễ bị tấn công chèn mẫu phía máy chủ nếu không được cấu hình an toàn.

Tính linh hoạt của Smarty cho phép thực thi động các hàm PHP trong các mẫu của nó, điều này có thể trở thành một rủi ro bảo mật đáng kể. Khả năng thực thi mã PHP thông qua các biến hoặc bổ ngữ trong mẫu cần được kiểm soát cẩn thận để ngăn chặn việc thực thi lệnh trái phép

Exploitation

Trước khi tạo payload, điều cần thiết là phải xác nhận xem ứng dụng đó có thực sự sử dụng Smarty hay không.  Ví dụ, hãy truy cập vào...http://ssti.họ:8000/smarty/(mở trong tab mới).

Chèn một thẻ Smarty đơn giản để xem nó có được xử lý hay không. Nếu ứng dụng trả về "HELLO", điều đó có nghĩa là công cụ tạo mẫu được ứng dụng sử dụng là Smarty. `{'Hello'|upper}`

<img width="2380" height="738" alt="image" src="https://github.com/user-attachments/assets/831bf41b-2edc-4c87-a342-5986cb82c4bd" />

Sau khi xác nhận trang web dễ bị tấn công SSTI thông qua Smarty, bạn có thể tạo một payload sử dụng các hàm PHP thực thi các lệnh hệ thống. Một trong những hàm phổ biến nhất thực hiện việc này là hàm `system()`. Sử dụng payload này  `{system("ls")}` là một phương pháp tấn công trực tiếp và hiệu quả nếu cài đặt bảo mật của Smarty cho phép thực thi hàm PHP.

<img width="2406" height="772" alt="image" src="https://github.com/user-attachments/assets/aa6752e2-b02d-4862-9dea-70b33b841b34" />

Khi công cụ tạo mẫu Smarty xử lý đầu vào này, nó sẽ thực thi ls lệnh. Lệnh này sẽ hiển thị danh sách thư mụccủa thư mục máy chủ nơi kịch bản được thực thi, cung cấp thông tin chi tiết về máy chủ.hệ thống tệp.

