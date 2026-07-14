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

John cũng có một chế độ khác, được gọi là chế độ Bẻ khóa đơn lẻ . Trong chế độ này, John chỉ sử dụng thông tin được cung cấp trong tên người dùng để cố gắng tìm ra các mật khẩu khả thi bằng cách thay đổi nhẹ các chữ cái và số có trong tên người dùng.

Biến đổi từ ngữ

Cách tốt nhất để giải thích chế độ Single Crack và word mangling là thông qua một ví dụ:

Hãy xem xét tên người dùng “Markus”.

Một số mật khẩu khả thi có thể là:

    Markus1, Markus2, Markus3 (v.v.)
    MARkus, MARkus, MARKus (v.v.)
    Markus!, Markus$, Markus* (v.v.)

Kỹ thuật này được gọi là biến đổi từ ngữ (word mangling). John xây dựng từ điển của mình dựa trên thông tin được cung cấp và sử dụng một tập hợp các quy tắc gọi là "quy tắc biến đổi từ ngữ", xác định cách nó có thể biến đổi từ ban đầu để tạo ra một danh sách từ dựa trên các yếu tố liên quan đến mục tiêu mà bạn đang cố gắng bẻ khóa. Điều này khai thác điểm yếu của mật khẩu dựa trên thông tin về tên người dùng hoặc dịch vụ mà người dùng đang đăng nhập.
GECOS

Phương pháp mã hóa từ ngữ của John cũng tương thích với trường GECOS của hệ điều hành UNIX, cũng như các hệ điều hành tương tự UNIX khác như... LINUX GECOS

GECOS là viết tắt của General Electric Comprehensive Operating System (Hệ điều hành toàn diện của General Electric). Trong bài tập trước, chúng ta đã xem xét các mục nhập cho cả hai. `/etc/shadow` Và `/etc/passwd` Nếu quan sát kỹ, bạn sẽ thấy các trường được phân tách bằng dấu hai chấm. :Trường thứ năm trong bản ghi tài khoản người dùng là trường GECOS. Nó lưu trữ thông tin chung về người dùng, chẳng hạn như họ tên đầy đủ, số văn phòng và số điện thoại, cùng nhiều thông tin khác. John có thể lấy thông tin được lưu trữ trong các bản ghi đó, chẳng hạn như họ tên đầy đủ và tên thư mục nhà, để thêm vào danh sách từ mà nó tạo ra khi bẻ khóa. `/etc/shadow` Các hàm băm với chế độ bẻ khóa đơn.
Sử dụng chế độ nứt đơn

Để sử dụng chế độ bẻ khóa đơn lẻ, chúng ta sử dụng cú pháp tương tự như đã sử dụng trước đây; ví dụ, nếu muốn bẻ khóa mật khẩu của người dùng có tên “Mike”, bằng chế độ đơn lẻ, chúng ta sẽ sử dụng:

`john --single --format=[format] [path to file]`

    --singleCờ này báo cho John biết bạn muốn sử dụng chế độ bẻ khóa băm đơn.
    --format=[format]Như mọi khi, việc xác định đúng định dạng là vô cùng quan trọng.

Ví dụ sử dụng:

`john --single --format=raw-sha256 hashes.txt`

Lưu ý về định dạng tập tin ở chế độ bẻ khóa đơn:

Nếu bạn đang bẻ khóa mã băm ở chế độ bẻ khóa đơn lẻ, bạn cần thay đổi định dạng tệp mà bạn cung cấp cho John để nó hiểu dữ liệu nào cần dùng để tạo danh sách từ. Bạn thực hiện điều này bằng cách thêm tên người dùng mà mã băm đó thuộc về vào đầu mã băm, vì vậy theo ví dụ trên, chúng ta sẽ thay đổi tệp `hashes.txt`

Từ `1efee03cdcb96d90ad48ccc7b8666033`

ĐẾN `mike:1efee03cdcb96d90ad48ccc7b8666033`

Quy tắc tùy chỉnh là gì?

Khi chúng ta tìm hiểu những gì John có thể làm ở Chế độ Bẻ khóa Đơn lẻ, bạn có thể đã có một số ý tưởng về các mẫu biến đổi mật khẩu tốt hoặc các mẫu mà mật khẩu của bạn thường sử dụng có thể được sao chép bằng một mẫu biến đổi mật khẩu cụ thể. Tin tốt là bạn có thể định nghĩa các quy tắc của riêng mình, mà John sẽ sử dụng để tạo mật khẩu một cách linh hoạt. Khả năng định nghĩa các quy tắc như vậy rất hữu ích khi bạn biết nhiều thông tin hơn về cấu trúc mật khẩu của mục tiêu mà bạn đang nhắm đến.

Các quy tắc tùy chỉnh thông thường

Nhiều tổ chức sẽ yêu cầu mật khẩu có độ phức tạp nhất định để chống lại các cuộc tấn công bằng từ điển. Nói cách khác, khi tạo tài khoản mới hoặc thay đổi mật khẩu, nếu bạn cố gắng sử dụng mật khẩu như... polopasswordNếu không, rất có thể nó sẽ không hoạt động. Lý do là do độ phức tạp của mật khẩu được quy định. Do đó, bạn có thể nhận được thông báo cho biết mật khẩu phải chứa ít nhất một ký tự từ mỗi loại sau:

    Chữ cái viết thường
    Chữ cái viết hoa
    Con số
    Biểu tượng

Độ phức tạp của mật khẩu là tốt! Tuy nhiên, chúng ta có thể tận dụng thực tế là hầu hết người dùng đều có thể đoán được vị trí của các ký hiệu này. Với các tiêu chí trên, nhiều người dùng sẽ sử dụng mật khẩu kiểu như sau:

`Polopassword1!`

Hãy xem xét mật khẩu có chữ cái viết hoa đầu tiên, tiếp theo là một số và cuối cùng là một ký hiệu. Mẫu mật khẩu quen thuộc này, được thêm vào trước và sau bởi các ký hiệu (như chữ cái viết hoa hoặc ký hiệu), là một mẫu dễ nhớ mà mọi người thường sử dụng và tái sử dụng khi tạo mật khẩu. Mẫu này cho phép chúng ta khai thác khả năng dự đoán độ phức tạp của mật khẩu.

Điều này đáp ứng được yêu cầu về độ phức tạp của mật khẩu; tuy nhiên, với tư cách là kẻ tấn công, chúng ta có thể lợi dụng việc biết vị trí có khả năng xuất hiện của các yếu tố được thêm vào này để tạo ra mật khẩu động từ danh sách từ của mình.

Cách tạo quy tắc tùy chỉnh

Các quy tắc tùy chỉnh được định nghĩa trong john.conftập tin. Tập tin này có thể được tìm thấy trong `/opt/john/``john.conf` Trên hộp tấn công TryHackMe. Nó thường nằm ở vị trí... `/etc/john`  `/john.conf` Nếu bạn đã cài đặt John bằng trình quản lý gói hoặc biên dịch từ mã nguồn với make.

Hãy cùng xem xét cú pháp của các quy tắc tùy chỉnh này, sử dụng ví dụ trên làm mẫu mục tiêu. Lưu ý rằng bạn có thể định nghĩa mức độ kiểm soát chi tiết rất cao trong các quy tắc này. Tôi khuyên bạn nên xem tại đây `https://www.openwall.com/john/doc/RULES.shtml` (mở trong tab mới) để có cái nhìn toàn diện về các bổ ngữ bạn có thể sử dụng và nhiều ví dụ hơn về cách triển khai quy tắc.

Dòng đầu tiên:

`[List.Rules:THMRules]` Tham số này được dùng để định nghĩa tên của quy tắc; đây là tham số bạn sẽ sử dụng để gọi quy tắc tùy chỉnh của mình là đối số John.

Sau đó, chúng ta sử dụng mẫu khớp kiểu regex để xác định vị trí từ sẽ được sửa đổi; một lần nữa, ở đây chúng ta chỉ đề cập đến các từ sửa đổi chính và phổ biến nhất:

    Az: Lấy từ và nối thêm các ký tự bạn định nghĩa vào sau.
    A0: Lấy từ và thêm các ký tự bạn định nghĩa vào đầu từ đó.
    c: Viết hoa chữ cái theo vị trí

Những công cụ này có thể được sử dụng kết hợp để xác định vị trí và nội dung trong từ mà bạn muốn sửa đổi.

Cuối cùng, chúng ta cần xác định những ký tự nào nên được thêm vào đầu, cuối hoặc bao gồm bằng cách nào khác. Chúng ta thực hiện điều này bằng cách thêm các nhóm ký tự trong dấu ngoặc vuông `[ ]` Vị trí sử dụng phù hợp. Các quy tắc này tuân theo các mẫu bổ ngữ bên trong dấu ngoặc kép `" "` Dưới đây là một số ví dụ phổ biến:

    [0-9]Sẽ bao gồm các số từ 0 đến 9.
    [0]: Chỉ bao gồm số 0
    [A-z]Sẽ bao gồm cả chữ hoa và chữ thường.
    [A-Z]: Chỉ bao gồm các chữ cái viết hoa
    [a-z]: Chỉ bao gồm các chữ cái viết thường

Xin lưu ý rằng:

    [a]Sẽ chỉ bao gồm a
    [!£$%@]Sẽ bao gồm các ký hiệu. !, £, $, %, Và @

Tóm lại, để tạo ra một danh sách từ dựa trên các quy tắc sao cho phù hợp với mật khẩu ví dụ. Polopassword1!(giả sử từ này) polopassword(nếu từ đó có trong danh sách từ của chúng tôi), chúng tôi sẽ tạo một mục quy tắc có dạng như sau:

`[List.Rules:PoloPassword]`

`cAz"[0-9] [!£$%@]"`

Sử dụng các yếu tố sau:

    c: Viết hoa chữ cái đầu tiên
    Az: Được thêm vào cuối từ
    [0-9]: Một số nằm trong khoảng từ 0 đến 9.
    [!£$%@]: Mật khẩu được theo sau bởi một trong những ký hiệu này.

Sử dụng các quy tắc tùy chỉnh

Sau đó, chúng ta có thể gọi quy tắc tùy chỉnh này là một đối số John bằng cách sử dụng `--rule=PoloPassword`lá cờ.

Dưới dạng một lệnh đầy đủ: `john --wordlist=[path to wordlist] --rule=PoloPassword [path to file]`

Lưu ý rằng, tôi thấy việc trình bày rõ các mẫu khi viết quy tắc rất hữu ích; như đã nêu ở trên, điều tương tự cũng áp dụng khi viết các mẫu RegEx.

Jumbo John đã có sẵn một danh sách đầy đủ các quy tắc tùy chỉnh chứa các bổ ngữ để sử dụng trong hầu hết mọi trường hợp. Nếu bạn gặp khó khăn, hãy thử xem các quy tắc đó [khoảng dòng 678] nếu cú ​​pháp của bạn không hoạt động chính xác.

Zip2John

Tương tự như `unshadow`công cụ mà chúng ta đã sử dụng trước đây, chúng ta sẽ sử dụng `zip2john` Công cụ này dùng để chuyển đổi tập tin Zip thành định dạng băm mà John có thể hiểu và hy vọng là có thể giải mã. Cách sử dụng chính như sau:

`zip2john [options] [zip file] > [output file]`

    [options]: Cho phép bạn truyền các tùy chọn kiểm tra tổng cụ thể đến zip2john Điều này thường không cần thiết.
    [zip file]: Đường dẫn đến tệp Zip mà bạn muốn lấy mã băm (hash) của tệp đó.
    >: Lệnh này chuyển hướng đầu ra của lệnh này sang một tệp khác.
    [output file]: Đây là tệp sẽ lưu trữ kết quả đầu ra.

Ví dụ sử dụng

`zip2john zipfile.zip > zip_hash.txt`

Phá vỡ

Sau đó, chúng ta có thể lấy tập tin mà chúng ta đã xuất ra. `zip2john` trong trường hợp sử dụng ví dụ của chúng tôi, `zip_hash.txt` và, như chúng ta đã làm với `unshadow` Hãy chuyển trực tiếp dữ liệu đó cho John vì chúng ta đã tạo đầu vào dành riêng cho việc này.

`john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt`
