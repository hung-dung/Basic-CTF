Sự trỗi dậy của API

Giao diện lập trình ứng dụng, hay gọi tắt là API, đã trở nên vô cùng phổ biến hiện nay. Một trong những lý do chính cho sự bùng nổ này là khả năng tạo ra một giao diện duy nhất.API Điều này cho phép hệ thống có thể phục vụ nhiều giao diện khác nhau cùng một lúc, chẳng hạn như ứng dụng web và ứng dụng di động. Nhờ đó, logic phía máy chủ được tập trung hóa và tái sử dụng cho tất cả các giao diện. Từ góc độ bảo mật, điều này cũng thường có lợi vì nó cho phép chúng ta triển khai bảo mật phía máy chủ trong một hệ thống duy nhất.APIĐiều đó sẽ bảo vệ máy chủ của chúng ta bất kể giao diện nào đang được sử dụng.

Tuy nhiên, các phương pháp quản lý phiên mới cũng được tạo ra cùng với sự phát triển của API. Vì cookie thường được liên kết với các ứng dụng web được sử dụng thông qua trình duyệt, nên xác thực dựa trên cookie cho API thường không hoạt động hiệu quả vì giải pháp này không tương thích với các giao diện khác. Đây là lúc quản lý phiên dựa trên token phát huy tác dụng.

Quản lý phiên dựa trên mã thông báo

Quản lý phiên dựa trên token là một khái niệm tương đối mới. Thay vì sử dụng các tính năng quản lý cookie tự động của trình duyệt, nó dựa vào mã phía máy khách để thực hiện quy trình. Sau khi xác thực, ứng dụng web cung cấp một token trong phần thân yêu cầu. Sử dụng mã JavaScript phía máy khách, token này sau đó được lưu trữ trong LocalStorage của trình duyệt.

Khi có yêu cầu mới được gửi, mã JavaScript phải tải mã thông báo từ bộ nhớ và đính kèm nó dưới dạng tiêu đề. Một trong những loại mã thông báo phổ biến nhất là JSONWeb Tokens (JWT) được truyền qua `Authorization: Bearer` phần tiêu đề. Tuy nhiên, vì chúng ta không sử dụng các tính năng quản lý cookie tích hợp sẵn của trình duyệt, nên mọi thứ khá hỗn loạn. Mặc dù có các tiêu chuẩn, nhưng không có gì bắt buộc mọi thứ phải tuân theo các tiêu chuẩn này. Các token như JWT là một cách để chuẩn hóa việc quản lý phiên dựa trên token.

Dự án API

Trong phòng học này, bạn sẽ thực hiện khai thác lỗ hổng bảo mật đối với một số API. API có thể được ghi lại thông tin bằng nhiều phương pháp khác nhau. Một phương pháp phổ biến là tạo một Postman dự án hoặc Swagger tập tin. Mặc dù chúng tôi khuyến khích bạn thử nghiệm với các giải pháp này, nhưng chúng yêu cầu bạn phải có tài khoản, điều mà chúng tôi không muốn bắt buộc trong phòng này. Thay vào đó, một giải thích đơn giản về API được cung cấp bên dưới. API vẫn nhất quán cho tất cả các ví dụ ngoại trừ ví dụ cuối cùng, có thêm các tính năng bổ sung. Khi bạn làm bài tập, hãy tham khảo phần này để được hướng dẫn. API được phát triển bằng Python Flask. Do đó, các ví dụ lập trình sẽ được viết bằng Python.

Điểm cuối API

Dự án API chỉ có một điểm cuối API duy nhất, đó là `http://MACHINE_IP/api/v1.0/exampleX` . `X`được thay thế bằng số của ví dụ. Điểm cuối này truy cập hai HTTP phương pháp:

`
Phương thức POST : Để xác thực và nhận JWT, bạn cần thực hiện yêu cầu POST với thông tin xác thực được cung cấp ở định dạng JSON.
GET : Để lấy thông tin chi tiết về người dùng của bạn và cuối cùng thực hiện nâng cao đặc quyền để khôi phục cờ tác vụ của bạn.
`
APIThông tin xác thực

Để xác thực với API Cần gửi một phần thân JSON chứa thông tin xác thực như sau:

tên người dùng : user
mật khẩu : passwordX

Cần `X` phải thay thế bằng số của ví dụ.

Ví dụ về API

Dưới đây là hai yêu cầu cURL bạn có thể sử dụng để tương tác với API. Để xác thực, bạn có thể thực hiện yêu cầu cURL sau:

`curl -H 'Content-Type: application/json' -X POST -d '{ "username" : "user", "password" : "passwordX" }' http://MACHINE_IP/api/v1.0/exampleX`

Để xác minh người dùng, có thể thực hiện yêu cầu cURL sau:

`curl -H 'Authorization: Bearer [JWT token]' http://MACHINE_IP/api/v1.0/example2?username=Y`

Thành phần này `[JWT token]` cần được thay thế bằng JWT nhận được từ yêu cầu đầu tiên. Trong trường hợp này, `Y` nó có thể là `user` hoặc `admin`, tùy thuộc vào quyền hạn của bạn.

API Quyền hạn

Mục tiêu chính trong mỗi ví dụ là giành được quyền quản trị và xác minh các quyền này. Khi bạn có một JWT hợp lệ trong đó admin được đặt là 1, bạn có thể yêu cầu thông tin chi tiết của người dùng quản trị. Thao tác này sẽ trả về cờ của bạn. Quy trình sẽ được hiển thị cho ví dụ đầu tiên, nhưng bạn sẽ phải sao chép các bước cho các ví dụ tiếp theo nghỉ ngơi trong số các ví dụ.

Mã thông báo web JSON

JWT là các mã thông báo độc lập có thể được sử dụng để truyền tải thông tin phiên một cách an toàn. Đây là một tiêu chuẩn mở.(mở trong tab mới)Bài viết này cung cấp thông tin cho bất kỳ nhà phát triển hoặc người tạo thư viện nào muốn sử dụng JWT. Cấu trúc của JWT được thể hiện trong hình ảnh động bên dưới:

Cấu trúc JWT

Một JWT bao gồm ba thành phần, mỗi thành phần được mã hóa Base64Url và phân tách bằng dấu chấm:

Phần tiêu đề - Phần tiêu đề thường cho biết loại mã thông báo, đó là JWT, cũng như thuật toán ký được sử dụng.

Payload - Payload là phần thân của token, chứa các thông tin xác nhận (claims). Thông tin xác nhận là một mẩu thông tin được cung cấp cho một thực thể cụ thể. Trong JWT, có các thông tin xác nhận đã đăng ký (registered claims), là các thông tin được định nghĩa trước bởi tiêu chuẩn JWT, và các thông tin xác nhận công khai hoặc riêng tư (public or private claims). Thông tin xác nhận công khai và riêng tư là những thông tin do nhà phát triển định nghĩa. Việc hiểu rõ sự khác biệt giữa thông tin xác nhận công khai và riêng tư là điều cần thiết, nhưng không phải vì mục đích bảo mật, do đó đây sẽ không phải là trọng tâm của chúng ta trong buổi này.

Chữ ký - Chữ ký là một phần của token cung cấp phương thức để xác minh tính xác thực của token. Chữ ký được tạo ra bằng cách sử dụng thuật toán được chỉ định trong phần tiêu đề của JWT. Chúng ta hãy cùng tìm hiểu sâu hơn về các thuật toán ký chính.
Thuật toán ký

Mặc dù có một số thuật toán khác nhau được định nghĩa trong tiêu chuẩn JWT, nhưng chúng ta chỉ thực sự quan tâm đến ba thuật toán chính:

None - Thuật toán None có nghĩa là không có thuật toán nào được sử dụng cho chữ ký. Về cơ bản, đây là một JWT không có chữ ký, có nghĩa là việc xác minh các thông tin được cung cấp trong JWT không thể được thực hiện thông qua chữ ký.

Ký đối xứng - Thuật toán ký đối xứng, chẳng hạn như HS256, tạo ra chữ ký bằng cách thêm một giá trị bí mật vào phần đầu và phần thân của JWT trước khi tạo ra giá trị băm. Việc xác minh chữ ký có thể được thực hiện bởi bất kỳ hệ thống nào biết khóa bí mật.

Ký bất đối xứng - Thuật toán ký bất đối xứng, chẳng hạn như RS256, tạo chữ ký bằng cách sử dụng khóa riêng để ký phần tiêu đề và phần thân của JWT. Quá trình này được thực hiện bằng cách tạo ra hàm băm và sau đó mã hóa hàm băm bằng khóa riêng. Việc xác minh chữ ký có thể được thực hiện bởi bất kỳ hệ thống nào biết khóa công khai liên kết với khóa riêng được sử dụng để tạo chữ ký.

Bảo mật trong chữ ký

JWT có thể được mã hóa (gọi là JWE), nhưng sức mạnh chính của JWT đến từ chữ ký. Sau khi JWT được ký, nó có thể được gửi đến máy khách, người có thể sử dụng JWT này ở bất cứ nơi nào cần thiết. Chúng ta có thể có một máy chủ xác thực tập trung tạo ra các JWT được sử dụng trên nhiều ứng dụng. Mỗi ứng dụng sau đó có thể xác minh chữ ký của JWT; nếu được xác minh, các thông tin được cung cấp trong JWT có thể được tin tưởng và sử dụng.

Tiết lộ thông tin nhạy cảm

Vấn đề phổ biến đầu tiên mà chúng ta sẽ đi sâu vào là việc lộ thông tin nhạy cảm trong JWT.

Một phương pháp quản lý phiên dựa trên cookie phổ biến là sử dụng phiên phía máy chủ để lưu trữ một số tham số. TrongPHPVí dụ, bạn có thể sử dụng `$SESSION['var']=data` để lưu trữ một giá trị liên kết với phiên của người dùng. Các giá trị này không được hiển thị ở phía máy khách và do đó chỉ có thể được khôi phục ở phía máy chủ. Tuy nhiên, với token, các thông tin xác thực sẽ bị lộ vì toàn bộ JWT được gửi đến phía máy khách. Nếu áp dụng cùng một phương pháp phát triển, thông tin nhạy cảm có thể bị tiết lộ. Một số ví dụ được thấy trong các ứng dụng thực tế:

Việc tiết lộ thông tin đăng nhập bằng cách sử dụng mã băm mật khẩu, hoặc tệ hơn nữa, gửi mật khẩu dạng văn bản gốc dưới dạng yêu cầu xác thực.
Việc để lộ thông tin mạng nội bộ, chẳng hạn như địa chỉ IP riêng hoặc tên máy chủ của máy chủ xác thực.
Ví dụ thực tế 1

Hãy cùng xem một ví dụ thực tế. Chúng ta hãy xác thực với hệ thống của mình.APIsử dụng yêu cầu cURL sau:

`curl -H 'Content-Type: application/json' -X POST -d '{ "username" : "user", "password" : "password1" }' http://MACHINE_IP/api/v1.0/example1`

Thao tác này sẽ cung cấp cho bạn một mã thông báo JWT. Sau khi khôi phục, hãy giải mã phần thân của JWT để tìm ra thông tin nhạy cảm. Bạn có thể giải mã phần thân theo cách thủ công hoặc sử dụng một trang web như `JWT.io` cho quá trình này.

Sai lầm trong quá trình phát triển

Trong ví dụ này, thông tin nhạy cảm đã được thêm vào yêu cầu bồi thường, như thể hiện bên dưới:
```
payload = {
    "username" : username,
    "password" : password,
    "admin" : 0,
    "flag" : "[redacted]"
}

access_token = jwt.encode(payload, self.secret, algorithm="HS256")
```
Giải pháp

Các giá trị như mật khẩu hoặc cờ không nên được thêm vào dưới dạng thông tin xác thực vì JWT sẽ được gửi ở phía máy khách. Thay vào đó, các giá trị này nên được lưu trữ an toàn ở phía máy chủ trong phần phụ trợ. Khi cần thiết, tên người dùng có thể được đọc từ JWT đã được xác thực và được sử dụng để tra cứu các giá trị này, như được minh họa trong ví dụ bên dưới:
```
payload = jwt.decode(token, self.secret, algorithms="HS256")

username = payload['username']
flag = self.db_lookup(username, "flag")
```
