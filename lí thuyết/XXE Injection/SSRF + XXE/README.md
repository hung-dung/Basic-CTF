Tấn công giả mạo yêu cầu phía máy chủ (SSRFCác cuộc tấn công (attack ) xảy ra khi kẻ tấn công lạm dụng chức năng trên máy chủ, khiến máy chủ thực hiện các yêu cầu đến một vị trí không mong muốn. Trong ngữ cảnh của...XXE, kẻ tấn công có thể thao túngXMLLệnh này dùng để yêu cầu máy chủ gửi các yêu cầu đến các dịch vụ nội bộ hoặc truy cập các tệp nội bộ. Kỹ thuật này có thể được sử dụng để quét mạng nội bộ, truy cập các điểm cuối bị hạn chế hoặc tương tác với các dịch vụ chỉ có thể truy cập được từ mạng cục bộ của máy chủ.

Quét mạng nội bộ

Hãy xem xét một kịch bản trong đó một máy chủ dễ bị tổn thương đang lưu trữ một ứng dụng web khác nội bộ trên một cổng không chuẩn. Kẻ tấn công có thể khai thác lỗ hổng XXE khiến máy chủ gửi yêu cầu đến tài nguyên mạng nội bộ của chính nó.

Ví dụ, sử dụng yêu cầu đã được thu thập từ tác vụ XXE nội tuyến, hãy gửi yêu cầu đã thu thập đó đến Burp Intruder và sử dụng đoạn mã tải trọng bên dưới:

```
<!DOCTYPE foo [
  <!ELEMENT foo ANY >
  <!ENTITY xxe SYSTEM "http://localhost:§10§/" >
]>
<contact>
  <name>&xxe;</name>
  <email>test@test.com</email>
  <message>test</message>
</contact>
```

Thực thể bên ngoài được thiết lập để lấy dữ liệu từ http://localhost:§10§/. Sau đó, kẻ xâm nhập sẽ lặp lại yêu cầu và tìm kiếm một dịch vụ nội bộ đang chạy trên máy chủ.

Các bước để tấn công vét cạn nhằm tìm kiếm các cổng mở:

1. Sau khi yêu cầu được thu thập từ In-Band XXE nằm trong Intruder, hãy nhấp vào  §nút Thêm trong khi chọn cổng.

<img width="2988" height="1104" alt="image" src="https://github.com/user-attachments/assets/5df8f24d-897e-420c-89d4-1a28da56a057" />

2. Trong tab Payloads, đặt loại payload thành Numbers với các thiết lập Payload từ 1 đến 65535.

<img width="2980" height="1288" alt="image" src="https://github.com/user-attachments/assets/348adb3e-9a0d-46e8-bb9e-6df4ac8adb4e" />

3. Sau khi hoàn tất, hãy nhấp vào nút Bắt đầu tấn công và nhấp vào cột Độ dài để sắp xếp mục có kích thước lớn nhất. Sự khác biệt về kích thước phản hồi của máy chủ cần được điều tra thêm vì nó có thể chứa thông tin khác biệt so với các yêu cầu xâm nhập khác.

<img width="1968" height="1368" alt="image" src="https://github.com/user-attachments/assets/d8cb8fc5-3f2e-4e28-8f80-23e96a006906" />

<img width="2252" height="1062" alt="image" src="https://github.com/user-attachments/assets/314cf5d3-904e-4036-9708-96993762e570" />

Cách máy chủ xử lý việc này :

Đối tượng được tham chiếu bên trong thẻ, kích hoạt máy chủ thực hiện một thao tác. &xxe;  <name> HTTPYêu cầu được gửi đến URL được chỉ định khi XML được phân tích cú pháp. Phản hồi của tài nguyên được yêu cầu sau đó sẽ được bao gồm trong phản hồi của máy chủ. Nếu ứng dụng chứa các khóa bí mật,APICác khóa hoặc mật khẩu được mã hóa cứng, thông tin này sau đó có thể được sử dụng trong một hình thức tấn công khác, chẳng hạn như sử dụng lại mật khẩu.

Những hệ lụy tiềm tàng về an ninh
Thu thập thông tin : Kẻ tấn công có thể phát hiện các dịch vụ đang chạy trên các cổng mạng nội bộ và hiểu rõ hơn về kiến ​​trúc bên trong của máy chủ.
Rò rỉ dữ liệu : Nếu dịch vụ nội bộ trả về thông tin nhạy cảm, thông tin đó có thể bị lộ ra bên ngoài thông qua lỗi hoặc dữ liệu XML đầu ra.
Nâng cao đặc quyền : Việc truy cập vào các dịch vụ nội bộ có thể dẫn đến các cuộc tấn công sâu hơn, tiềm ẩn nguy cơ nâng cao khả năng của kẻ tấn công trong mạng.



