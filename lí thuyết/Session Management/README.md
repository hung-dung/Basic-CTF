Trước khi bàn về tất cả những vấn đề có thể xảy ra, chúng ta cần tìm hiểu về quản lý phiên. Như đã đề cập trong bài tập trước, bạn không gửi tên người dùng và mật khẩu của mình cùng với mỗi yêu cầu. Tuy nhiên,HTTPGiao thức này vốn dĩ không lưu trạng thái. Do đó, phiên được sử dụng để theo dõi người dùng trong suốt quá trình họ sử dụng ứng dụng web. Quản lý phiên là quá trình quản lý các phiên này và đảm bảo chúng luôn được bảo mật.

Vòng đời quản lý phiên

Cách tốt nhất để tìm hiểu về quản lý phiên là sử dụng vòng đời quản lý phiên, như được minh họa trong hình động bên dưới.

<img width="1124" height="513" alt="image" src="https://github.com/user-attachments/assets/1cbd4513-a135-4e24-b88f-777a130edad6" />

Tạo phiên

Bạn có thể nghĩ rằng bước đầu tiên trong vòng đời này chỉ xảy ra sau khi bạn cung cấp thông tin đăng nhập, chẳng hạn như tên người dùng và mật khẩu. Tuy nhiên, trên nhiều ứng dụng web, phiên làm việc ban đầu đã được tạo khi bạn truy cập ứng dụng. Điều này là do một số ứng dụng muốn theo dõi hành động của bạn ngay cả trước khi xác thực. Tuy nhiên, trọng tâm chính của buổi học này sẽ là các phiên làm việc đã được xác thực. Sau khi bạn cung cấp tên người dùng và mật khẩu, bạn sẽ nhận được một giá trị phiên (session value) được gửi kèm theo mỗi yêu cầu mới. Cách các giá trị phiên này được tạo, sử dụng và lưu trữ là rất quan trọng trong việc bảo mật quá trình tạo phiên.

Theo dõi phiên

Sau khi nhận được giá trị phiên, giá trị này sẽ được gửi kèm với mỗi yêu cầu mới. Điều này cho phép ứng dụng web theo dõi các hành động của bạn ngay cả khi...HTTPGiao thức này có bản chất không lưu trạng thái. Với mỗi yêu cầu được gửi đi, ứng dụng web có thể khôi phục giá trị phiên từ yêu cầu và thực hiện tra cứu phía máy chủ để hiểu phiên đó thuộc về ai và họ có những quyền hạn gì. Trong trường hợp có sự cố trong quá trình theo dõi phiên, điều này có thể cho phép kẻ tấn công chiếm đoạt phiên hoặc mạo danh người dùng.

Hết hạn phiên

Bởi vì HTTP Giao thức này không có trạng thái, do đó có thể xảy ra trường hợp người dùng ứng dụng web đột ngột ngừng sử dụng. Ví dụ, bạn có thể đóng tab hoặc toàn bộ trình duyệt. Vì giao thức không có trạng thái, ứng dụng web không có phương thức nào để biết hành động này đã xảy ra. Đây là lúc thời hạn phiên (session expiration) phát huy tác dụng. Giá trị phiên của bạn cần có thời gian tồn tại. Nếu thời gian tồn tại hết hạn và bạn gửi giá trị phiên cũ đến ứng dụng web, yêu cầu sẽ bị từ chối vì phiên đã hết hạn. Thay vào đó, bạn sẽ được chuyển hướng đến trang đăng nhập để xác thực lại và bắt đầu lại vòng đời quản lý phiên!

Kết thúc phiên

Tuy nhiên, trong một số trường hợp, người dùng có thể buộc phải đăng xuất. Trong trường hợp này, ứng dụng web cần phải chấm dứt phiên làm việc của người dùng. Mặc dù điều này tương tự như việc hết hạn phiên, nhưng nó khác biệt ở chỗ ngay cả khi thời gian tồn tại của phiên vẫn còn hiệu lực, bản thân phiên làm việc cũng cần phải bị chấm dứt. Các vấn đề trong quá trình chấm dứt này có thể cho phép kẻ tấn công giành được quyền truy cập lâu dài vào tài khoản.

Để hiểu rõ các lỗ hổng thường gặp trong quản lý phiên, trước tiên chúng ta cần xem xét xác thực và ủy quyền. Mặc dù nghe có vẻ giống nhau và thường bị nhầm lẫn, nhưng mỗi yếu tố đều đóng một vai trò quan trọng và riêng biệt trong quản lý phiên. Để giải thích rõ hơn sự khác biệt, hãy cùng xem xét...IAAA người mẫu:

<img width="1141" height="212" alt="image" src="https://github.com/user-attachments/assets/6ec963cb-5788-47a2-8878-4789b8834819" />

Nhận dạng

Xác thực danh tính là quá trình xác minh người dùng. Quá trình này bắt đầu bằng việc người dùng xác nhận mình là một người dùng cụ thể. Trong hầu hết các ứng dụng web, việc này được thực hiện bằng cách nhập tên người dùng của bạn. Bạn đang xác nhận rằng bạn là người được liên kết với tên người dùng cụ thể đó. Một số ứng dụng sử dụng tên người dùng được tạo riêng, trong khi những ứng dụng khác sẽ sử dụng địa chỉ email của bạn làm tên người dùng.

Xác thực

Xác thực là quá trình đảm bảo người dùng đúng là người mà họ tự xưng. Trong khi xác định danh tính, bạn cung cấp tên người dùng, thì đối với xác thực, bạn cung cấp bằng chứng chứng minh bạn chính là người mà bạn nói. Ví dụ, bạn có thể cung cấp mật khẩu liên kết với tên người dùng đã khai báo. Ứng dụng web có thể xác nhận thông tin này nếu nó hợp lệ; đây là lúc quá trình tạo phiên bắt đầu.

Ủy quyền

Ủy quyền là quá trình đảm bảo người dùng cụ thể có các quyền cần thiết để thực hiện hành động được yêu cầu. Ví dụ, trong khi tất cả người dùng có thể xem dữ liệu, chỉ một số ít người được chọn mới có thể chỉnh sửa dữ liệu đó. Trong vòng đời quản lý phiên, theo dõi phiên đóng vai trò quan trọng trong việc ủy ​​quyền.

Trách nhiệm giải trình

Trách nhiệm giải trình là quá trình tạo ra bản ghi về các hành động do người dùng thực hiện. Chúng ta cần theo dõi phiên hoạt động của người dùng và ghi lại tất cả các hành động được thực hiện trong phiên cụ thể đó. Thông tin này đóng vai trò quan trọng trong trường hợp xảy ra sự cố bảo mật để làm rõ những gì đã xảy ra.

IAAA và Quản lý phiên

Giờ bạn đã hiểu sự khác biệt giữa xác thực và ủy quyền, hãy quay lại với quản lý phiên. Xác thực đóng vai trò trong việc tạo ra các phiên. Ủy quyền trở nên quan trọng để xác minh rằng người dùng được liên kết với một phiên cụ thể có quyền thực hiện hành động mà họ yêu cầu. Trách nhiệm giải trình rất quan trọng để chúng ta có thể ghép nối lại những gì thực sự đã xảy ra trong một sự cố, điều đó có nghĩa là việc ghi nhật ký các yêu cầu và phiên được liên kết với mỗi yêu cầu cũng rất quan trọng.

Trước khi đi sâu vào vấn đề bảo mật quản lý phiên, chủ đề cuối cùng cần đề cập là loại phiên được sử dụng. Hai phương pháp chính là cookie và token, mỗi loại đều có những ưu điểm và nhược điểm riêng.

Quản lý phiên dựa trên cookie

Quản lý phiên dựa trên cookie thường được gọi là phương pháp quản lý phiên truyền thống. Khi ứng dụng web muốn bắt đầu theo dõi, trong phản hồi, giá trị tiêu đề Set-Cookie sẽ được gửi đi. Trình duyệt của bạn sẽ diễn giải tiêu đề này để lưu trữ một giá trị cookie mới. Hãy cùng xem xét một tiêu đề Set-Cookie như vậy:

Set-Cookie: session=12345;

Trình duyệt của bạn sẽ tạo một mục nhập cookie `session` với tên và giá trị `12345` hợp lệ cho miền mà cookie được nhận từ đó. Một số thuộc tính cũng có thể được thêm vào tiêu đề này. Nếu bạn muốn tìm hiểu thêm về tất cả chúng, vui lòng tham khảo tại đây. Nhưng một số trong những cái đáng chú ý là:
```
Bảo mật - Cho trình duyệt biết rằng cookie chỉ có thể được truyền qua các kênh HTTPS đã được xác minh. Nếu có lỗi chứng chỉ hoặc sử dụng HTTP, giá trị cookie sẽ không được truyền đi.
HTTPOnly - Cho trình duyệt biết rằng giá trị của cookie không được phép đọc bởi JavaScript phía máy khách.
Hết hạn - Thông báo cho trình duyệt khi nào giá trị cookie sẽ không còn hợp lệ và cần được xóa.
SameSite - Cho trình duyệt biết liệu cookie có thể được truyền trong các yêu cầu liên trang web hay không để giúp bảo vệ chống lại các cuộc tấn công CSRF.
```
Một điều quan trọng cần nhớ với xác thực dựa trên cookie là chính trình duyệt sẽ quyết định khi nào một giá trị cookie cụ thể sẽ được gửi kèm theo yêu cầu. Sau khi xem xét tên miền và các thuộc tính của cookie, trình duyệt sẽ đưa ra quyết định này và cookie được đính kèm tự động mà không cần bất kỳ mã JavaScript bổ sung nào ở phía máy khách.

Quản lý phiên dựa trên mã thông báo

Quản lý phiên dựa trên token là một khái niệm tương đối mới. Thay vì sử dụng các tính năng quản lý cookie tự động của trình duyệt, nó dựa vào mã phía máy khách để thực hiện quy trình. Sau khi xác thực, ứng dụng web cung cấp một token trong phần thân yêu cầu. Sử dụng mã JavaScript phía máy khách, token này sau đó được lưu trữ trong LocalStorage của trình duyệt.

Khi có yêu cầu mới được gửi, mã JavaScript phải tải mã thông báo từ bộ nhớ và đính kèm nó vào phần tiêu đề. Một trong những loại mã thông báo phổ biến nhất là JSON Web Tokens (JWT), được truyền qua phần Authorization: Bearertiêu đề. Tuy nhiên, vì chúng ta không sử dụng các tính năng quản lý cookie tích hợp sẵn của trình duyệt, nên mọi thứ đều có thể xảy ra. Mặc dù có các tiêu chuẩn, nhưng không có gì thực sự bắt buộc bất cứ điều gì không tuân theo các tiêu chuẩn này.

Lợi ích và nhược điểm

Ưu điểm và nhược điểm của mỗi phương pháp này có mối liên hệ trực tiếp với nhau, vì vậy chúng ta hãy cùng xem xét:

Quản lý phiên cookie
Quản lý phiên dựa trên mã thông báo
Cookie được trình duyệt tự động gửi kèm theo mỗi yêu cầu.
Mã token phải được gửi dưới dạng tiêu đề kèm theo mỗi yêu cầu bằng JavaScript phía máy khách.
Các thuộc tính cookie có thể được sử dụng để tăng cường khả năng bảo vệ cookie của trình duyệt.
Các token không có cơ chế bảo mật tự động và do đó cần được bảo vệ khỏi việc tiết lộ thông tin.
Cookie có thể dễ bị tấn công bằng các phương thức tấn công thông thường phía máy khách, chẳng hạn như...CSRF, trong đó trình duyệt bị đánh lừa để thực hiện yêu cầu thay mặt người dùng.
Vì mã thông báo không tự động được thêm vào bất kỳ yêu cầu nào và không thể được đọc từ LocalStorage bởi các miền khác, nên các cuộc tấn công phía máy khách thông thường như...CSRFbị chặn.
Vì cookie chỉ hoạt động trên một miền cụ thể, nên việc sử dụng chúng một cách an toàn trong các ứng dụng web phi tập trung có thể gặp khó khăn.
Token hoạt động tốt trong các ứng dụng web phi tập trung, vì chúng được quản lý thông qua JavaScript và thường có thể chứa tất cả thông tin cần thiết để xác minh chính token đó.

Cuối cùng cũng đến lúc tìm hiểu về bảo mật quản lý phiên. Quay trở lại với vòng đời quản lý phiên, hãy cùng xem xét những sự cố có thể xảy ra ở mỗi giai đoạn.

Tạo phiên

Quá trình tạo phiên là nơi dễ phát sinh nhiều lỗ hổng bảo mật nhất. Hãy cùng tìm hiểu một vài lỗ hổng phổ biến.

Giá trị phiên yếu

Ngày nay, việc thấy các giá trị phiên yếu ít phổ biến hơn do các khung phân tích được sử dụng nhất quán. Tuy nhiên, với sự gia tăng của các mô hình LLM và các mô hình khác,Trí tuệ nhân tạoVới các giải pháp hỗ trợ mã, bạn sẽ ngạc nhiên khi thấy những lỗ hổng bảo mật kiểu cũ này lại thường xuyên xuất hiện trở lại.

Nếu một cơ chế tạo phiên tùy chỉnh đã được triển khai, rất có thể các giá trị phiên có thể bị đoán được. Một ví dụ điển hình là cơ chế mã hóa tên người dùng bằng base64 thành giá trị phiên. Nếu kẻ tấn công có thể phân tích ngược quy trình tạo phiên, chúng có thể tạo ra hoặc đoán được các giá trị phiên để chiếm đoạt tài khoản của người dùng hợp pháp.

Giá trị phiên có thể điều khiển

Trong một số loại token, chẳng hạn như JWT, tất cả thông tin cần thiết để tạo và xác minh tính hợp lệ của JWT đều được cung cấp. Nếu các biện pháp bảo mật không được thực thi, chẳng hạn như xác minh chữ ký của token hoặc đảm bảo rằng chính chữ ký đó được tạo ra một cách an toàn, thì kẻ tấn công có thể tạo ra token của riêng chúng. Các loại tấn công này sẽ được thảo luận chi tiết hơn trong một buổi học khác.

Sự cố định phiên

Bạn còn nhớ ứng dụng web đã cấp cho bạn một phiên làm việc trước khi xác thực không? Những ứng dụng web này có thể dễ bị tấn công bởi kiểu gọi là chiếm đoạt phiên (session fixation). Nếu giá trị phiên của bạn không được thay đổi đúng cách sau khi xác thực, một kẻ tấn công có vị trí thích hợp có thể ghi lại phiên đó khi bạn vẫn chưa được xác thực và chờ bạn xác thực để truy cập vào phiên của bạn.

Truyền phiên không an toàn

Trong môi trường hiện đại, việc máy chủ xác thực và máy chủ ứng dụng được tách biệt là điều phổ biến. Hãy nghĩ đến những thứ như Đăng nhập một lần (Single Sign-On)SSO(Giải pháp) Một ứng dụng được sử dụng để xác thực cho nhiều ứng dụng web khác. Để quá trình này hoạt động, dữ liệu phiên của bạn phải được chuyển từ máy chủ xác thực đến máy chủ ứng dụng thông qua trình duyệt của bạn. Tuy nhiên, trong quá trình truyền tải này, một số vấn đề có thể phát sinh, làm lộ thông tin phiên của bạn cho kẻ tấn công. Phổ biến nhất là chuyển hướng không an toàn, trong đó kẻ tấn công có thể kiểm soát URL mà bạn sẽ được chuyển hướng đến sau khi xác thực. Điều này có thể cho phép kẻ tấn công chiếm đoạt phiên của bạn. Điều này không chỉ xảy ra với các triển khai tùy chỉnh, mà còn với các giải pháp của Oracle.SSOGiải pháp đó có một lỗi nghiêm trọng cho phép điều này xảy ra.(mở trong tab mới).

Theo dõi phiên

Theo dõi phiên là nguyên nhân gây ra nhiều lỗ hổng bảo mật thứ hai. Hãy cùng xem xét.

Bỏ qua xác thực

Việc bỏ qua xác thực xảy ra khi không có đủ các bước kiểm tra được thực hiện để xác định xem người dùng có được phép thực hiện hành động mà họ yêu cầu hay không. Về bản chất, điều này dẫn đến việc không theo dõi chính xác phiên làm việc của người dùng và các quyền liên quan. Cũng cần phải nói thêm về hai loại bỏ qua xác thực:

Bỏ qua theo chiều dọc - Bạn có thể thực hiện một thao tác chỉ dành cho người dùng có quyền cao hơn.
Bỏ qua theo chiều ngang - Bạn có thể thực hiện một hành động mà bạn được phép thực hiện, nhưng trên một tập dữ liệu mà bạn không được phép thực hiện hành động đó.
Trong hầu hết các ứng dụng, việc phòng chống các cuộc tấn công vượt quyền truy cập theo chiều dọc khá dễ dàng nhờ sử dụng các hàm trang trí và cấu hình kiểm soát truy cập dựa trên đường dẫn. Tuy nhiên, với các cuộc tấn công vượt quyền truy cập theo chiều ngang, người dùng đang thực hiện một hành động mà họ được phép thực hiện. Vấn đề là họ đang thực hiện hành động đó trên dữ liệu của người khác. Để khắc phục điều này, cần có mã thực tế để xác minh người dùng là ai (được trích xuất từ ​​phiên làm việc của họ), dữ liệu nào họ đang yêu cầu và liệu họ có được phép yêu cầu hoặc sửa đổi tập dữ liệu đó hay không.

Ghi nhật ký không đầy đủ

Một vấn đề then chốt trong các sự cố là thiếu thông tin đầy đủ để ghép nối các mảnh ghép của cuộc tấn công. Mặc dù phần lớn nhật ký sẽ được ghi lại ở cấp độ cơ sở hạ tầng, nhưng việc ghi nhật ký ứng dụng có thể rất quan trọng để hiểu điều gì đã xảy ra. Trong trường hợp không có thông tin về các hành động được thực hiện bởi một phiên cụ thể và khả năng truy vết phiên đó đến người dùng, điều này có thể tạo ra những lỗ hổng trong quá trình điều tra mà không thể lấp đầy. Điều quan trọng nữa là phải đảm bảo nhật ký bao gồm cả các hành động được chấp nhận và bị từ chối. Trong trường hợp tấn công chiếm đoạt phiên, các hành động sẽ có vẻ hợp lệ. Do đó, chỉ ghi nhật ký các hành động bị từ chối là không đủ để làm rõ toàn bộ sự việc.

Hết hạn phiên

Việc hết hạn phiên chỉ có một lỗ hổng duy nhất, đó là khi thời gian hết hạn của phiên quá dài. Một phiên nên được xem như một vé xem phim. Mỗi đêm, cùng một bộ phim được chiếu, nhưng chúng ta không muốn ai đó có thể sử dụng cùng một vé để xem phim lần nữa. Điều tương tự cũng áp dụng cho các phiên, chúng ta cần đảm bảo rằng thời gian hết hạn của phiên phải tính đến trường hợp sử dụng cụ thể của ứng dụng. Một ứng dụng ngân hàng nên có thời gian tồn tại phiên ngắn hơn so với trình duyệt webmail của bạn.

Hơn nữa, đối với các phiên hoạt động kéo dài, chẳng hạn như phiên của trình duyệt webmail, bản thân phiên đó cần phải xác nhận vị trí sử dụng. Nếu vị trí này thay đổi (điều này có thể là dấu hiệu của việc chiếm đoạt phiên), phiên đó cần phải bị chấm dứt.

Kết thúc phiên

Đối với việc chấm dứt phiên, vấn đề chính là khi các phiên không được chấm dứt đúng cách ở phía máy chủ khi thực hiện thao tác đăng xuất. Giả sử kẻ tấn công chiếm đoạt phiên của người dùng. Trong trường hợp đó, ngay cả khi người dùng nhận thức được vấn đề, nếu không có khả năng vô hiệu hóa phiên ở phía máy chủ, người dùng không có phương pháp nào để loại bỏ quyền truy cập của kẻ tấn công. Tuy nhiên, điều này có thể là một vấn đề khá nghiêm trọng đối với các token mà thời hạn sử dụng được nhúng ngay trong token đó. Trong những trường hợp này, token có thể được thêm vào danh sách chặn để xác minh. Một số ứng dụng cũng tiến xa hơn bằng cách cho phép xem và chấm dứt tất cả các phiên của người dùng. Hơn nữa, sau khi đặt lại mật khẩu thành công, cũng nên chấm dứt tất cả các phiên để cho phép người dùng lấy lại toàn quyền kiểm soát tài khoản của họ.
