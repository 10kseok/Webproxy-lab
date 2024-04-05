# TCP Server (/echo server)
TCP 소켓을 통해 echo client가 메세지를 전달하면 echo server 전달받은 내용을 client에게 그대로 전달한다.

# Web Server (/tiny)
tiny 서버는 HTTP 요청을 받으면, 요청에 맞는 HTTP 응답을 전송한다.
일반적인 uri(__/home.html__)의 경우에는 정적 웹서버로 동작하며,
cgi-bin인 붙은 uri(__/cgi-bin/adder?{num1}&{num2}__)에서는 실행 파일을 처리하여 동적 웹서버로 동작한다.

정적 파일인 경우 html, gif, png, jpg, mp4 형식을 제외한 파일들은 text/plain으로 다뤄진다.
현재 adder라는 실행 파일만을 제공하고 있으며, 이 파일은 파라미터로 두 개의 수를 더한 값을 계산하여 HTTP 응답 결과를 생성한다.

# Proxy Server (proxy.*)
tiny 서버로 들어가기 전에 들리는 proxy 서버로, 필수 헤더들을 확인하고 누락된 헤더를 추가하여 tiny 서버로 HTTP 요청을 보낸다.
tiny 서버로부터 받은 응답을 클라이언트에게 그대로 응답하고 있다.