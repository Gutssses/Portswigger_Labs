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
</html>`
   ```

5. Put this is server and click on store and  Send it to the Victim.

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
</html>`
   ```

5. Put this is server and click on store and  Send it to the Victim.

6. Make sure that you change email every time you send.

7. And check all parameter such as: action:`victim email change path`, email change,  method.

There you go !!!

---


