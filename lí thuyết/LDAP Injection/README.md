LDAP, viết tắt của Lightweight Directory Access Protocol (Giao thức truy cập thư mục nhẹ), là một giao thức được sử dụng rộng rãi để truy cập và duy trì các dịch vụ thông tin thư mục phân tán trên mạng Giao thức Internet (IP). LDAP cho phép các tổ chức quản lý người dùng tập trung, cũng như các nhóm và thông tin thư mục khác, thường được sử dụng cho mục đích xác thực và ủy quyền trong các ứng dụng web và nội bộ.

Trong LDAP Các mục trong thư mục được cấu trúc như các đối tượng, mỗi đối tượng tuân theo một lược đồ cụ thể xác định các quy tắc và thuộc tính áp dụng cho đối tượng đó. Cách tiếp cận hướng đối tượng này đảm bảo tính nhất quán và chi phối cách các đối tượng như người dùng hoặc nhóm có thể được biểu diễn và thao tác trong thư mục.

Các dịch vụ sử dụng LDAP :

1. Microsoft Active Directory: Một dịch vụ dành cho mạng miền Windows, sử dụng LDAP như một phần của bộ giao thức cơ bản để quản lý tài nguyên miền.
2. OpenLDAP: Một triển khai mã nguồn mở của LDAP, được sử dụng rộng rãi để quản lý thông tin người dùng và hỗ trợ các cơ chế xác thực trên nhiều nền tảng khác nhau.

Định dạng LDIF

Các mục nhập LDAP có thể được biểu diễn bằng Định dạng Trao đổi Dữ liệu LDAP (LDIF), một định dạng dữ liệu văn bản thuần túy tiêu chuẩn để biểu diễn các mục nhập thư mục LDAP và các thao tác cập nhật. LDIF nhập và xuất nội dung thư mục và mô tả các sửa đổi thư mục như thêm, sửa đổi hoặc xóa các mục nhập.

Kết cấu

Thư mục LDAP tuân theo cấu trúc phân cấp như hệ thống tệp. Cấu trúc cây của nó bao gồm nhiều mục đại diện cho một đối tượng duy nhất, chẳng hạn như người dùng, nhóm hoặc tài nguyên.

<img width="1598" height="428" alt="image" src="https://github.com/user-attachments/assets/8b53417f-456e-4f12-adc6-37c9ed79b496" />

Ở cấp cao nhất của cây LDAP, chúng ta tìm thấy tên miền cấp cao nhất (TLD) , chẳng hạn như `dc=ldap,dc=thm`. Bên dưới TLD, có thể có các tên miền phụ hoặc đơn vị tổ chức (OU) , chẳng hạn như `ou=people` hoặc `ou=groups`, giúp phân loại thêm các mục trong thư mục.

1. Tên phân biệt (DN): Dùng làm mã định danh duy nhất cho mỗi mục trong thư mục, chỉ định đường dẫn từ đỉnh của cây LDAP đến mục đó, ví dụ: cn=John Doe,ou=people,dc=example,dc=com.
2. Tên phân biệt tương đối (RDN): Đại diện cho các cấp độ riêng lẻ trong hệ thống phân cấp thư mục, chẳng hạn như `cn=John Doe`, trong đó `cn` viết tắt của Common Name (Tên thông dụng).
3. Thuộc tính: Xác định các đặc tính của các mục trong thư mục, ví dụ `mail=john@example.com` như địa chỉ email.






