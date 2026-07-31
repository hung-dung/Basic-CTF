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

Các lỗ hổng trong quy trình đặt lại mật khẩu

Cơ chế đặt lại mật khẩu là một phần quan trọng mang lại sự tiện lợi cho người dùng trong các ứng dụng web hiện đại. Tuy nhiên, việc triển khai chúng đòi hỏi phải xem xét cẩn thận về vấn đề bảo mật vì các quy trình đặt lại mật khẩu kém bảo mật có thể dễ dàng bị khai thác.

Đặt lại dựa trên email

Khi người dùng đặt lại mật khẩu, ứng dụng sẽ gửi một email chứa liên kết đặt lại mật khẩu hoặc mã xác thực đến địa chỉ email đã đăng ký của người dùng. Sau đó, người dùng nhấp vào liên kết này, dẫn họ đến một trang nơi họ có thể nhập mật khẩu mới và xác nhận, hoặc hệ thống sẽ tự động tạo mật khẩu mới cho người dùng. Phương pháp này phụ thuộc rất nhiều vào tính bảo mật của tài khoản email người dùng và tính bí mật của liên kết hoặc mã xác thực được gửi đi.

Đặt lại dựa trên câu hỏi bảo mật

Quá trình này bao gồm việc người dùng trả lời một loạt câu hỏi bảo mật được cấu hình sẵn mà họ đã thiết lập khi tạo tài khoản. Nếu câu trả lời chính xác, hệ thống cho phép người dùng tiếp tục đặt lại mật khẩu. Mặc dù phương pháp này bổ sung thêm một lớp bảo mật bằng cách yêu cầu thông tin mà chỉ người dùng mới biết, nhưng nó có thể bị xâm phạm nếu kẻ tấn công có được quyền truy cập vào thông tin nhận dạng cá nhân.PII), điều này đôi khi có thể dễ dàng tìm thấy hoặc đoán được.

Đặt lại bằng tin nhắn SMS

Phương pháp này hoạt động tương tự như việc đặt lại mật khẩu qua email nhưng sử dụng tin nhắn SMS để gửi mã hoặc liên kết đặt lại mật khẩu trực tiếp đến điện thoại di động của người dùng. Sau khi nhận được mã, người dùng có thể nhập mã đó trên trang web được cung cấp để truy cập chức năng đặt lại mật khẩu. Phương pháp này giả định rằng việc truy cập vào điện thoại của người dùng là an toàn, nhưng nó có thể dễ bị tấn công bằng cách đánh cắp SIM hoặc chặn bắt thông tin.

Mỗi phương pháp này đều có những điểm yếu riêng:

Mã thông báo dễ đoán : Nếu mã thông báo đặt lại được sử dụng trong các liên kết hoặc tin nhắn SMS dễ đoán hoặc tuân theo một trình tự nhất định, kẻ tấn công có thể đoán hoặc tấn công vét cạn để tạo ra các URL đặt lại hợp lệ.

Vấn đề hết hạn token : Các token có hiệu lực quá lâu hoặc không hết hạn ngay sau khi sử dụng sẽ tạo ra cơ hội cho kẻ tấn công. Điều quan trọng là các token phải hết hạn nhanh chóng để hạn chế cơ hội này.

Xác thực không đầy đủ : Các cơ chế xác minh danh tính người dùng, như câu hỏi bảo mật hoặc xác thực qua email, có thể yếu và dễ bị khai thác nếu các câu hỏi quá phổ biến hoặc tài khoản email bị xâm phạm.

Tiết lộ thông tin : Bất kỳ thông báo lỗi nào cho biết địa chỉ email hoặc tên người dùng đã được đăng ký hay chưa đều có thể vô tình giúp kẻ tấn công trong quá trình thu thập thông tin, xác nhận sự tồn tại của các tài khoản.

Truyền tải không an toàn : Việc truyền các liên kết đặt lại hoặc mã thông báo qua các kết nối không phải HTTPS có thể khiến các yếu tố quan trọng này dễ bị kẻ nghe lén mạng chặn bắt.

Khai thác các mã thông báo có thể dự đoán được

Các token đơn giản, dễ đoán hoặc có thời gian hết hạn dài có thể đặc biệt dễ bị tấn công chặn hoặc tấn công vét cạn. Ví dụ, đoạn mã dưới đây được sử dụng bởi ứng dụng dễ bị tổn thương được lưu trữ trong phòng thí nghiệm Token dễ đoán:

```
$token = mt_rand(100, 200);
$query = $conn->prepare("UPDATE users SET reset_token = ? WHERE email = ?");
$query->bind_param("ss", $token, $email);
$query->execute();
```

Đoạn mã trên thiết lập một mã PIN ba chữ số ngẫu nhiên làm mã đặt lại cho email đã gửi. Vì mã này không sử dụng các ký tự hỗn hợp, nên nó có thể dễ dàng bị tấn công bằng phương pháp vét cạn.

Để chứng minh điều này, hãy truy cập  http://enum.thm/labs/predictable_tokens/(mở trong tab mới).

<img width="1980" height="838" alt="image" src="https://github.com/user-attachments/assets/3d609d9f-904f-4d3f-a61d-650b905c21be" />

Truy cập trang đặt lại mật khẩu của ứng dụng, nhập "admin@admin.com" vào trường Email  và nhấn Gửi.

<img width="1934" height="768" alt="image" src="https://github.com/user-attachments/assets/73544285-79f1-4e04-974e-79e1532d5310" />

Ứng dụng sẽ trả về thông báo thành công.

<img width="1880" height="848" alt="image" src="https://github.com/user-attachments/assets/1a93d79e-89d9-40d3-a4a5-dc76a4eeea87" />

Để minh họa, ứng dụng web sử dụng liên kết đặt lại:`http://enum.thm/labs/predictable_tokens/reset_password.php?token=123`

<img width="2998" height="846" alt="image" src="https://github.com/user-attachments/assets/aba480cc-0a87-4714-aac2-4b75a7da650f" />

Lưu ý rằng mã thông báo là một giá trị số đơn giản.  Sử dụng Burp Suite, điều hướng đến URL ở trên và bắt lấy yêu cầu.

Tiếp theo, gửi yêu cầu đến Intruder, chọn giá trị của tham số token và nhấp vào nút Thêm payload, như hình bên dưới.

<img width="2988" height="866" alt="image" src="https://github.com/user-attachments/assets/d512f851-6ced-4bd9-92fe-75535de345ce" />

Sử dụng AttackBox hoặc máy ảo tấn công của riêng bạn, hãy dùng Crunch để tạo ra một danh sách các số từ 100 đến 200. Danh sách này sẽ được sử dụng làm từ điển trong cuộc tấn công vét cạn.

```
user@tryhackme $ crunch 3 3 -o otp.txt -t %%% -s 100 -e 200             

Crunch will now generate the following amount of data: 404 bytes
0 MB
0 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 101

crunch: 100% completed generating output
```

Quay lại Intruder và cấu hình payload để sử dụng tệp đã tạo

<img width="2986" height="1380" alt="image" src="https://github.com/user-attachments/assets/23b566a1-dfe7-4e6e-bd98-6e5c26245430" />

<img width="2720" height="824" alt="image" src="https://github.com/user-attachments/assets/0ad6118b-9ab6-495d-bff6-a590916585c0" />

Nếu bạn đang sử dụng, cuộc tấn công sẽ mất một thời gian để hoàn tất.Burp Suite Phiên bản Cộng đồng. Tuy nhiên, sau khi đăng ký thành công, bạn sẽ nhận được phản hồi có độ dài nội dung lớn hơn nhiều so với các phản hồi có thông báo lỗi "Mã thông báo không hợp lệ".

<img width="2144" height="1330" alt="image" src="https://github.com/user-attachments/assets/bb2fe5b4-9b09-4a98-9b7e-bc1cde021143" />

Đăng nhập vào ứng dụng bằng mật khẩu mới.

<img width="2988" height="466" alt="image" src="https://github.com/user-attachments/assets/667f3705-5746-42e2-b7f9-555902abdae3" />

Xác thực cơ bản trong năm 2024?
Xác thực cơ bản cung cấp một phương pháp đơn giản hơn để bảo mật quyền truy cập vào thiết bị. Nó chỉ yêu cầu tên người dùng và mật khẩu, giúp dễ dàng triển khai và quản lý trên các thiết bị có khả năng xử lý hạn chế.  Các thiết bị mạng như bộ định tuyến thường sử dụng xác thực cơ bản để kiểm soát quyền truy cập vào giao diện quản trị của chúng. Trong trường hợp này, mục tiêu chính là ngăn chặn truy cập trái phép với thiết lập tối thiểu.

Mặc dù xác thực cơ bản không cung cấp các tính năng bảo mật mạnh mẽ như các phương thức phức tạp hơn như OAuth hoặc xác thực dựa trên mã thông báo, nhưng sự đơn giản của nó làm cho nó phù hợp với các môi trường không yêu cầu quản lý phiên và theo dõi người dùng hoặc việc quản lý được thực hiện theo cách khác. Ví dụ, trong các thiết bị như bộ định tuyến chủ yếu được truy cập để thay đổi cấu hình hơn là sử dụng thường xuyên, việc duy trì trạng thái phiên là không cần thiết và có thể làm phức tạp hiệu suất của thiết bị.

HTTPXác thực cơ bản được định nghĩa trongRFC7617(mở trong tab mới)Điều khoản này quy định rằng thông tin đăng nhập (tên người dùng và mật khẩu) phải được truyền tải dưới dạng chuỗi mã hóa base64 trong...HTTPTiêu đề xác thực. Phương pháp này đơn giản nhưng không an toàn trên các kết nối không phải HTTPS, vì base64 không phải là phương pháp mã hóa và có thể dễ dàng giải mã. Mối đe dọa thực sự thường đến từ thông tin đăng nhập yếu có thể bị tấn công bằng phương pháp vét cạn.

HTTPXác thực cơ bản cung cấp một cơ chế thách thức-phản hồi đơn giản để yêu cầu thông tin đăng nhập của người dùng.

<img width="1334" height="1412" alt="image" src="https://github.com/user-attachments/assets/d639a3f7-f782-4868-a59d-71bfbe7bad37" />

Định dạng tiêu đề Ủy quyền như sau:

`Authorization: Basic <credentials>`

`<credentials>` Mã hóa base64 của nằm ở đâu username:password? Để biết thông số kỹ thuật chi tiết, vui lòng tham khảo RFC 7617.(mở trong tab mới).

Sự bóc lột

Để chứng minh điều này, hãy truy cập  http://enum.thm/labs/basic_auth/(mở trong tab mới).

<img width="3014" height="894" alt="image" src="https://github.com/user-attachments/assets/46984d9e-4ea7-4567-b321-fdbed47ec4f3" />

Nhập bất kỳ tên người dùng và mật khẩu nào vào cửa sổ bật lên và thu thập yêu cầu xác thực cơ bản bằng Burp.

<img width="2980" height="846" alt="image" src="https://github.com/user-attachments/assets/b3e79a2e-9240-47c9-b54d-47ee35f3d0e4" />

<img width="2910" height="840" alt="image" src="https://github.com/user-attachments/assets/9a5c873c-789e-4778-a8bc-767030a55e4b" />

Nhấp chuột phải vào yêu cầu và gửi nó đến Intruder.

<img width="2926" height="998" alt="image" src="https://github.com/user-attachments/assets/cf5935f1-518b-4112-b32b-329170322aaa" />

Trong Burp Intruder, hãy vào tab "Positions" và giải mã chuỗi được mã hóa base64 trong tiêu đề Authorization.

<img width="2992" height="1496" alt="image" src="https://github.com/user-attachments/assets/d019ddfe-70b4-4cfb-85ce-5e0b717f9e99" />

Sau khi giải mã, hãy chọn chuỗi đã giải mã và nhấp vào nút Thêm ở góc trên bên phải.

<img width="3000" height="986" alt="image" src="https://github.com/user-attachments/assets/359e6e8d-aed8-4640-a266-e5fb6b7047df" />

Bước tiếp theo là cấu hình payload. Vào tab Payloads và đặt loại payload thành Simple list, sau đó chọn danh sách từ bạn muốn sử dụng. Trong ví dụ này, chúng ta sẽ sử dụng 500-worst-passwords.txt(mở trong tab mới)Từ SecLists. Nếu bạn đang sử dụng AttackBox, bạn có thể sử dụng cùng danh sách từ nằm tại  `/usr/share/wordlists/SecLists/Passwords/Common-Credentials/500-worst-passwords.txt`

<img width="2978" height="1392" alt="image" src="https://github.com/user-attachments/assets/2a12f7b2-f5ec-4b1f-ad49-25ac9fc43c4a" />

Vì phần tiêu đề được mã hóa base64, chúng ta cần thêm hai quy tắc trong phần xử lý Payload. Quy tắc đầu tiên tự động thêm tên người dùng vào mật khẩu, vì vậy thay vì 123456, payload sẽ là "admin:123456".

<img width="2990" height="1432" alt="image" src="https://github.com/user-attachments/assets/8e178bf5-17ea-4127-9001-42b65c59e85e" />

Quy tắc thứ hai sẽ mã hóa base64 tên người dùng và mật khẩu kết hợp từ danh sách được cung cấp.

<img width="2992" height="1414" alt="image" src="https://github.com/user-attachments/assets/bce06391-d3ce-4441-9559-7768c75c79eb" />

Chúng ta cũng nên loại bỏ ký tự "=" (dấu bằng) khỏi mã hóa vì base64 sử dụng "=" để đệm. Để làm điều này, hãy cuộn xuống và xóa dấu "=" khỏi danh sách các ký tự trong phần mã hóa Payload.

<img width="3016" height="1594" alt="image" src="https://github.com/user-attachments/assets/e378a878-ee8e-4f39-93ca-8edb939cb671" />

Sau khi hoàn tất, hãy quay lại tab Vị trí và nhấp vào nút Bắt đầu tấn công. Cuộc tấn công sẽ mất chưa đến 2 phút.

<img width="2682" height="1224" alt="image" src="https://github.com/user-attachments/assets/f15f6c3e-b77d-4ed3-8f56-151490edde00" />

Khi nhận được mã trạng thái 200, điều đó có nghĩa là tấn công vét cạn thành công và một trong những mật khẩu trong danh sách được cung cấp đang hoạt động. Giải mã chuỗi base64 được mã hóa trong yêu cầu thành công.

<img width="2682" height="982" alt="image" src="https://github.com/user-attachments/assets/ec0a1f8f-801c-46ef-ac3c-735546dfb8d6" />

<img width="1010" height="400" alt="image" src="https://github.com/user-attachments/assets/1fca83c8-d2d2-451e-8498-0a78b912bf65" />

Sử dụng chuỗi base64 đã giải mã để đăng nhập vào ứng dụng.

<img width="2266" height="724" alt="image" src="https://github.com/user-attachments/assets/7b7ca10d-a514-4fee-b125-a90771263fbe" />

<img width="1114" height="306" alt="image" src="https://github.com/user-attachments/assets/0e8d1e3c-f570-46f3-838b-c588aeddb3cf" />
