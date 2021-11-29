# Host Header
*Exploit -> [Host Header Attacks](3.%20Methodology/3.2%20Exploitation/Host%20Header%20Attacks.md)*
**If sending a malformed Host returns to intended website, move on to exploiting!**
**Usually give `Invalid Host Header` Error**
**Also useful to check CORS headers like Origin, X-Forwarded-For, X-Forwarded-Host, etc**

## Flawed Host Validation
### Injection Points
- Uncheck ports -> `Host: <NORMAL>:<INJECTION>`
- Unchecked full domain name -> `Host: <INJECTION><NORMAL>`
	-> `Host: <NORMAL>.<INJECTION>`
- Controlled Subdomain -> `Host: <INJECTION>.<NORMAL>`
- Embedded Credentials -> `Host: <NORMAL>@<INJECTION>`
- Fragments -> `Host: <INJECTION>#<NORMAL>`

### Ambiguous Requests
**See if there are discrepancies between how front and backend parse headers**
- Duplicate Host headers
- Give absolute URL as path
- Add spaces to wrapped Host headers

### Host Override
**Make your request appear as their proxy**
**Param Miner's Guess Headers automates this**
- X-Forwarded-Host
- X-Host
- X-Forwarded-Server
- X-HTTP-Host-Override
- Forwarded
- Origin (Supplies URL)
#### IP based
- X-Forwarded-IP
- X-Forwarded-For

# Route Based SSRF
`Host: <DOMAIN>` -> If response, [Intranet Access](3.%20Methodology/3.2%20Exploitation/Host%20Header%20Attacks.md#Intranet%20Access)

