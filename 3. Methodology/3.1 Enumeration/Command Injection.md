# Detecting Command Injection
*Exploit -> [[Command Injection]]*
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

## Blind Injection Detection
*Exploit -> [[3.3 Command Injection#Blind Command Injection]]*
### Sleep - Can't use with `&`
Bash - `;sleep 5;#`

### Ping
Bash - `& ping -c 5 127.0.0.1 &`
Cmd - `& ping /n 5 127.0.0.1 &`
