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
długość/rozmiar odpoweidzi może być inna dla zalogowanego i niezalogowanego usera, np. pojawia się wiadomość "niepoprawne dane";  
 "błędny login i hasło", przy poprawnym loginie zmienia się w "błędne hasło"
##### LAB Username enumeration via subtly different responses
j.w. ale odpoweidź dla poprawnego loginu jest nieznacznie inna niż dla niepoprawnego
##### LAB Username enumeration via response timing
### Flawed brute-force protection
##### LAB Broken brute-force protection, IP block
jeśli IP jest blokowane po zbyt wielu nieudanych próbach logowania można, co drógi raz się zalogować - to może resetować licznik prób

jeśli zbyt dużo błędnych logowań to może zostać zablokowane konto  
`X-Forwarded-For` header is supported, which allows you to spoof your IP address 
#### Account locking
##### LAB Username enumeration via account lock
jeśli odpoweidnio dużo razy prubuje się zalogować to login zostaje zablokowany, np. na 1min. Wtedy wiadom, że to użytkownik, który istnieje
#### User rate limiting
##### LAB Broken brute-force protection, multiple credentials per request
jeśli aplikacja wysyła login i hasło w formacie JSON to można dodatć listę haseł
```JSON
"username" : "carlos",
"password" : "hasło"

//Zamienić na 

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
1. zobaczyć jak działa 2FA
1. wpisaneie loginu i hasła loguje
2. wysyła requesta o stronę potwierdzającą
3. przenosi na stronę do potwierdzania
4. jeśli kod nie potwierdza to wylogowuje

należy w response do requesta po zalogowaniu przejść bezpośrednio do następnej strony
pominąć stronę potwierdzania kodem zmieniając w response adres z (przykładowo) GET /2FA na /account


### Flawed two-factor verification logic

##### LAB 2FA broken logic
### Brute-forcing 2FA verification codes
##### LAB 2FA bypass using a brute-force attack
