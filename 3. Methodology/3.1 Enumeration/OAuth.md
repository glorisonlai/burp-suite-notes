# OAuth Flow
## Common GET Endpoints
-   /.well-known/oauth-authorization-server
-   /.well-known/openid-configuration
## Common POST Endpoints
- /authorization
## Common Endpoint Request params
- client_id - ID of client app
- redirect_uri - URI when sending authorization code. **Commonly attacked**.
- response_type - [[OAuth#Grant Types]]
- scope - Subset of granted application data. OpenID Connect requires mandatory `openid` scope
- state - Nonce session token. Form of CSRF token. Missing/predictable states: [[3.2 CSRF]]

## Common Endpoint Response params
- client_secret - OAuth secret key
- grant_type - [[OAuth#Grant Types]]
- Access token :
	```
	{
		"access_token": Code to send to /userinfo endpoint
		"token_type": Type of code. Usually "Bearer" in OAuth
		"expires_in": Expiration (seconds)
		"scope": Subset of application data
	}
	```

## Grant Types
### Code
response_type = authorization_token
![[Pasted image 20211107141523.png]]

### Implicit
response_type = token
![[Pasted image 20211107142530.png]]
[[3.1 Implicit OAuth Tokens]]

# OpenID Connect
Extension of OAuth protocol, to provide dedicated identity and authentication layer.
Has a standardised scope
## Common GET Endpoints
-   /.well-known/jwks.json
-   /.well-known/openid-configuration
## Common POST Endpoints
- /registration
## Additional Request Params
- scope - `openid [profile|email|address|phone]`
- response_type - `id_token [token|code]`
## Additonal Response Params
- id_token - JWT of details requested by scope