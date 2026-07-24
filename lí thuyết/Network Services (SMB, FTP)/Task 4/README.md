Câu hỏi 1: Cú pháp chính xác để truy cập vào thư mục chia sẻ SMB có tên "secret" với tư cách người dùng "suit" trên máy có địa chỉ IP 10.10.10.2 ở cổng mặc định là gì?

`smbclient //10.10.10.2/secret -U suit -p 445`

Câu hỏi 2 không cần trả lời, vậy nên chúng ta chuyển sang câu hỏi tiếp theo.

Câu hỏi 3: Chia sẻ này có cho phép truy cập ẩn danh không? Có/Không?

Để trả lời câu hỏi này, chúng ta cần thử đăng nhập vào thư mục chia sẻ với tư cách người dùng ẩn danh. Chúng ta thực hiện điều này bằng lệnh: `smbclient //10.10.109.231/profiles -U anonymous -p 139` Và sau đó, khi được yêu cầu nhập mật khẩu, đừng nhập gì cả. 

<img width="541" height="75" alt="image" src="https://github.com/user-attachments/assets/0522d806-af50-41fb-a852-e9a398428462" />

Câu trả lời của chúng tôi là có (Y), việc sử dụng ẩn danh thực sự được cho phép trên phần chia sẻ này.

Câu hỏi 4: Tuyệt vời! Hãy xem xung quanh xem có tài liệu nào thú vị có thể chứa thông tin giá trị không. Chúng ta có thể đoán thư mục hồ sơ này thuộc về ai?

Chúng ta có thể nhìn xung quanh với `ls`. 

<img width="621" height="278" alt="image" src="https://github.com/user-attachments/assets/e1695f53-180e-4e6b-bb6f-2b264e80596b" />

Tệp 'Working From Home Information.txt' trông có vẻ thú vị. Hãy tải nó xuống bằng... `get`. 

<img width="644" height="82" alt="image" src="https://github.com/user-attachments/assets/b0ff4ea9-e66b-4d53-ab86-70964b2e7aa9" />

Sau đó chúng ta `cat` nó trong bảng điều khiển cục bộ của chúng tôi. 

<img width="645" height="333" alt="image" src="https://github.com/user-attachments/assets/1d40b2c7-124d-4e6c-954a-bab792210653" />

Có vẻ như thư mục hồ sơ này thuộc về một người tên là 'John Cactus', và điều đó đã giải đáp thắc mắc của chúng ta. 

Câu hỏi 5: Dịch vụ nào đã được cấu hình để cho phép anh ấy làm việc tại nhà? 

<img width="644" height="152" alt="image" src="https://github.com/user-attachments/assets/516d5255-f16a-468e-a24b-256906bb4f1b" />

Thông báo mà chúng tôi tải xuống cho biết anh ấy đã được kích hoạt quyền SSH.

Câu hỏi 6: Được rồi! Bây giờ chúng ta đã biết điều này, vậy chúng ta nên tìm trong thư mục nào trên thư mục chia sẻ đó?

Nếu anh ta đã được cấp quyền truy cập SSH, chúng ta chắc chắn nên xem xét kỹ thư mục .ssh đó. 

<img width="622" height="226" alt="image" src="https://github.com/user-attachments/assets/b521c6c4-1946-4c31-ad24-880db60c465c" />

Câu 7: Thư mục này chứa các khóa xác thực cho phép người dùng tự xác thực và truy cập vào máy chủ. Khóa nào trong số này hữu ích nhất đối với chúng ta?

Điều này không dễ nhận thấy ngay, nhưng một chút tìm kiếm trên Google cho chúng ta biết tên mặc định của tệp nhận dạng ssh là `id_rsa`. 

<img width="601" height="180" alt="image" src="https://github.com/user-attachments/assets/52baae77-7008-440a-b48a-b234ff605141" />

Câu hỏi 8: Tải tập tin này về máy tính cục bộ của bạn và thay đổi quyền truy cập thành "600" bằng lệnh "chmod 600 [tệp tin]". Bây giờ, hãy sử dụng thông tin bạn đã thu thập được để tìm ra tên người dùng của tài khoản. Sau đó, sử dụng dịch vụ và khóa để đăng nhập vào máy chủ. Cờ smb.txt là gì?

Chúng ta có thể tải xuống tệp bằng `get` Để an toàn hơn, chúng ta cũng có thể tải xuống. .`pub` Cũng như tệp tin. 

<img width="649" height="127" alt="image" src="https://github.com/user-attachments/assets/f8487262-26d9-4f4d-aa49-abfc4a6448dd" />

Tại địa phương, chúng ta có thể `cat` Cả hai đều giúp chúng ta hiểu rõ chính xác những gì mình đang làm việc. 

<img width="545" height="503" alt="image" src="https://github.com/user-attachments/assets/010fb999-a3f6-4992-80e2-516293896223" />

`id_rsa` Chỉ chứa một khóa. Tuy nhiên, 

<img width="646" height="126" alt="image" src="https://github.com/user-attachments/assets/b4c76318-c0b1-4138-8448-b7aa81e82895" />

`id_rsa.pub` Cuối cùng, nó cung cấp cho chúng ta một giao diện trông giống như trang đăng nhập. 

Vậy là chúng ta đã có khóa SSH và tên người dùng. Nhưng làm thế nào để sử dụng khóa SSH? Đã đến lúc tìm hiểu. `ssh -h` (-h không phải là một cờ ssh thực sự, nhưng nó sẽ báo lỗi ngắn gọn và hữu ích không kém ^^; ) 

<img width="606" height="177" alt="image" src="https://github.com/user-attachments/assets/c7c90641-73ab-49cd-89e5-11aae1bb3eb2" />

Điều chúng ta cần là cờ -i. Lệnh của chúng ta sẽ trông giống như thế này: `ssh cactus@10.10.109.231 -i id_rsa`

<img width="559" height="403" alt="image" src="https://github.com/user-attachments/assets/ae1cb04e-8ab0-44e4-98c5-7cb6b1a3eff2" />

Và thế là, chúng ta đã vào được bên trong. Giờ thì chúng ta có thể `cat smb.txt`. 

<img width="241" height="57" alt="image" src="https://github.com/user-attachments/assets/193faaec-0807-458e-9a9d-ad6930fdfed3" />
