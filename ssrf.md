####  Reference: [Basic SSRF against the local server](https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-localhost)
##### Steps:
In SSRF we send requset message to server which make request to other sever and get detail.
Here we need to get info of /admin functionality and by this we need to delet carlos.

1. In site you can check the stock of product.

2. Now when you see the request site make to check the stock.

3. Site send another reuqest to server which give back the status of stock.

4. Now we use this to get info.

5. In request message of stock checking change `stockApi=stockIdurl` to `stockApi=http//localhost/admin`.

6. This will show you the html page of admin but you can't perform the changes.

7. So you need to see that when you delet carlos it send another request to `delet?user=carlos`.

8. but ths not work because we are not authorized user, so we send another reuqest this time we replace `stocApi=localhost/admin` to `stockApi=http//localhost/admin/delet?user=carlos`.

9. This reuqest give back result as carlos get deleted.

There you go !!!

 ---
#### Reference: [Basic SSRF against another back-end system](https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-backend-system)
#### Steps:

1. You look for An SSRF Vuln by inspecting every request.

2. When you see stock it's request message has stockApi=http..

3. This means you can past another url.

4. But you can't access info of /admin by changing url, you need IP of internal server.

5. We scan the internal server 192.168.0.x

6. By using Burp Intruder we can find /admin panel in internal server.
	1. send request message to Intruder.
	2. change url of stockApi to `http:/192.168.0.1:8080/admin` .
	3. Change 1 from 1 to 255 and check 200 status code.

7. After finding admin panel check what application send request message when you delet carlos.

8. And replace that request in stockApi path.

There you go !!!
