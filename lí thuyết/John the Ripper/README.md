Có nhiều cách để sử dụng John the Ripper

Để giải mã các hàm băm đơn giản. Chúng ta sẽ cùng xem xét một vài hàm băm trước khi tự mình thực hiện việc giải mã một số hàm băm khác.
Cú pháp cơ bản của John

Cú pháp cơ bản của John the Ripper

Các lệnh như sau. Chúng ta sẽ tìm hiểu các tùy chọn và bổ ngữ cụ thể được sử dụng khi chúng ta dùng chúng.

`john [options] [file path]`

`john`: Kích hoạt chương trình John the Ripper
`[options]`: Chỉ định các tùy chọn bạn muốn sử dụng
`[file path]`: Đây là tệp chứa mã băm mà bạn đang cố gắng giải mã; nếu tệp nằm trong cùng thư mục, bạn không cần phải chỉ định đường dẫn, chỉ cần chỉ định tên tệp.

Ví dụ sử dụng:

`john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt`

Để sử dụng mã định danh băm, bạn có thể sử dụng wget hoặc curlđể tải xuống tệp Python `hash-id.py` GitLab của nó Tải xuống từ trang (mở trong tab mới) . Sau đó, khởi chạy nó bằng lệnh `python3 hash-id.py` và nhập mã băm mà bạn đang cố gắng xác định. Nó sẽ cung cấp cho bạn danh sách các định dạng có khả năng nhất. Hai bước này được hiển thị trong cửa sổ dòng lệnh bên dưới.

`wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py`

` python3 hash-id.py`

Bẻ khóa theo định dạng cụ thể

Khi bạn đã xác định được mã băm cần xử lý, bạn có thể yêu cầu John sử dụng mã băm đó trong quá trình giải mã bằng cú pháp sau:

`john --format=[format] --wordlist=[path to wordlist] [path to file]`

`--format=`:Đây là tín hiệu để báo cho John biết rằng bạn đang cung cấp cho nó một mã băm có định dạng cụ thể và yêu cầu nó sử dụng định dạng sau để giải mã.
`[format]`: Định dạng của mã băm

Ví dụ sử dụng:

`john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt`

Lưu ý về định dạng:

Khi bạn bảo John sử dụng các định dạng, nếu bạn đang làm việc với một kiểu băm chuẩn, ví dụ:

Như trong ví dụ trên, bạn phải thêm tiền tố là raw-Bạn có thể nói với John rằng bạn chỉ đang làm việc với một kiểu băm tiêu chuẩn, mặc dù điều này không phải lúc nào cũng đúng. Để kiểm tra xem bạn có cần thêm tiền tố hay không, bạn có thể liệt kê tất cả các định dạng của John bằng cách sử dụng `john --list=formats`và kiểm tra thủ công hoặc tìm kiếm kiểu băm của bạn bằng một công cụ như sau: `john --list=formats | grep -iF "md5" `.


NTHash / NTLM  <br>

NThash là định dạng băm mà các máy tính chạy hệ điều hành Windows hiện đại sử dụng để lưu trữ mật khẩu người dùng và dịch vụ. Nó cũng thường được gọi là...NTLM, điều này đề cập đến phiên bản trước của định dạng băm mật khẩu của Windows được gọi là LM, do đó là NT/LM.

Một chút lịch sử: ký hiệu NT cho các sản phẩm Windows ban đầu có nghĩa là Công nghệ Mới. Nó được sử dụng bắt đầu từ Windows NT để chỉ các sản phẩm không được xây dựng từ nền tảng MS-DOS. Cuối cùng, dòng "NT" trở thành loại hệ điều hành tiêu chuẩn được Microsoft phát hành, và tên gọi này đã bị loại bỏ, nhưng nó vẫn còn tồn tại trong tên của một số công nghệ của Microsoft.

Trong Windows, SAM (Security Account Manager) được sử dụng để lưu trữ thông tin tài khoản người dùng, bao gồm tên người dùng và mật khẩu đã được mã hóa. Bạn có thể tải xuống NTHash/NTLM
Tìm mã băm bằng cách sao lưu cơ sở dữ liệu SAM trên máy tính Windows, sử dụng công cụ như Mimikatz hoặc sử dụng cơ sở dữ liệu Active Directory: `NTDS.dit` Bạn có thể không cần phải bẻ khóa mã băm để tiếp tục leo thang đặc quyền, vì bạn thường có thể thực hiện tấn công "truyền mã băm" thay thế, nhưng đôi khi, bẻ khóa mã băm là một lựa chọn khả thi nếu chính sách mật khẩu yếu. 

Giải mã băm từ /etc/shadow <br>

/etc/shadow là tệp trên máy Linux nơi lưu trữ các mã băm mật khẩu. Nó cũng lưu trữ các thông tin khác, chẳng hạn như ngày thay đổi mật khẩu lần cuối và thông tin về thời hạn hết hạn của mật khẩu. Mỗi dòng chứa một mục nhập cho mỗi người dùng hoặc tài khoản người dùng của hệ thống. Tệp này thường chỉ có thể truy cập được bởi người dùng root, vì vậy bạn phải có đủ đặc quyền để truy cập các mã băm. Tuy nhiên, nếu bạn có đủ đặc quyền, bạn có khả năng sẽ giải mã được một số mã băm đó.

Unshadow

John rất khắt khe về định dạng dữ liệu cần thiết để có thể làm việc với nó; vì lý do này, để bẻ khóa... `/etc/shadow`, bạn phải kết hợp nó với `/etc/passwd` Tệp này giúp John hiểu được dữ liệu được cung cấp. Để làm điều này, chúng tôi sử dụng một công cụ được tích hợp sẵn trong bộ công cụ của John, có tên là... `unshadow `Cú pháp cơ bản của unshadowCụ thể như sau:

`unshadow [path to passwd] [path to shadow]`

    `unshadow`: Kích hoạt công cụ bỏ bóng
    `[path to passwd]`: Tệp chứa bản sao của /etc/passwdtập tin bạn đã lấy từ máy tính trong phòng thí nghiệm
    `[path to shadow]`: Tệp chứa bản sao của /etc/shadowtập tin bạn đã lấy từ máy tính trong phòng thí nghiệm

Ví dụ sử dụng:

`unshadow local_passwd local_shadow > unshadowed.txt`

Ghi chú về các tệp

Khi sử dụng `unshadow` Bạn có thể sử dụng toàn bộ `/etc/passwd` Và `/etc/shadow`, giả sử bạn có sẵn chúng, hoặc bạn có thể sử dụng dòng liên quan từ mỗi tệp, ví dụ:

TỆP 1 - local_passwd

Chứa /etc/passwd` dòng lệnh dành cho người dùng root:

`root:x:0:0::/root:/bin/bash`

TỆP 2 - local_shadow

Chứa `/etc/shadow` dòng lệnh dành cho người dùng root: `root:$6$2nwjN454g.dv4HN/$m9Z/r2xVfweYVkrr.v5Ft8Ws3/YYksfNwq96UL1FX0OJjY1L6l.DS3KEVsZ9rOVLB/ldTeEL/OIhJZ4GMFMGA0:18576::::::`
Phá vỡ

Sau đó, chúng ta có thể đưa đầu ra từ vào. `unshadow`, trong trường hợp sử dụng ví dụ của chúng tôi được gọi là `unshadowed.txt` Trực tiếp vào John. Chúng ta không cần phải chỉ định chế độ ở đây vì chúng ta đã tạo đầu vào dành riêng cho John; tuy nhiên, trong một số trường hợp, bạn sẽ cần chỉ định định dạng như chúng ta đã làm trước đây bằng cách sử dụng: `--format=sha512crypt`

`john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt`
