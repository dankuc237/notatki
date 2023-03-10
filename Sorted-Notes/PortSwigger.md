<!-- TOC -->

- [Authentication vulnerabilities](#authentication-vulnerabilities)
  - [Vulnerabilities in password-based login](#vulnerabilities-in-password-based-login)
    - [Brute-force attacks](#brute-force-attacks)
      - [Brute-forcing usernames/passwords](#brute-forcing-usernamespasswords)
      - [Username enumeration](#username-enumeration)
        - [LAB Username enumeration via different responses](#lab-username-enumeration-via-different-responses)
        - [LAB Username enumeration via subtly different responses](#lab-username-enumeration-via-subtly-different-responses)
        - [LAB Username enumeration via response timing](#lab-username-enumeration-via-response-timing)
    - [Flawed brute-force protection](#flawed-brute-force-protection)
        - [LAB Broken brute-force protection, IP block](#lab-broken-brute-force-protection-ip-block)
      - [Account locking](#account-locking)
        - [LAB Username enumeration via account lock](#lab-username-enumeration-via-account-lock)
      - [User rate limiting](#user-rate-limiting)
        - [LAB Broken brute-force protection, multiple credentials per request](#lab-broken-brute-force-protection-multiple-credentials-per-request)
    - [HTTP basic authentication](#http-basic-authentication)
  - [Vulnerabilities in multi-factor authentication](#vulnerabilities-in-multi-factor-authentication)
    - [Two-factor authentication tokens](#two-factor-authentication-tokens)
    - [Bypassing two-factor authentication](#bypassing-two-factor-authentication)
        - [LAB 2FA simple bypass](#lab-2fa-simple-bypass)
    - [Flawed two-factor verification logic](#flawed-two-factor-verification-logic)
        - [LAB 2FA broken logic](#lab-2fa-broken-logic)
    - [Brute-forcing 2FA verification codes](#brute-forcing-2fa-verification-codes)
        - [LAB 2FA bypass using a brute-force attack](#lab-2fa-bypass-using-a-brute-force-attack)

<!-- /TOC -->
# Authentication vulnerabilities
## Vulnerabilities in password-based login
### Brute-force attacks
#### Brute-forcing usernames/passwords
#### Username enumeration
you should pay particular attention to any differences in:
* Status codes
* Error messages
* Response times
##### LAB Username enumeration via different responses
d??ugo????/rozmiar odpoweidzi mo??e by?? inna dla zalogowanego i niezalogowanego usera, np. pojawia si?? wiadomo???? "niepoprawne dane";  
 "b????dny login i has??o", przy poprawnym loginie zmienia si?? w "b????dne has??o"
##### LAB Username enumeration via subtly different responses
j.w. ale odpoweid?? dla poprawnego loginu jest nieznacznie inna ni?? dla niepoprawnego
##### LAB Username enumeration via response timing
### Flawed brute-force protection
##### LAB Broken brute-force protection, IP block
je??li IP jest blokowane po zbyt wielu nieudanych pr??bach logowania mo??na, co dr??gi raz si?? zalogowa?? - to mo??e resetowa?? licznik pr??b

je??li zbyt du??o b????dnych logowa?? to mo??e zosta?? zablokowane konto  
`X-Forwarded-For` header is supported, which allows you to spoof your IP address 
#### Account locking
##### LAB Username enumeration via account lock
je??li odpoweidnio du??o razy prubuje si?? zalogowa?? to login zostaje zablokowany, np. na 1min. Wtedy wiadom, ??e to u??ytkownik, kt??ry istnieje
#### User rate limiting
##### LAB Broken brute-force protection, multiple credentials per request
je??li aplikacja wysy??a login i has??o w formacie JSON to mo??na dodat?? list?? hase??
```JSON
"username" : "carlos",
"password" : "has??o"

//Zamieni?? na 

"username" : "carlos",
"password" : [
    "123456",
    "password",
    "qwerty"
    ...
]
```
### HTTP basic authentication
 Although fairly old, its relative simplicity and ease of implementation means you might sometimes see HTTP basic authentication being used. In HTTP basic authentication, the client receives an authentication token from the server, which is constructed by concatenating the username and password, and encoding it in Base64. This token is stored and managed by the browser, which automatically adds it to the Authorization header of every subsequent request as follows:

`Authorization: Basic base64(username:password)`



## Vulnerabilities in multi-factor authentication
### Two-factor authentication tokens
### Bypassing two-factor authentication
##### LAB 2FA simple bypass
1. zobaczy?? jak dzia??a 2FA
1. wpisaneie loginu i has??a loguje
2. wysy??a requesta o stron?? potwierdzaj??c??
3. przenosi na stron?? do potwierdzania
4. je??li kod nie potwierdza to wylogowuje

nale??y w response do requesta po zalogowaniu przej???? bezpo??rednio do nast??pnej strony
pomin???? stron?? potwierdzania kodem zmieniaj??c w response adres z (przyk??adowo) GET /2FA na /account


### Flawed two-factor verification logic

##### LAB 2FA broken logic
### Brute-forcing 2FA verification codes
##### LAB 2FA bypass using a brute-force attack
