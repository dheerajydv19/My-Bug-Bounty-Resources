# Authentication Vulnerabilities

## Tip -
1. If you login on any website using google login, if its not asking which google account you want to use, its a misconfiguation bug.
- Exploit - Now I will login via Oauth -> Google -> Complete the steps to authenticate -> Sign out all including Google account -> Sign in again via Oauth -> Direct access to the account without authentication
- Time to attack:
Victim logs into redacted.com account via Google on public computer => Moments later, victim leaves their computer (despite being signed out of redacted.com and Google account) => At this point, anyone can access the victim’s account using Google.

# 2FA Bypass Techniques
  - Response Manipulation: In response, if "success":false Change it to "success":true
  - Status Code Manipulation: If Status Code is 4xx Try to change it to 200 OK and see if it bypass restrictions
  - 2FA Code Reusability: Same code can be reused
  - 2FA Code Leakage in Response: Check the response of the 2FA Code Triggering Request to see if the code is leaked
  - Lack of Brute-Force Protection: Possible to brute-force any length 2FA Code
  - Missing 2FA Code Integrity Validation: The 2FA code of any user account can be used to bypass the victim 2FA code
  - Password Reset Disable 2FA: 2FA gets disabled when changing the Email/Password
  - Bypass 2FA with null or 000000: Enter the code 000000 or null to bypass the 2FA protection
  
  
