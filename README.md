# TCP Server (/echo server)
TCP 소켓을 통해 echo client가 메세지를 전달하면 echo server 전달받은 내용을 client에게 그대로 전달한다.

## client
<img width="1171" height="68" src="/images/echo-client.png">

## server
<img width="1075" height="68" src="/images/echo-server.png">

# Web Server (/tiny)
tiny 서버는 HTTP 요청을 받으면, 요청에 맞는 HTTP 응답을 전송한다.
일반적인 uri(__/home.html__)의 경우에는 정적 웹서버로 동작하며,
cgi-bin인 붙은 uri(__/cgi-bin/adder?{num1}&{num2}__)에서는 실행 파일을 처리하여 동적 웹서버로 동작한다.

정적 파일인 경우 html, gif, png, jpg, mp4 형식을 제외한 파일들은 text/plain으로 다뤄진다.
현재 adder라는 실행 파일만을 제공하고 있으며, 이 파일은 파라미터로 두 개의 수를 더한 값을 계산하여 HTTP 응답 결과를 생성한다.

## HTTP 요청 및 응답
### Static
```shell
curl -v localhost:8080
```
```shell
* Rebuilt URL to: localhost:8080/
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 8080 (#0)
> GET / HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.58.0
> Accept: */*
> 
* HTTP 1.0, assume close after body
< HTTP/1.0 200 OK
< Server: Tiny Web Server
< Connection: close
< Content-length: 603
< Content-type: text/html
< Your HTTP Version is: HTTP/1.1
< 
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Home</title>
</head>
<body>
    <div style="text-align: center; justify-content: center">
        <p>
            <img align="middle" src="godzilla.gif">
            Dave O'Hallaron
        </p> 
        <p>
            <video width="320" height="600" controls>
                <source src="super_cute_nephew.mp4" type="video/mp4">
            </video>
            <button onclick="location.href='/adder.html'">Adder로 이동</button>
        </p>
    </div>
</body>
</html>
* Closing connection 0
```
### Dynamic
```shell
curl -v 'localhost:8080/cgi-bin/adder?1&2'
```
```shell
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 8080 (#0)
> GET /cgi-bin/adder?1&2 HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.58.0
> Accept: */*
> 
* HTTP 1.0, assume close after body
< HTTP/1.0 200 OK
< Server: Tiny Web Server
< Your HTTP Version is: HTTP/1.1
< Connection: close
< Content-length: 123
< Content-type: text/html
< 
<h1>Welcome to add.com: The Internet addition portal.</h1>
<p>The answer is: 1 + 2 = 3</p>
<h3>Thanks for visiting!</h3>
* Closing connection 0
```

# Proxy Server (proxy.*)
tiny 서버로 들어가기 전에 들리는 proxy 서버로, 필수 헤더들을 확인하고 누락된 헤더를 추가하여 tiny 서버로 HTTP 요청을 보낸다.
tiny 서버로부터 받은 응답을 클라이언트에게 그대로 응답하고 있다.  

## 채점 결과(driver.sh)
<img width="710" height="645" src="/images/adjust-proxy.png">
