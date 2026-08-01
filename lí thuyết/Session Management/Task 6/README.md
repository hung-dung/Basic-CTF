Liệt kê

Để khai thác hiệu quả một vòng đời quản lý phiên dễ bị tổn thương, trước tiên chúng ta cần lập sơ đồ vòng đời đó và ghi chép chi tiết. Khi đã hiểu rõ vòng đời dự định, chúng ta có thể bắt đầu tìm kiếm các điểm yếu. Chúng ta sẽ sử dụng các công cụ tích hợp sẵn của trình duyệt cho ví dụ này. Tuy nhiên, bạn cũng có thể làm theo với các công cụ kiểm thử ứng dụng web nâng cao hơn, chẳng hạn như Burp. Hãy truy cập vào ứng dụng của chúng ta tại địa chỉ sau: http://10.113.138.1. Đầu tiên, chúng ta sẽ xem trang sau:

<img width="886" height="847" alt="image" src="https://github.com/user-attachments/assets/5f264cb0-e0a3-4e66-9ba7-af4f54d3aabf" />

Điều đầu tiên chúng ta nhận thấy là khi truy cập trang lần đầu, chúng ta không thấy bất kỳ cookie hay mã thông báo nào. Điều này cho thấy rằng các phiên truy cập không được xác thực rất có thể không được theo dõi. Nếu nhấp vào nút Đăng ký, chúng ta sẽ thấy có hai hình thức đăng ký chính:

Sinh viên - Bất kỳ ai cũng có thể sử dụng tính năng này để tạo hồ sơ.
Giảng viên - Cần mã xác minh để hoàn tất quá trình đăng ký.

Điều này cho thấy rằng ngay cả khi không sử dụng bất kỳ kỹ thuật tấn công vét cạn nào, chúng ta vẫn có thể khởi động vòng đời quản lý phiên bằng cách tạo tài khoản học sinh. Hãy tạo một tài khoản học sinh và xem điều gì sẽ xảy ra:

<img width="393" height="612" alt="image" src="https://github.com/user-attachments/assets/cc70b990-f2c6-4cfa-9e29-daebd1321b1a" />

Sau khi tạo tài khoản người dùng, chúng ta nhận được thông báo rằng tài khoản đã được tạo và được chuyển hướng trở lại trang đăng nhập. Hãy thử đăng nhập bằng tài khoản của mình và theo dõi lưu lượng mạng:

<img width="760" height="667" alt="image" src="https://github.com/user-attachments/assets/8539fa28-995b-4487-8107-3e8cda3fdd83" />

Điều này cho chúng ta biết khá nhiều thông tin:

Cookie được sử dụng để quản lý phiên.
Cờ HTTPOnly được thiết lập, điều này có nghĩa là chúng ta sẽ không thể sử dụng JavaScript để đọc giá trị cookie.
Với quá trình xác thực này, chúng ta cũng nhận thấy rằng giờ đây chúng ta có quyền truy cập vào nhiều chức năng hơn:

<img width="1088" height="630" alt="image" src="https://github.com/user-attachments/assets/47fb0352-2df4-4eb7-8050-eaf77fbc31d7" />

Bằng cách sử dụng menu điều hướng và xem xét lưu lượng mạng, chúng ta có thể thấy rằng việc theo dõi phiên được thực thi thông qua cookie được truyền kèm theo mỗi yêu cầu:

<img width="764" height="650" alt="image" src="https://github.com/user-attachments/assets/87bed13d-cfba-4458-b20e-157f91c5a9ec" />

một điều thú vị cần lưu ý là ngay cả khi thời gian hết hạn của cookie chưa đến, cùng một tiêu đề cookie được thiết lập vẫn được sử dụng để làm mới cookie về cùng một giá trị và kéo dài thời gian tồn tại hơn nữa. Điều này có thể cho thấy đây là một cookie tồn tại lâu dài. Hãy xem điều gì xảy ra khi chúng ta xóa cookie này. Trong phần lưu trữ, hãy xóa cookie và thực hiện lại yêu cầu mô-đun:

<img width="764" height="611" alt="image" src="https://github.com/user-attachments/assets/3ee61846-cc2b-43e8-85e8-d431e990ec3e" />

Yêu cầu dường như vẫn thành công? Tuy nhiên, nếu bạn xem xét kỹ hơn, bạn sẽ thấy rằng hiện tại chúng ta chỉ có thể thấy các mô-đun chứ không thấy số lượng sinh viên đã đăng ký hoặc các bài kiểm tra tiềm năng:

<img width="817" height="444" alt="image" src="https://github.com/user-attachments/assets/441bf8e3-74a4-4e21-a11c-4347229cab61" />

Điều này cho chúng ta biết rằng chúng ta có thể cần phải điều tra thêm để xác định chính xác những gì chúng ta được phép truy cập từ góc độ hoàn toàn không cần xác thực. Điều này sẽ cần điều tra thêm để lập bản đồ đầy đủ về vòng đời quản lý phiên. Tuy nhiên, chúng ta sẽ giữ mọi thứ đơn giản hơn một chút. Hãy xem xét chức năng đăng xuất. Sau khi nhấn nút đăng xuất, chúng ta có thể thấy rằng phiên của chúng ta đã bị xóa ở phía máy khách:

<img width="885" height="360" alt="image" src="https://github.com/user-attachments/assets/8bc7a443-9791-43fd-940f-fdc08a9cf40c" />

Tuy nhiên, có lẽ chúng ta nên kiểm tra xem phiên làm việc có bị chấm dứt ở phía máy chủ hay không. Bạn có thể xác thực lại với ứng dụng và thay thế cookie mới bằng giá trị cookie cũ. Nhưng dường như việc chấm dứt phiên làm việc vẫn hoạt động ở một mức độ nào đó vì bạn nhận được lỗi 500 Internal Server Error khi làm mới trang. Điều này cho chúng ta biết rằng có điều gì đó không ổn ở đây, vì một phiên làm việc không hợp lệ không nên dẫn đến lỗi máy chủ nội bộ. Hãy cùng điều tra.

Hãy cùng xem lại một số nhận định trước đây của chúng ta. Nếu truy cập vào Bộ nhớ cục bộ, chúng ta sẽ thấy khá nhiều dữ liệu đang được lưu trữ

<img width="936" height="226" alt="image" src="https://github.com/user-attachments/assets/a0bc7fa4-ab2c-4a51-a35d-ebf67567f7ec" />

Hãy thử thay đổi vai trò người dùng từ sinh viên thành `admin` và làm mới trang:

<img width="956" height="843" alt="Screenshot 2026-08-01 154332" src="https://github.com/user-attachments/assets/7aca07ea-85e3-40ab-924e-1bd4fde1eedf" />

<img width="958" height="697" alt="Screenshot 2026-08-01 154628" src="https://github.com/user-attachments/assets/3b8105a4-b392-4cd9-ae4f-33fe6cbcb67c" />

Click vao Student 

<img width="963" height="725" alt="Screenshot 2026-08-01 154650" src="https://github.com/user-attachments/assets/d1a4f8fe-7d0a-40b3-973c-92b24e045025" />

