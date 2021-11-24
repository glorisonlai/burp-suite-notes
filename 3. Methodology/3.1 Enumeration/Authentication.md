# Enumerating Auth Systems
**Use Burp Intruder, or write your own threaded script**
**If possible, register an account first to tell the difference between good/bad requests**
**Same principles apply to resetting passwords/forgot passwords/registering accounts**
## Quick Wins
- Different response text/size based on correct usernames
- Different response time based on:
	- Correct/incorrect username
	- Length of password

## Bypassing Rate Limiting
- Giving correct credentials at fixed interval
- Purposely rate limiting brute force trials

## Bypassing Account Lockout
- Custom error message may occur for valid usernames

## MFA
- Make sure 2FA is needed before accessing pages
### Turbo Intruder
