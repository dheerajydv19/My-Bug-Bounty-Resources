# Authentication Vulnerabilities

## Tip -
1. If you login on any website using google login, if its not asking which google account you want to use, its a misconfiguation bug.
- Exploit - Now I will login via Oauth -> Google -> Complete the steps to authenticate -> Sign out all including Google account -> Sign in again via Oauth -> Direct access to the account without authentication
- Time to attack:
Victim logs into redacted.com account via Google on public computer => Moments later, victim leaves their computer (despite being signed out of redacted.com and Google account) => At this point, anyone can access the victim’s account using Google.

