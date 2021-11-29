# Detecting Command Injection
## Detection
** Enumerate and identify server language before attempting **
### Separators
Windows/Unix - `|` `||` `&` `&&`
Unix - `;` `\n` `0x0a`

### Comments
Unix - `#`
Windows - `::`

### Obvious Injection
Bash - `& echo blah &`

### Inline Injection
Bash - `<CMD>` `$(<CMD>)`

### Blind Injection Detection
#### Sleep - Can't use with `&`
Bash - `;sleep 5;#`

#### Ping
Bash - `;ping -c 5 127.0.0.1;#`
Cmd - `;ping /n 5 127.0.0.1;#`

#### Links
[3.3 Command Injection](3.3%20Command%20Injection.md)