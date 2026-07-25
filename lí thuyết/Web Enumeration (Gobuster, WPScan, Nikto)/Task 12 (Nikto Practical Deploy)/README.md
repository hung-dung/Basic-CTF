```
┌──(kali㉿kali)-[~]
└─$ rustscan -a 10.114.176.58             
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Real hackers hack time ⌛

[~] The config file is expected to be at "/home/kali/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.114.176.58:22
Open 10.114.176.58:80
Open 10.114.176.58:1090
Open 10.114.176.58:1091
Open 10.114.176.58:1099
Open 10.114.176.58:1098
Open 10.114.176.58:3873
Open 10.114.176.58:4446
Open 10.114.176.58:4713
Open 10.114.176.58:4712
Open 10.114.176.58:5445
Open 10.114.176.58:5455
Open 10.114.176.58:5500
Open 10.114.176.58:5501
Open 10.114.176.58:8009
Open 10.114.176.58:8080
Open 10.114.176.58:8083
```

```
┌──(kali㉿kali)-[~]
└─$ nikto -h 10.114.176.58 -p 80
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          10.114.176.58
+ Target Hostname:    10.114.176.58
+ Target Port:        80
+ Start Time:         2026-07-25 04:39:05 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.4.7 (Ubuntu)
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
```

```
┌──(kali㉿kali)-[~]
└─$ nikto -h 10.114.176.58 -p 8080
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          10.114.176.58
+ Target Hostname:    10.114.176.58
+ Target Port:        8080
+ Start Time:         2026-07-25 04:49:07 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache-Coyote/1.1
+ /: Retrieved x-powered-by header: Servlet/3.0; JBossAS-6.
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ /favicon.ico: identifies this app/server as: JBoss Server. See: https://en.wikipedia.org/wiki/Favicon
+ OPTIONS: Allowed HTTP Methods: GET, HEAD, POST, PUT, DELETE, TRACE, OPTIONS .
+ HTTP method ('Allow' Header): 'PUT' method could allow clients to save files on the web server.
+ HTTP method ('Allow' Header): 'DELETE' may allow clients to remove files on the web server.
+ /admin-console/config.php: Cookie JSESSIONID created without the httponly flag. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies
- STATUS: Completed 1500 requests (~22% complete, 28.5 minutes left): currently in plugin 'Nikto Tests'
- STATUS: Running average: Not enough data.
```
