# Dorks List
 1. inurl:nokia not for distribution | confidential | “employee only” | proprietary | top secret | classified | trade secret | internal | private filetype:pdf
 2. inurl:.gov not for distribution | confidential | “employee only” | proprietary | top secret | classified | trade secret | internal | private | WS_FTP | ws_ftp | log | LOG filetype:log
 3. inurl:.gov not for distribution | confidential | “employee only” | proprietary | top secret | classified | trade secret | internal | private filetype:xls
 4. inurl:.gov not for distribution | confidential | “employee only” | proprietary | top secret | classified | trade secret | internal | private filetype:csv
 5. inurl:.gov not for distribution | confidential | “employee only” | proprietary | top secret | classified | trade secret | internal | private filetype:doc
 6. inurl:.gov not for distribution | confidential | “employee only” | proprietary | top secret | classified | trade secret | internal | private filetype:txt
 7. index of / site: /etc/certs + “index of /” */* site:example.com
 8. index of /.git site:example.com
 9. inurl:/proc/self/cwd
 10. filetype:log username putty
 11. filetype:xls inurl:"email.xls"
 
 # Top google Dorking
 1. publicly exposed documents :- site:http://target.com ext:doc | ext:docx | ext:odt | ext:rtf | ext:sxw | ext:psw | ext:ppt | ext:pptx | ext:pps | ext:csv
 2. Directory listing bug :- site:http://target.com intitle:index.of
 3. Configuration files :- site:http://target.com ext:xml | ext:conf | ext:cnf | ext:reg | ext:inf | ext:rdp | ext:cfg | ext:txt | ext:ora | ext:ini | ext:env
 4. database file exposed :- site:http://target.com ext:sql | ext:dbf | ext:mdb
 5. Log files exposed :- site:http://target.com ext:log
 6. Backup and old files :- site:http://target.com ext:bkf | ext:bkp | ext:bak | ext:old | ext:backup
 7. login page of admin pannel :- site:http://target.com inurl:login | inurl:signin | intitle:Login | intitle:"sign in" | inurl:auth
 8. php errors/warning :- site:http://target.com "PHP Parse error" | "PHP Warning" | "PHP Error"
 9. sql error :- site:site.com1 intext:"sql syntax near" | intext:"syntax error has occurred" | intext:"incorrect syntax near" | intext:"unexpected end of SQL command" | intext:"Warning: mysql_connect()" | intext:"Warning: mysql_query()" | intext:"Warning: pg_connect()"
 10. signup page :- site:http://target.com inurl:signup | inurl:register | intitle:Signup


https://pentest-tools.com/information-gathering/google-hacking

# Content Discovery
Wordlist for fuzzing 
- https://github.com/AlbusSec/Penetration-List/tree/main/Information%20Disclosure%20-01/Sensitive-Directory-list

# Github Dorking

https://shahjerry33.medium.com/github-recon-its-really-deep-6553d6dfbb1f


# Wordpress juciy endpoints

- wp-admin.php  
- wp-config.php
- wp-content/uploads
- Wp-load
- wp-signup.php
- Wp-json
- wp-includes [directory]
- index.php
- wp-login.php
- wp-links-opml.php
- wp-activate.php
- wp-blog-header.php
- wp-cron.php
- wp-links.php
- wp-mail.php
- xmlrpc.php
- wp-settings.php
- wp-trackback.php
- wp-signup.php
- /_wpeprivate/config.json




