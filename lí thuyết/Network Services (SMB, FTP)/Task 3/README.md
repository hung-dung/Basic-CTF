Câu hỏi 1: Thực hiện quét nmap với cổng tùy chọn. Có bao nhiêu cổng đang mở?

Chúng ta sẽ tiến hành quét bằng lệnh này. `nmap -A 10.10.109.231 -vv` (Lưu ý: -A là một chế độ mạnh và nên được sử dụng thận trọng ngoài các máy học tập được chọn lọc) 

<img width="636" height="378" alt="image" src="https://github.com/user-attachments/assets/cd59ccc0-ff78-4c7b-9117-ad0d09111f49" />

Quá trình quét cho thấy chúng ta có 3 cổng đang mở, trả lời câu hỏi 1. 

Câu hỏi 2: SMB đang chạy trên những cổng nào?

<img width="517" height="58" alt="image" src="https://github.com/user-attachments/assets/6b198d36-e6cd-49e3-b0eb-9ed3dbff29b3" />

Kết quả quét cho thấy chúng ta có giao thức SMB đang chạy trên cổng 139 và 445.

Câu hỏi 3: Hãy bắt đầu với Enum4Linux, tiến hành liệt kê cơ bản đầy đủ. Trước tiên, tên nhóm làm việc là gì? 

Để tiến hành thống kê cơ bản đầy đủ, chúng ta sử dụng `enum4linux -A 10.10.109.231` Chúng tôi nhận được rất nhiều thông tin. Phần liên quan đến câu hỏi của chúng tôi nằm ở đây: 

<img width="452" height="86" alt="image" src="https://github.com/user-attachments/assets/5948675f-f46f-4254-9583-2e8e53bc4da2" />

Nhóm làm việc có tên là 'WORKGROUP'. 

Câu hỏi 4: Tên của máy móc đó xuất hiện là gì?

Để làm điều này, chúng ta xem phần "Thông tin hệ điều hành".

<img width="645" height="213" alt="image" src="https://github.com/user-attachments/assets/ff51e4cc-dc6d-4b66-b0db-9144fcb914b7" />

Tên máy của chúng tôi là 'POLOSMB'. 

Câu hỏi 6: Hệ điều hành đang sử dụng là phiên bản nào?

Phần này cũng cung cấp câu trả lời cho câu hỏi đó. 

<img width="291" height="80" alt="image" src="https://github.com/user-attachments/assets/e657c1e8-7e4a-4011-9d53-32e6eb190557" />

Phiên bản hệ điều hành (OS) là 6.1. 

Câu hỏi 7: Phần nào trong số đó nổi bật và đáng để chúng ta điều tra thêm?

Để làm điều này, chúng ta xem phần "Liệt kê cổ phần". 

<img width="626" height="200" alt="image" src="https://github.com/user-attachments/assets/f4fac4d6-0213-4af5-91a4-215ebbe04d85" />

Chúng tôi muốn điều tra tỷ lệ chia sẻ 'hồ sơ', vì chúng tôi có thể trích xuất thông tin người dùng từ đó.

Vậy là, Nhiệm vụ 3 đã hoàn thành! 
