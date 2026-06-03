# Vertical privilege escalation 
### Vertical privilege escalation

If a user can gain access to functionality that they are not permitted to access then this is vertical privilege escalation. For example, if a non-administrative user can gain access to an admin page where they can delete user accounts, then this is vertical privilege escalation.


#### Reference: [Unprotected admin functionality](https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality)

##### Steps:
In this lab i need to find admin page and i need to delet carlos.

1. I visited the website and view the page source code and tried to find any link related to admin page, Not found any.
   
2. Then i tried `/admin`, which showes not found.
   
3. the tried to looked for `/robots.txt` file and found `/administrator-panel`.
   
4. Deleted the carlos.

There you go !!!

---

#### Reference: [Unprotected admin functionality with unpredictable URL](https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality-with-unpredictable-url)

##### Steps:

1. As i opend the application i looked into page source and i find javascript in whch Admin functionality is there.
```
<script>
var isAdmin = false;
if (isAdmin) {
   var topLinksTag = document.getElementsByClassName("top-links")[0];
   var adminPanelTag = document.createElement('a');
   adminPanelTag.setAttribute('href', '/admin-ump7rt');
   adminPanelTag.innerText = 'Admin panel';
   topLinksTag.append(adminPanelTag);
   var pTag = document.createElement('p');
   pTag.innerText = '|';
   topLinksTag.appendChild(pTag);
}
</script>
```

2. Here is the path: `/admin-ump7rt` of admin.

3. Delet the carlos.

There you go !!!

---
#### Reference: [User role controlled by request parameter](https://portswigger.net/web-security/access-control/lab-user-role-controlled-by-request-parameter)

##### Steps:

1. I check page source code nothing was there.

2. check for `/admin` it was there but restricted.

3. loged-in by `wiener:peter`.

4. tried to change url parameter by id=wiener to id=admin, Not worked.

5. looked into site map using burpsutie and check every reuqest message.

6. In `/my-account?id=wiener` there is parameter Admin=false.

7. Change the parameter but response message has nothing.

8. So check in tools section in firefox and then set Admin=true in Storage/cookies Section.

9. Admin panel option emerged.

10. Deleted the carlos.

There you go !!!

---
#### Reference: [User role can be modified in user profile](https://portswigger.net/web-security/access-control/lab-user-role-can-be-modified-in-user-profile)

##### Steps:

1. There is `/admin` panel but not access by normal user, user with roleid of 2 can access 

2. try to change `/my-account?id=wiener` to `/my-account?id=roleid`, but not worked

3. changed the email from wiener to roleid and anylise the response message

4. Body of resonpse message have parameter, roleid:1

5. now modified the requestmessage with roleid:2

6. Admin panel is appeard

7. Delet carlos

There you go !!!

---
---

# Horizontal privilege escalation

#### Reference:[User ID controlled by request parameter](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter)

##### Steps:

1. login as `wiener:peter`.

2. replace wiener to carlos.

3. you  will get Carlos API Key.

There you go !!!

---
#### Reference: [User ID controlled by request parameter, with unpredictable user IDs](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-unpredictable-user-ids)

##### Steps:


1. log in as `wiener:peter`.

2. Now you will notice that the id=81115wers154we8 (GUIDs).

3. You can't guess carlos id.

4. see the blog author there is blog published by carlos.

5. open the blog and when you view the page source you will notice that carlos id is there.

6. replace your id with carlos id in url.

7. you got carlos API.

There you go !!!

---
#### Reference: [User ID controlled by request parameter with data leakage in redirect](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-data-leakage-in-redirect)

##### Steps:

1. You log in as `wiener:peter`.

2. You change wiener to carlos in url but you got redirected to login page.

3. But when you anaylst response message you will find out that carlos API is there.

There you go !!!

---
---

# Horizontal to vertical privilege escalation

#### Reference: [User ID controlled by request parameter with password disclosure](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-password-disclosure)

##### Steps:

1. Log in as `wiener:peter`.

2. As you can see, in the website when you log in there is your current password.

3. Now try to change user by changing wiener to carlos, It worked.

4. Now try admin, administrator-panel, administrator.

5. Administrator work, and you log in as Admin and you delet the carlos.

There you go !!!

---
---
# Insecure direct object references

#### Reference: [Insecure direct object references](https://portswigger.net/web-security/access-control/lab-insecure-direct-object-references)

##### Steps:

1. You log in as `wiener:peter`.

2. You see there is another option as live chat and you can downlaod your chat .

3. When you first downlaod you notice the naming is 2.txt, and it's starting from 2.

4. So i tried from homepage(.web-security-academy.net): homepage/1.txt, homepage/2.txt, homepage/carlos.txt.

5. Also homepage/robots.txt, and many more but didnot work.

6. So i tried looked in burp and show request message of transcript download and notice path for downloading transcript, which is: `/download-transcript/2.txt`.

7. I tried homepage/download-trasncript/1.txt.

8. And found password of carlos.

There you go !!!

