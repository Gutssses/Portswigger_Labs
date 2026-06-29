
#### Reference: [Information disclosure in error messages](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-in-error-messages)

##### Analysis:

we need to see what third party service is running on server.

Using burp you can see all request response.

You can change the productId, with this how about we give unexpected input which will give us error.

##### Steps:

1. Explore application.

2. Go to Burp and send /product?productId=15 to Repeater.

3. change 15 to example.

4. you wil get error.

5. Now see cre fully you will see there is third party software. called: Apache Struts 2 2.3.31

6. Submit version value.

There you go !!!

---
#### Reference: [Information disclosure on debug page](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-on-debug-page)

##### Anlaysis: 
SECRET_KEY is hidden somewhere in debug page.

you can start with source view of homepage.

##### Steps:

1. Explore application.

2. Inspect source view of homepage.

3. There you will link which call debug: `/cgi-bin/phpinfo.php`  

4. you will send request to Repeater and send that request to server.

5. Inside response you will secrh term: SECRET_KEY.

6. copy the key and submit in the solution.

There you go !!!

---
#### Reference: [Source code disclosure via backup files](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-via-backup-files)

##### Analysis:

you need to find hidden directory.

you can try robots.txt  or view source code.

##### Steps:

1. Browse to /robots.txt.

2. you will find it says: Disallow /backup.

3. Now browse to /backup you will find ProductTemplate.java.bak.

4. Now Browse to /backup/ProductTemplate.java.bak there you will find hard-coded password.

5. Submit that password.

There you go !!!

---
#### Reference: [Authentication bypass via information disclosure](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-authentication-bypass)

##### Analysis:

When you find some juicy page, you can try to change the request method to TRACE.

TRACE-  it give back request message back with response, but sometimes it will give back addtion information.

Like:  `X-Custom-IP-Authorization: 1.187.164.6` 

##### Steps:

1. You can find /admin panel.

2. Go to burp and modify GET /admin to TRACE /admin.

3. Notice that you got an header inside response header.

4. Go to Burp > Proxy > Match and Replace. 

5. Inside HTTP match and replace rule. click on add.

6. Leave everything as it is, just fill the Replace fiel with the header you got.

7. Click on test. Under Auto-modifed request you will see it is adding header.

8. Click on Ok.

9. Now go to /admin panel and delet carlos.

There you go !!!

---
#### Reference: [Information disclosure in version control history](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-in-version-control-history)

##### Analysis:

When you get .git in the website you will find someinformation realted to site.

##### Steps:

1. Go to /.git in url.

2. copy url and go to terminal and run : `wget -r lab/.git`

3. run git log, and you will se all previous log.

4. You will notice that file is modified in last commit.

5. You can run git command what is modified
	1. git diff 2423k2 32jkl23 or git log -p
	2. You will get what changes have been made

6. You will get the admin password using this login as amin and delet carlos.

There you go !!!

---

					`Complited Lab`



