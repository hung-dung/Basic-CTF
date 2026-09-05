Là gì SSTI?

Lỗ hổng Server-Side Template Injection (SSTI) xảy ra khi dữ liệu đầu vào của người dùng được tích hợp không an toàn vào mẫu phía máy chủ, cho phép kẻ tấn công chèn và thực thi mã tùy ý trên máy chủ. Các công cụ tạo mẫu thường được sử dụng trong các ứng dụng web để tạo HTML động bằng cách kết hợp các mẫu cố định với dữ liệu động. Khi các công cụ này xử lý dữ liệu đầu vào của người dùng mà không được làm sạch đúng cách, chúng sẽ dễ bị tấn công SSTI.

Khái niệm cốt lõi của SSTI

1. Tạo nội dung động: Các công cụ tạo mẫu thay thế các chỗ giữ chỗ bằng dữ liệu thực tế, cho phép các ứng dụng tạo ra các trang HTML động. Quá trình này có thể bị khai thác nếu dữ liệu đầu vào của người dùng không được xử lý đúng cách.
2. Dữ liệu đầu vào của người dùng được coi là mã mẫu: Khi dữ liệu đầu vào của người dùng được xử lý như một phần của mã mẫu, chúng có thể đưa logic độc hại vào kết quả đầu ra, dẫn đến lỗi SSTI (Single-Stack Interaction Interaction).
Cốt lõi của lỗ hổng SSTI nằm ở việc xử lý không đúng cách dữ liệu đầu vào của người dùng trong các mẫu phía máy chủ. Các công cụ tạo mẫu diễn giải và thực thi các biểu thức được nhúng để tạo nội dung động. Nếu kẻ tấn công có thể chèn các mã độc hại vào các biểu thức này, chúng có thể thao túng logic phía máy chủ và có khả năng thực thi mã tùy ý.

Luồng tấn công SSTI

<img width="1140" height="460" alt="image" src="https://github.com/user-attachments/assets/22897f7e-26d7-43c6-a477-202953ed44c6" />

Khi dữ liệu người dùng nhập trực tiếp vào các mẫu mà không được xác thực hoặc mã hóa đúng cách, kẻ tấn công có thể tạo ra các payload làm thay đổi hành vi của mẫu. Điều này có thể dẫn đến nhiều hành động không mong muốn ở phía máy chủ, bao gồm:

1. Đọc hoặc chỉnh sửa các tập tin phía máy chủ.
2. Thực thi các lệnh hệ thống.
3. Truy cập thông tin nhạy cảm (ví dụ: biến môi trường, thông tin đăng nhập cơ sở dữ liệu).

Công cụ tạo mẫu

Công cụ tạo mẫu (template engine) giống như một cỗ máy giúp xây dựng các trang web một cách động. Dưới đây là cách hoạt động đơn giản của nó:

Hãy tưởng tượng bạn đang làm thiệp chúc mừng sinh nhật cho một người bạn. Bạn muốn ghi tên, tuổi và một lời nhắn cá nhân. Thay vì viết một tấm thiệp mới từ đầu, bạn sử dụng một mẫu có sẵn chỗ dành cho tên, tuổi và lời nhắn.

Công cụ tạo mẫu hoạt động tương tự:

1. Mẫu : Công cụ này sử dụng một mẫu được thiết kế sẵn với các phần giữ chỗ như {{ name }} cho nội dung động.
2. Dữ liệu đầu vào từ người dùng : Hệ thống nhận dữ liệu đầu vào từ người dùng (như tên, tuổi hoặc tin nhắn) và lưu trữ vào một biến.
3. Kết hợp : Công cụ sẽ kết hợp mẫu với dữ liệu do người dùng nhập, thay thế các chỗ giữ chỗ bằng dữ liệu thực tế.
4. Kết quả : Công cụ sẽ tạo ra một trang web động hoàn chỉnh với nội dung do người dùng nhập vào được chèn vào mẫu.

Các công cụ tạo mẫu cung cấp nhiều chức năng giúp tăng tốc quá trình phát triển nhưng cũng có thể tiềm ẩn rủi ro. Hầu hết các công cụ tạo mẫu cho phép sử dụng biểu thức để thực hiện các phép tính đơn giản hoặc các thao tác logic trong mẫu.

<img width="1140" height="500" alt="image" src="https://github.com/user-attachments/assets/efcab369-6d82-413c-81d7-98e4a1333f5d" />

Trong bối cảnh của SSTI Khả năng thực thi mã của công cụ tạo mẫu chính là điểm khiến nó dễ bị tấn công. Nếu dữ liệu đầu vào của người dùng không được xử lý đúng cách, kẻ tấn công có thể chèn mã độc hại, và công cụ tạo mẫu sẽ thực thi mã đó, dẫn đến những hậu quả không mong muốn.

Các công cụ tạo mẫu phổ biến

Các công cụ tạo mẫu là một phần không thể thiếu trong phát triển web hiện đại, cho phép các nhà phát triển tạo ra nội dung HTML động bằng cách kết hợp các mẫu với dữ liệu. Dưới đây là một số công cụ tạo mẫu được sử dụng phổ biến nhất:

1. Jinja2 : Rất phổ biến trong các ứng dụng Python, nổi tiếng với khả năng diễn đạt mạnh mẽ và tính biểu đạt cao.
2. Twig : Công cụ tạo mẫu mặc định cho Symfony.PHPTwig cung cấp một môi trường mạnh mẽ với các thiết lập mặc định an toàn.
3. Pug/Jade : Được biết đến với cú pháp mẫu HTML tối giản và gọn gàng, Pug/Jade rất phổ biến trong cộng đồng các nhà phát triển Node.js.

Cách các công cụ tạo mẫu phân tích và xử lý dữ liệu đầu vào

Các công cụ tạo mẫu hoạt động bằng cách phân tích các tệp mẫu, chứa nội dung tĩnh kết hợp với cú pháp đặc biệt dành cho nội dung động. Khi hiển thị mẫu, công cụ sẽ thay thế các phần động bằng dữ liệu thực tế được cung cấp trong quá trình thực thi. Ví dụ:

```
from jinja2 import Template

hello_template = Template("Hello, {{ name }}!")
output = hello_template.render(name="World")
print(output)
```

Trong ví dụ này, {{ name }}là một chỗ giữ chỗ sẽ được thay thế bằng giá trị "World"trong quá trình hiển thị.

Xác định công cụ tạo mẫu
Các công cụ tạo mẫu khác nhau có cú pháp và tính năng riêng biệt, khiến chúng dễ bị tấn công SSTI theo nhiều cách khác nhau. Dưới đây là một số ví dụ về cú pháp mẫu dễ bị tổn thương:

Jinja2/Twig

Jinja2 và Twig có cú pháp và hành vi tương tự nhau, khiến việc phân biệt chúng chỉ dựa vào phản hồi của payload trở nên khá khó khăn. Tuy nhiên, bạn có thể phát hiện sự hiện diện của chúng bằng cách kiểm tra khả năng xử lý biểu thức. Ví dụ, sử dụng máy ảo dễ bị tổn thương, nếu bạn sử dụng payload {{7*'7'}} trong Twig, đầu ra sẽ là 49.

<img width="2254" height="710" alt="image" src="https://github.com/user-attachments/assets/c9b7d716-33f3-4c27-9e78-726dab2acb45" />

Tuy nhiên, nếu bạn sử dụng cùng một payload trong một ứng dụng sử dụng Jinja2, thì kết quả đầu ra sẽ là 7777777

<img width="2336" height="734" alt="image" src="https://github.com/user-attachments/assets/4e118b25-4742-42ab-9d26-39fb4962a26c" />

Jade/Pug

Pug, trước đây được biết đến với tên Jade, sử dụng cú pháp khác để xử lý biểu thức, điều này có thể bị lợi dụng để xác định cách sử dụng của nó. Pug/Jade đánh giá các biểu thức JavaScript bên trong #{}. Ví dụ, sử dụng payload #{7*7} sẽ trả về 49.

<img width="2330" height="726" alt="image" src="https://github.com/user-attachments/assets/c941acb3-ed52-4b1b-b055-01869ba6cd59" />

Không giống như Jinja2 hay Twig, Pug/Jade cho phép thực thi trực tiếp JavaScript bên trong các mẫu của nó mà không cần các dấu phân cách bổ sung như {{ }}. Ví dụ:

<img width="2348" height="744" alt="image" src="https://github.com/user-attachments/assets/46327352-0093-4199-8385-27d89959f568" />








