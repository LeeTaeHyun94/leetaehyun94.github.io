---
layout: post
title:  "CORS Policy"
description: "Cross Origin Resource Sharing Policy"
date:   2019-02-11 21:40:00
categories: Web
comments: true
---
## 1. Background
HTTP 요청은 기본적으로 Cross-Site HTTP Request가 가능하다.
- Cross-Site HTTP Request : `<img>` 태그로 다른 도메인의 이미지 파일을 가져오거나, `<link>` 태그로 다른 도메인의 CSS를 가져오는 것
  - 그러나, `<script></script>` 태그로 둘러싸여 있는 스코프에서 생성된 Cross-Site HTTP Request는 Same Origin Policy가 적용되어 요청이 거부된다.
  - Same Origin Policy : 두 웹 페이지의 프로토콜, 포트, 호스트가 동일해야 한다는 정책
  - AJAX가 보편화되어  `<script></script>` 태그로 둘러싸여 있는 스크립트에서 생성되는 XMLHTTPRequest에 대해서도 Cross-Site HTTP Request가 가능해야 한다는 요구가 늘어나면서, W3C에서는 CORS라는 권고안이 나오게 되었다.

## 2. CORS Request
CORS Request는 두 가지 기준으로 각각 두 가지 종류로 나뉜다.
- 종류 : 브라우저가 요청 내용을 분석하여 조건에 해당하는 방식으로 서버에 요청을 보내므로 프로그래머가 목적에 맞는 방식을 고려하고 그 방식의 조건에 맞게 프로그래밍해야 한다.
  - Simple Request
    - GET, HEAD, POST 방식 중 하나를 사용해야 한다.
    - POST 방식일 경우, Content-type이 아래 세 가지 중 하나여야 한다.
      - application/x-www-form-urlencoded
      - multipart/form-data
      - text/plain
    - 커스텀 헤더 X
    - 1 Request -> 서버 -> 1 Response

    ```HTML
    GET /resources/public-data/ HTTP/1.1
    Host: bar.other
    User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.1b3pre) Gecko/20081130 Minefield/3.1b3pre
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
    Accept-Language: en-us,en;q=0.5
    Accept-Encoding: gzip,deflate
    Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
    Connection: keep-alive
    Referer: http://foo.example/examples/access-control/simpleXSInvocation.html
    Origin: http://foo.example


    HTTP/1.1 200 OK
    Date: Mon, 01 Dec 2008 00:23:53 GMT
    Server: Apache/2.0.61
    Access-Control-Allow-Origin: *
    Keep-Alive: timeout=2, max=100
    Connection: Keep-Alive
    Transfer-Encoding: chunked
    Content-Type: application/xml

    [XML Data]
    ```

  - Preflight Request
    - Simple Request에 해당하지 않는 경우는 모두 Preflight Request 방식이다.
    - GET, HEAD, POST 메서드를 제외한 나머지 메서드 (PUT, PATCH, TRACE, DELETE)
    - POST 메서드의 경우, Content-type이 아래 세 가지 외의 다른 값을 가질 때 사전 요청이 수행된다.
      - application/x-www-form-urlencoded
      - multipart/form-data
      - text/plain
    - 모든 Content-type
    - 커스텀 헤더 O
    - 한 번의 요청에 아래의 과정을 거친다.
      - 예비 요청(Preflight Request) -> 서버 -> 1 Response
      - 본 요청(Actual Request) -> 서버 -> 2 Response
    - 예비 요청과 본 요청에 대한 응답을 프로그래머가 처리하는 것은 아니다.
    - 프로그래머는 Access-Control- 계열의 Response Header를 정해줄 수 있다.
      - Access-Control-Allow-Origin : 헤더의 값으로 지정된 도메인으로부터의 요청만 서버의 리소스에 접근할 수 있게 설정한다.
        - `Access-Control-Allow-Origin: "URI" | *`
      - Access-Control-Expose-Headers : 기본적으로 브라우저에 노출되지는 않지만, 브라우저 측에서 접근할 수 있는(노출되는) 헤더를 설정한다.
        - Cache-Control
        - Content-Language
        - Content-Type
        - Expires
        - Last-Modified
        - Pragma
        - `Access-Control-Expose-Headers: Content-Length, X-My-Custom-Header, X-Another-Custom-Header` : 이런 방식으로 허용해주면 접근할 수 없었던 Content-Length 헤더 정보를 얻을 수 있다.
      - Access-Control-Allow-Methods : Preflight Request에 대한 Response Header에 사용되며, 서버의 리소스에 접근할 수 있는 HTTP Method 방식을 지정한다.
      - Access-Control-Allow-Headers : 예비 요청에 대한 Response Header에 사용되며, 본 요청에서 사용할 수 있는 HTTP Header를 지정한다.
      - Access-Control-Allow-Credentials : Request with Credential 방식이 사용될 수 있는지를 지정한다.
      - Access-Control-Max-Age : Preflight Request의 결과가 캐시에 얼마나 오랫동안 남아 있을지를 설정한다.
        - `Access-Control-Max-Age: <delta-seconds>`
      - etc...

    ```
    OPTIONS /resources/post-here/ HTTP/1.1
    Host: bar.other
    User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.1b3pre) Gecko/20081130 Minefield/3.1b3pre
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
    Accept-Language: en-us,en;q=0.5
    Accept-Encoding: gzip,deflate
    Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
    Connection: keep-alive
    Origin: http://foo.example
    Access-Control-Request-Method: POST
    Access-Control-Request-Headers: X-PINGOTHER


    HTTP/1.1 200 OK
    Date: Mon, 01 Dec 2008 01:15:39 GMT
    Server: Apache/2.0.61 (Unix)
    Access-Control-Allow-Origin: http://foo.example
    Access-Control-Allow-Methods: POST, GET, OPTIONS
    Access-Control-Allow-Headers: X-PINGOTHER
    Access-Control-Max-Age: 1728000
    Vary: Accept-Encoding
    Content-Encoding: gzip
    Content-Length: 0
    Keep-Alive: timeout=2, max=100
    Connection: Keep-Alive
    Content-Type: text/plain

    POST /resources/post-here/ HTTP/1.1
    Host: bar.other
    User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.1b3pre) Gecko/20081130 Minefield/3.1b3pre
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
    Accept-Language: en-us,en;q=0.5
    Accept-Encoding: gzip,deflate
    Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
    Connection: keep-alive
    X-PINGOTHER: pingpong
    Content-Type: text/xml; charset=UTF-8
    Referer: http://foo.example/examples/preflightInvocation.html
    Content-Length: 55
    Origin: http://foo.example
    Pragma: no-cache
    Cache-Control: no-cache

    <?xml version="1.0"?><person><name>Arun</name></person>


    HTTP/1.1 200 OK
    Date: Mon, 01 Dec 2008 01:15:40 GMT
    Server: Apache/2.0.61 (Unix)
    Access-Control-Allow-Origin: http://foo.example
    Vary: Accept-Encoding
    Content-Encoding: gzip
    Content-Length: 235
    Keep-Alive: timeout=2, max=99
    Connection: Keep-Alive
    Content-Type: text/plain

    [Some GZIP'd payload]
    ```

  - Request with Credential
    - HTTP Cookie와 HTTP Authentication 정보를 인식할 수 있게 해주는 요청

    ```javascript
    var invocation = new XMLHttpRequest();
    var url = 'http://bar.other/resources/credentialed-content/';
    function callOtherDomain(){
        if(invocation) {
            invocation.open('GET', url, true);
            invocation.withCredentials = true;
            invocation.onreadystatechange = handler;
            invocation.send();
        }
    }
    ```
    - .withCredentials로 Credential 요청 여부 지정
    - 서버 측에서 CORS 정책에 대한 설정을 할 때, Access-Control-Allow-Credentials을 true로 설정해야 하며, 허용되는 도메인은 모든 도메인을 허용하는 것이 아니라 특정 도메인만을 허용해야 한다.
    ```
    HTTP/1.1 200 OK
    Date: Mon, 01 Dec 2008 01:34:52 GMT
    Server: Apache/2.0.61 (Unix) PHP/4.4.7 mod_ssl/2.0.61 OpenSSL/0.9.7e mod_fastcgi/2.4.2 DAV/2 SVN/1.4.2
    X-Powered-By: PHP/5.2.6
    Access-Control-Allow-Origin: http://foo.example
    Access-Control-Allow-Credentials: true
    Cache-Control: no-cache
    Pragma: no-cache
    Set-Cookie: pageAccess=3; expires=Wed, 31-Dec-2008 01:34:53 GMT
    Vary: Accept-Encoding
    Content-Encoding: gzip
    Content-Length: 106
    Keep-Alive: timeout=2, max=100
    Connection: Keep-Alive
    Content-Type: text/plain
    ```

  - Request without Credential
    - CORS 요청 시, 기본 값이 `withCredentials = false`이다.
- CORS 관련 HTTP Request Headers : 클라이언트가 서버에 CORS 요청을 보낼 때 사용하는 헤더, 브라우저가 자동으로 지정한다.
  - Origin : Cross-site Request를 보내는 요청 도메인 URI를 나타내며, Access-control이 적용되는 모든 요청에 포함된다. 경로에 대한 정보는 포함하지 않는다.
  - Access-Control-Request-Method : 예비 요청을 보낼 때 포함되어 본 요청에서 어떤 HTTP Method를 사용할 지 서버에 알려준다.
  - Access-Control-Request-Headers : 예비 요청을 보낼 때 포함되어 본 요청에서 어떤 HTTP Header를 사용할 지 서버에 알려준다.

## 3. Conclusion
- CORS 정책을 적절히 활용하면, 클라이언트는 AJAX 기반 요청을 통해 Same Origin Policy의 제약을 넘어 다른 도메인의 자원을 사용할 수 있으며, 서버는 안전하게 자원을 제공할 수 있다.
- CORS 정책에 대한 오류를 없애기 위해서는 서버에서 직접적으로 따로 허용해주거나, 프록시 서버의 느낌으로 Same Origin Policy를 지키거나 CORS Policy 정책을 허용해준 자신의 서버를 이용하여 대리로 자원을 요청한 다음, 응답받는 식으로 해결해야 한다.