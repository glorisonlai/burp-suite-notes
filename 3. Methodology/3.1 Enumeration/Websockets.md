# Websockets
**Basically the same as a normal request, except the handshake (headers) are sent at the start**
## Instantiating Websockets
```javascript
var ws = new WebSocket("wss://<DOMAIN>") # Encrypted TLS
var ws = new WebSocket("ws://<DOMAIN>") # Unencrypted
```
### Handshake Template
#### Request
```
GET /chat HTTP/1.1
Host: normal-website.com
Sec-WebSocket-Version: 13
Sec-WebSocket-Key: wDqumtseNBJdhkihL6PW7w== # Random value - For caching, not security
Connection: keep-alive, Upgrade
Cookie: session=KOsEJNuflw4Rd9BDNrVmvwBF9rEijeE2
Upgrade: websocket
```
#### Response
```
HTTP/1.1 101 Switching Protocols
Connection: Upgrade
Upgrade: websocket
Sec-WebSocket-Accept: 0FFP+2nmNIf/h+4BP36k9uzrYGk= # Hashed Sec-WebSocket-Key
```

## Messages
```
ws.send(<MSG>); # Commonly JSON
```

## Enumeration
### Messages
**Vulnerable to the traditional techniques as XSS, XXE, OAST, etc**

### Handshake
**Vulnerable to same Header techniques, such as OAST, Host Header, CORS, SSRF, etc**
#### Specific Headers
**Generally probing for interesting headers**
- `X-Forwarded-For: <IP>`
- `Sec-WebSocket-Key: <PREDICTABLE VALUE>` -> Session takeover
- General authentication mechanism