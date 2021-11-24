# Dom Injection
**Quick cheat sheet [here](https://portswigger.net/web-security/dom-based)**
**Looking for reflection / stored HTML**
## Sources
- `document.URL`
- `document.documentURI`
- `document.URLUnencoded`
- `document.baseURI`
- `location`
- `document.cookie`
- `document.referrer`
- `window.name`
- `history.pushState`
- `history.replaceState`
- `localStorage`
- `sessionStorage`
- `IndexedDB (mozIndexedDB, webkitIndexedDB, msIndexedDB)`
- `Database`
## Sinks
- `eval()`
- `setTimeout()`
- `execCommand()`
- `document.write()`
- `document.writeln()`
- `document.domain`
- `element.innerHTML` - **Does NOT accept `<script> / <svg onload>`**
- `element.outerHTML`
- `element.insertAdjacentHTML`
- `element.onevent`

## DOM Clobbering
**Looking for user controlled variables**
### Common
- `window.<ID>` -> Make a HTML element with id `<ID>`
- `<CLASS>.protoype.*`
