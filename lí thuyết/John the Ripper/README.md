Có nhiều cách để sử dụng John the Ripper

Để giải mã các hàm băm đơn giản. Chúng ta sẽ cùng xem xét một vài hàm băm trước khi tự mình thực hiện việc giải mã một số hàm băm khác.
Cú pháp cơ bản của John

Cú pháp cơ bản của John the Ripper

Các lệnh như sau. Chúng ta sẽ tìm hiểu các tùy chọn và bổ ngữ cụ thể được sử dụng khi chúng ta dùng chúng.

john [options] [file path]

john: Kích hoạt chương trình John the Ripper
[options]: Chỉ định các tùy chọn bạn muốn sử dụng
[file path]: Đây là tệp chứa mã băm mà bạn đang cố gắng giải mã; nếu tệp nằm trong cùng thư mục, bạn không cần phải chỉ định đường dẫn, chỉ cần chỉ định tên tệp.

Ví dụ sử dụng:

john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt

Để sử dụng mã định danh băm, bạn có thể sử dụng wget hoặc curlđể tải xuống tệp Python hash-id.py GitLab của nó Tải xuống từ trang (mở trong tab mới) . Sau đó, khởi chạy nó bằng lệnh python3 hash-id.pyvà nhập mã băm mà bạn đang cố gắng xác định. Nó sẽ cung cấp cho bạn danh sách các định dạng có khả năng nhất. Hai bước này được hiển thị trong cửa sổ dòng lệnh bên dưới.

wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py

$ python3 hash-id.py

Bẻ khóa theo định dạng cụ thể

Khi bạn đã xác định được mã băm cần xử lý, bạn có thể yêu cầu John sử dụng mã băm đó trong quá trình giải mã bằng cú pháp sau:

john --format=[format] --wordlist=[path to wordlist] [path to file]

--format=Đây là tín hiệu để báo cho John biết rằng bạn đang cung cấp cho nó một mã băm có định dạng cụ thể và yêu cầu nó sử dụng định dạng sau để giải mã.
[format]: Định dạng của mã băm

Ví dụ sử dụng:

john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt

Lưu ý về định dạng:

Khi bạn bảo John sử dụng các định dạng, nếu bạn đang làm việc với một kiểu băm chuẩn, ví dụ:

Như trong ví dụ trên, bạn phải thêm tiền tố là raw-Bạn có thể nói với John rằng bạn chỉ đang làm việc với một kiểu băm tiêu chuẩn, mặc dù điều này không phải lúc nào cũng đúng. Để kiểm tra xem bạn có cần thêm tiền tố hay không, bạn có thể liệt kê tất cả các định dạng của John bằng cách sử dụng `john --list=formats`và kiểm tra thủ công hoặc tìm kiếm kiểu băm của bạn bằng một công cụ như sau: `john --list=formats | grep -iF "md5" `.
