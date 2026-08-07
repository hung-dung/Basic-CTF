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

Những lỗi trong quá trình xác thực chữ ký

Lỗi phổ biến thứ hai với JWT là không xác minh chữ ký đúng cách. Nếu chữ ký không được xác minh chính xác, kẻ tấn công có thể làm giả mã thông báo JWT hợp lệ để truy cập vào tài khoản của người dùng khác. Hãy cùng xem xét các vấn đề thường gặp khi xác minh chữ ký.

Không xác minh chữ ký

Vấn đề đầu tiên với việc xác thực chữ ký là khi không có bất kỳ bước xác thực chữ ký nào được thực hiện. Nếu máy chủ không xác minh chữ ký của JWT, thì có thể sửa đổi các thông tin trong JWT theo ý muốn của bạn. Mặc dù hiếm khi tìm thấy các API không thực hiện xác thực chữ ký, nhưng việc xác thực chữ ký có thể đã bị bỏ qua ở một điểm cuối duy nhất trong hệ thống.APITùy thuộc vào mức độ nhạy cảm của điểm cuối, điều này có thể gây ra tác động đáng kể đến hoạt động kinh doanh.

Ví dụ thực tế 2

Hãy xác thực vớiAPI:

`curl -H 'Content-Type: application/json' -X POST -d '{ "username" : "user", "password" : "password2" }' http://10.112.178.211/api/v1.0/example2`

Sau khi xác thực thành công, hãy xác minh người dùng của chúng ta:

`curl -H 'Authorization: Bearer [JWT Token]' http://10.112.178.211/api/v1.0/example2?username=user`

Tuy nhiên, hãy thử xác minh người dùng của chúng ta mà không cần chữ ký, xóa phần thứ ba của JWT (chỉ để lại dấu chấm) và thực hiện lại yêu cầu. Bạn sẽ thấy rằng quá trình xác minh vẫn hoạt động! Điều này có nghĩa là chữ ký không được xác minh. Hãy sửa đổi trường "admin" trong payload thành 1và thử xác minh với tư cách người dùng quản trị để lấy cờ của bạn.

Sai lầm trong quá trình phát triển

Trong ví dụ này, chữ ký không được xác minh, như minh họa bên dưới:

`payload = jwt.decode(token, options={'verify_signature': False})`
﻿Mặc dù hiếm khi thấy điều này trên các API thông thường, nhưng nó thường xảy ra trên các API máy chủ-máy chủ. Trong trường hợp kẻ tấn công có quyền truy cập trực tiếp vào máy chủ phụ trợ, JWT có thể bị làm giả.

Giải pháp

JWT luôn cần được xác minh hoặc sử dụng các yếu tố xác thực bổ sung, chẳng hạn như chứng chỉ, để liên lạc giữa các máy chủ. JWT có thể được xác minh bằng cách cung cấp khóa bí mật (hoặc khóa công khai), như trong ví dụ bên dưới:

`payload = jwt.decode(token, self.secret, algorithms="HS256")`

Hạ cấp xuống mức Không có

Một vấn đề phổ biến khác là việc hạ cấp thuật toán chữ ký. JWT hỗ trợ Nonethuật toán ký, điều này có nghĩa là thực tế không có chữ ký nào được sử dụng với JWT. Mặc dù điều này nghe có vẻ ngớ ngẩn, nhưng ý tưởng đằng sau tiêu chuẩn này là dành cho giao tiếp giữa các máy chủ, trong đó chữ ký của JWT được xác minh trong một quy trình ở phía máy chủ trước đó. Do đó, máy chủ thứ hai sẽ không cần phải xác minh chữ ký. Tuy nhiên, giả sử các nhà phát triển không khóa thuật toán chữ ký hoặc, ít nhất, từ chối `None` thuật toán đó. Trong trường hợp đó, bạn chỉ cần thay đổi thuật toán được chỉ định trong JWT của mình thành None, điều này sẽ khiến thư viện được sử dụng để xác minh chữ ký luôn trả về true, do đó cho phép bạn lại làm giả bất kỳ thông tin nào trong token của mình.

Ví dụ thực tế 3

Xác thực với API để nhận JWT và sau đó xác minh người dùng của bạn. Để thực hiện cuộc tấn công này, bạn cần tự tay thay đổi trường algclaim trong header thành None. Bạn có thể sử dụng CyberChef.(mở trong tab mới)Để làm điều này, hãy sử dụng tùy chọn Base64 được mã hóa URL. Gửi lại JWT để xác minh rằng nó vẫn được chấp nhận, ngay cả khi chữ ký không còn hợp lệ do đã có những thay đổi. Sau đó, bạn có thể sửa đổi phần adminxác nhận để khôi phục cờ.

Sai lầm trong quá trình phát triển

Mặc dù thoạt nhìn có vẻ giống vấn đề trước đây, nhưng xét từ góc độ phát triển, nó phức tạp hơn một chút. Đôi khi, các nhà phát triển muốn đảm bảo rằng việc triển khai của họ chấp nhận nhiều thuật toán xác thực chữ ký JWT khác nhau. Khi đó, việc triển khai thường sẽ đọc phần tiêu đề của JWT và phân tích thuật toán tìm thấy thành phần xác thực chữ ký, như được minh họa bên dưới:
```
header = jwt.get_unverified_header(token)

signature_algorithm = header['alg']

payload = jwt.decode(token, self.secret, algorithms=signature_algorithm)
```
Tuy nhiên, khi tác nhân đe dọa chỉ Noneđịnh thuật toán, quá trình xác minh chữ ký sẽ bị bỏ qua. Pyjwt(mở trong tab mới)Thư viện JWT được sử dụng trong phòng này đã triển khai mã hóa bảo mật để ngăn chặn vấn đề này. Nếu một khóa bí mật được chỉ định khi thuật toán None được chọn, một ngoại lệ sẽ được đưa ra.

Giải pháp

Nếu cần hỗ trợ nhiều thuật toán chữ ký, các thuật toán được hỗ trợ cần được cung cấp cho hàm giải mã dưới dạng một danh sách mảng, như minh họa bên dưới:
```
payload = jwt.decode(token, self.secret, algorithms=["HS256", "HS384", "HS512"])

username = payload['username']
flag = self.db_lookup(username, "flag")
```
Bí mật đối xứng yếu

Nếu sử dụng thuật toán ký đối xứng, tính bảo mật của JWT phụ thuộc vào độ mạnh và độ phức tạp của khóa bí mật được sử dụng. Nếu sử dụng khóa bí mật yếu, có thể thực hiện tấn công bẻ khóa ngoại tuyến để khôi phục khóa bí mật. Sau khi biết được giá trị khóa bí mật, bạn có thể thay đổi các thông tin trong JWT và tính toán lại chữ ký hợp lệ bằng cách sử dụng khóa bí mật đó.

Ví dụ thực tế 4

Trong ví dụ này, một khóa bí mật yếu đã được sử dụng để tạo JWT. Sau khi nhận được JWT, bạn có một số tùy chọn để bẻ khóa khóa bí mật đó. Trong ví dụ này, chúng ta sẽ nói về việc sử dụng Hashcat.(mở trong tab mới)Để giải mã bí mật của JWT. Bạn cũng có thể sử dụng các giải pháp khác như John.(mở trong tab mới)Ngoài ra, bạn có thể sử dụng các bước sau để giải mã bí mật:

Lưu JWT vào một tệp văn bản có tên là jwt.txt.
Tải xuống danh sách bí mật JWT thông dụng. Đối với phòng này, bạn có thể sử dụng `wget https://raw.githubusercontent.com/wallarm/jwt-secrets/master/jwt.secrets.list` để tải xuống danh sách đó.
Sử dụng Hashcat để giải mã bí mật bằng cách sử dụng `hashcat -m 16500 -a 0 jwt.txt jwt.secrets.list`
Khi bạn biết được bí mật là gì, bạn có thể tạo một mã thông báo quản trị mới để khôi phục cờ!

Sai lầm trong quá trình phát triển

Vấn đề xảy ra khi sử dụng khóa bí mật JWT yếu. Điều này thường xảy ra khi các nhà phát triển vội vàng hoặc sao chép mã từ các ví dụ.

Giải pháp

Cần chọn một giá trị bí mật an toàn. Vì giá trị này sẽ được sử dụng trong phần mềm chứ không phải bởi con người, nên cần sử dụng một chuỗi ký tự ngẫu nhiên dài làm giá trị bí mật.

Nhầm lẫn thuật toán chữ ký

Vấn đề phổ biến cuối cùng với việc xác thực chữ ký là khi có thể thực hiện tấn công nhầm lẫn thuật toán. Điều này tương tự như `None` tấn công hạ cấp, tuy nhiên, nó xảy ra cụ thể khi có sự nhầm lẫn giữa các thuật toán ký đối xứng và bất đối xứng. Ví dụ, nếu sử dụng thuật toán ký bất đối xứng, chẳng hạn như RS256, thì có thể hạ cấp thuật toán xuống HS256. Trong những trường hợp này, một số thư viện sẽ mặc định sử dụng khóa công khai làm khóa bí mật cho thuật toán ký đối xứng. Vì khóa công khai có thể được biết, bạn có thể làm giả một chữ ký hợp lệ bằng cách sử dụng thuật toán HS256 kết hợp với khóa công khai.

Ví dụ thực tế 5

Điều này tương tự như ví dụ 3. Ngoại trừ lần này, thuật toán None không được phép sử dụng. Tuy nhiên, sau khi xác thực với ví dụ, bạn cũng sẽ nhận được khóa công khai. Vì khóa công khai không được coi là thông tin nhạy cảm, nên việc tìm thấy khóa công khai là khá phổ biến. Đôi khi, khóa công khai thậm chí còn được nhúng như một yêu cầu trong JWT. Trong ví dụ này, bạn phải hạ cấp thuật toán xuống HS256 và sau đó sử dụng khóa công khai làm bí mật để ký JWT. Bạn có thể sử dụng đoạn mã được cung cấp bên dưới để hỗ trợ bạn tạo JWT giả mạo này:
```
import jwt

public_key = "ADD_KEY_HERE"

payload = {
    'username' : 'user',
    'admin' : 0
}

access_token = jwt.encode(payload, public_key, algorithm="HS256")
print (access_token)
```

Lưu ý: Chúng tôi khuyên bạn nên sử dụng AttackBox cho ví dụ thực tế này vì Pyjwt đã được cài đặt sẵn. Trước khi chạy script, hãy chỉnh sửa tệp `/usr/lib/python3/dist-packages/jwt/algorithms.py` bằng trình soạn thảo văn bản yêu thích của bạn và chuyển đến dòng 143. Sau đó, tiến hành bình luận các dòng 143-146và chạy script. Nếu bạn đang sử dụng máy ảo của riêng mình, bạn có thể phải cài đặt Pyjwt ( pip3 install pyjwt) để sử dụng script này. Bạn cũng cần chỉnh sửa tệp `algorithm.py` của thư viện Pyjwt ở dòng 258 để xóa `is_ssh_key` điều kiện vì bản vá cho lỗ hổng này đã được phát hành. Hãy nhớ rằng vị trí này có thể khác nhau tùy thuộc vào máy ảo và cài đặt. Một phương pháp dễ dàng hơn nếu bạn không thoải mái với việc chỉnh sửa mã thư viện là sử dụng  jwt.io Sau khi xác minh nó hoạt động, bạn có thể sửa đổi các yêu cầu để tự mình trở thành quản trị viên và khôi phục cờ.

Sai lầm trong quá trình phát triển

Lỗi trong ví dụ này tương tự như ví dụ 3 nhưng phức tạp hơn một chút. Mặc dù thuật toán None bị cấm, vấn đề chính nằm ở chỗ cả thuật toán chữ ký đối xứng và bất đối xứng đều được cho phép, như được minh họa trong ví dụ bên dưới:
```
payload = jwt.decode(token, self.secret, algorithms=["HS256", "HS384", "HS512", "RS256", "RS384", "RS512"])
```
Cần hết sức cẩn thận để không bao giờ trộn lẫn các thuật toán chữ ký với nhau vì tham số bí mật của hàm giải mã có thể bị nhầm lẫn giữa khóa bí mật và khóa công khai.

Giải pháp

Mặc dù cả hai loại thuật toán chữ ký đều được cho phép, nhưng cần thêm một chút logic để đảm bảo không có sự nhầm lẫn, như ví dụ dưới đây minh họa:
```
header = jwt.get_unverified_header(token)

algorithm = header['alg']
payload = ""

if "RS" in algorithm:
    payload = jwt.decode(token, self.public_key, algorithms=["RS256", "RS384", "RS512"])
elif "HS" in algorithm:
    payload = jwt.decode(token, self.secret, algorithms=["HS256", "HS384", "HS512"])

username = payload['username']
flag = self.db_lookup(username, "flag")
```
