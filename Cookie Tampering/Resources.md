# Cookie Tampering / Weak Authentication

## Description

This challenge focuses on insecure client-side trust. The application uses a cookie named `I_am_admin` to determine whether a user has administrative rights. However, the value is stored as an MD5 hash, and the server appears to rely solely on this client-controlled cookie to grant elevated privileges.

## How to Get the Flag

* With the DevTools, navigate to Application → Storage → Cookies → [**http://localhost**](http://localhost).
* A cookie named `I_am_admin` appears with a 32‑character hexadecimal value.
* Since MD5 hashes also have a 32‑character hex format, the value looks like a hash.
* Using an online hash cracking tool such as CrackStation, the hash can be reversed to the string `false`.
* Generate a MD5 hash with the value `true`.
* Replacing the existing cookie value with the MD5 hash of `true` and refreshing the page triggers an alert containing the flag.

## Vulnerability Explanation

* The application trusts client‑side cookies for authorization.
* Any user can freely inspect and modify cookies in the browser.
* Relying on MD5 hashes for access control provides no real protection.
* Attackers can escalate privileges to administrator simply by modifying a cookie.
* This can lead to data exposure, unauthorized actions, or complete takeover of the application.

## Prevention of Vulnerability

* Never trust client-side data.
* Never design authentification logic that might be guessed by the user.
* Avoid MD5 for anything security‑relevant; use strong hashing algorithms with proper keys or signatures.
