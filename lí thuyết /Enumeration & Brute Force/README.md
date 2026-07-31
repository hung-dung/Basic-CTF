Liệt kê xác thực

Hãy coi mình như một thám tử kỹ thuật số. Việc này không chỉ đơn thuần là thu thập manh mối, mà còn là hiểu được những manh mối đó tiết lộ điều gì về tính bảo mật của hệ thống. Về cơ bản, đó chính là những gì mà việc liệt kê xác thực bao gồm. Nó giống như việc ghép các mảnh ghép của một bức tranh hơn là chỉ đơn thuần đánh dấu vào các mục trong danh sách kiểm tra.

Việc liệt kê xác thực giống như việc bóc từng lớp vỏ hành tây. Bạn loại bỏ từng lớp bảo mật của hệ thống để khám phá các hoạt động thực sự bên dưới. Nó không chỉ đơn thuần là những kiểm tra thông thường; mà là để xem mọi thứ được kết nối với nhau như thế nào. 

Xác định tên người dùng hợp lệ

Việc biết được tên người dùng hợp lệ cho phép kẻ tấn công chỉ tập trung vào mật khẩu. Bạn có thể tìm ra tên người dùng bằng nhiều cách khác nhau, chẳng hạn như quan sát cách ứng dụng phản hồi trong quá trình đăng nhập hoặc đặt lại mật khẩu. Ví dụ, các thông báo lỗi chỉ rõ "tài khoản này không tồn tại" hoặc "mật khẩu không chính xác" có thể gợi ý về tên người dùng hợp lệ, giúp công việc của kẻ tấn công dễ dàng hơn. 

Chính sách mật khẩu

Các hướng dẫn khi tạo mật khẩu có thể cung cấp những hiểu biết giá trị về độ phức tạp của mật khẩu được sử dụng trong một ứng dụng. Bằng cách hiểu các chính sách này, kẻ tấn công có thể đánh giá độ phức tạp tiềm tàng của mật khẩu và điều chỉnh chiến lược của mình cho phù hợp. Ví dụ, như bên dưới
Đoạn mã PHP này sử dụng biểu thức chính quy (regex) để yêu cầu mật khẩu phải bao gồm các ký hiệu, số và chữ cái viết hoa: 

```
<?php
$password = $_POST['pass']; // Example1
$pattern = '/^(?=.*[A-Z])(?=.*\d)(?=.*[\W_]).+$/';

if (preg_match($pattern, $password)) {
    echo "Password is valid.";
} else {
    echo "Password is invalid. It must contain at least one uppercase letter, one number, and one symbol.";
}
?>
```
Trong ví dụ trên, nếu mật khẩu được cung cấp không đáp ứng chính sách được định nghĩa trong biến mẫu , ứng dụng sẽ trả về thông báo lỗi tiết lộ yêu cầu về mã biểu thức chính quy. Kẻ tấn công có thể tạo ra một từ điển đáp ứng chính sách này. 

Những địa điểm thường dùng để liệt kê

Các ứng dụng web có rất nhiều tính năng giúp người dùng dễ dàng hơn nhưng cũng có thể khiến họ gặp rủi ro:

Trang đăng ký

Các ứng dụng web thường làm cho quá trình đăng ký người dùng trở nên đơn giản và dễ hiểu bằng cách ngay lập tức cho biết liệu email hoặc tên người dùng có khả dụng hay không. Mặc dù phản hồi này được thiết kế để nâng cao trải nghiệm người dùng, nhưng nó có thể vô tình phục vụ mục đích kép. Nếu một lần đăng ký dẫn đến thông báo cho biết tên người dùng hoặc email đã được sử dụng, ứng dụng đang vô tình xác nhận sự tồn tại của nó cho bất kỳ ai đang cố gắng đăng ký. Kẻ tấn công khai thác tính năng này bằng cách thử nghiệm các tên người dùng hoặc email tiềm năng, từ đó lập danh sách người dùng đang hoạt động mà không cần truy cập trực tiếp vào cơ sở dữ liệu.

Tính năng đặt lại mật khẩu

Cơ chế đặt lại mật khẩu được thiết kế để giúp người dùng lấy lại quyền truy cập vào tài khoản của họ bằng cách nhập thông tin chi tiết để nhận hướng dẫn đặt lại. Tuy nhiên, sự khác biệt trong phản hồi của ứng dụng có thể vô tình tiết lộ thông tin nhạy cảm. Ví dụ, sự khác biệt trong phản hồi của ứng dụng về việc tên người dùng có tồn tại hay không có thể giúp kẻ tấn công xác minh danh tính người dùng. Bằng cách phân tích các phản hồi này, kẻ tấn công có thể tinh chỉnh danh sách tên người dùng hợp lệ của chúng, cải thiện đáng kể hiệu quả của các cuộc tấn công tiếp theo.

Lỗi dài dòng

Các thông báo lỗi dài dòng trong quá trình đăng nhập hoặc các quy trình tương tác khác có thể tiết lộ quá nhiều thông tin. Khi các thông báo này phân biệt giữa "không tìm thấy tên người dùng" và "mật khẩu không chính xác", mục đích là để giúp người dùng hiểu rõ vấn đề đăng nhập của họ. Tuy nhiên, chúng cũng cung cấp cho kẻ tấn công những manh mối rõ ràng về tên người dùng hợp lệ, điều này có thể bị lợi dụng để thực hiện các cuộc tấn công có mục tiêu hơn.

Thông tin về vi phạm dữ liệu

Dữ liệu từ các vụ vi phạm an ninh trước đây là một kho báu đối với tin tặc vì nó cho phép chúng kiểm tra xem tên người dùng và mật khẩu bị xâm phạm có được sử dụng lại trên các nền tảng khác nhau hay không. Nếu kẻ tấn công tìm thấy sự trùng khớp, điều đó không chỉ cho thấy tên người dùng được sử dụng lại mà còn cả khả năng tái sử dụng mật khẩu, đặc biệt nếu nền tảng đó đã từng bị xâm phạm trước đây. Kỹ thuật này cho thấy tác động của một vụ vi phạm dữ liệu duy nhất có thể lan rộng qua nhiều nền tảng, khai thác các mối liên hệ giữa các danh tính trực tuyến khác nhau. 

Hiểu về các lỗi diễn đạt dài dòng

Hãy tưởng tượng bạn là một thám tử có khả năng phát hiện ra những manh mối mà người khác có thể bỏ qua. Trong thế giới phát triển web, các lỗi chi tiết giống như những lời thì thầm vô tình của hệ thống, tiết lộ những bí mật vốn dĩ cần được giữ kín. Những thông báo lỗi chi tiết này vô cùng quý giá trong quá trình gỡ lỗi, giúp các nhà phát triển hiểu chính xác điều gì đã xảy ra. Tuy nhiên, cũng giống như một cuộc trò chuyện tình cờ có thể tiết lộ quá nhiều, những lỗi chi tiết này có thể vô tình làm lộ dữ liệu nhạy cảm cho những người biết cách lắng nghe. 

Những lỗi diễn đạt dài dòng có thể trở thành kho tàng thông tin quý giá, cung cấp những hiểu biết như:

    Đường dẫn nội bộ : Giống như một tấm bản đồ dẫn đến kho báu ẩn giấu, chúng tiết lộ đường dẫn tệp và cấu trúc thư mục của máy chủ ứng dụng, có thể chứa các tệp cấu hình hoặc khóa bí mật mà người dùng thông thường không thể nhìn thấy.
    Chi tiết cơ sở dữ liệu : Cung cấp cái nhìn thoáng qua về cơ sở dữ liệu, những lỗi này có thể tiết lộ các thông tin bí mật như tên bảng và chi tiết cột.
    Thông tin người dùng : Đôi khi, những lỗi này thậm chí có thể hé lộ tên người dùng hoặc dữ liệu cá nhân khác, cung cấp những manh mối quan trọng cho việc điều tra tiếp theo.

