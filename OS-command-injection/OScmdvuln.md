Reference:  [OS command injection, simple case](https://portswigger.net/web-security/os-command-injection/lab-simple) 

### Steps

1. i check out the website and and find out the that when i check stock the request goes to the server

2. now i try to enter whoami command in the traffic, 
   
3. i used & whoami & but this does not work because i am using this `&` function at parameter value

4. So then i tried `|` example: productId=1&storeId=1|whoami.

There you go!!!

---

Reference:  [Blind OS command injection with time delays](https://portswigger.net/web-security/os-command-injection/lab-blind-time-delays) 

### Steps:

As i read in the portswigger, feedback goes to the server and then server send feed back to the administrator panel through mail -s.. way

so i put the payload afther the mail input with link encrypt.

payload: `& ping -c 10 127.0.0.1 &`

there you go!!! 
