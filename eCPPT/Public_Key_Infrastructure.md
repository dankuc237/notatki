# Public Key Infrastructure 
Dobrze wytłumaczone: https://www.youtube.com/playlist?list=PLSNNzog5eyduzyJ8_6Je-tYOgMHvo344c

[Idiot guide dla PKI](https://www.giac.org/paper/gsec/2171/idiots-guide-public-key-infrastructure/103692)
[crashcourse PKI](https://www.nexusgroup.com/crash-course-pki/)

Public Key Infrastructure (PKI) to zbiór sprzętu, oprogramowania, ludzi, zasad i procedur niezbędnych do tworzenia, zarządzania, przechowywania, dystrybucji i unieważniania cyfrowych certyfikatów.

- X.509 is the standard for public key certificates.
- X.509 certificates are widely used in protocols like SSL/TLS, SET, S/MIME, IPsec and more.

---

**Działanie Certificate Authority (CA)**
Certificate authorities are one of the integral parts that make up a larger system called PKI (public key infrastructure)
Distributed trust model https://www.youtube.com/watch?v=LPxeYtMDxl0
The certificate can be used to verify that a public key belongs to an individual.
A certificate binds a public key with an identity by means of digital signature.
Certificate Authorities Are Like Passport Authorities for the Internet

---

W kryptografii, PKI opiera się na kilku elementach, aby upewnić się, że tożsamość osoby lub organizacji jest skutecznie potwierdzona i zweryfikowana za pomocą Certificate Authority (CA). Tożsamość użytkownika musi być unikalna dla każdego CA. Sam CA oferuje usługę zapewnienia pewności co do autentyczności.

Oto podstawowe kroki, które opisują sposób działania PKI:

1. **Generowanie kluczy:** Każdy użytkownik PKI otrzymuje parę kluczy: publiczny i prywatny. Klucz publiczny jest udostępniany publicznie, a klucz prywatny jest przechowywany poufnie przez użytkownika.
2. **Tworzenie certyfikatów:** Użytkownik, chcąc udowodnić swoją tożsamość, prosi o certyfikat od Certyfikującego Organu (CA). CA weryfikuje tożsamość użytkownika i tworzy cyfrowy certyfikat zawierający klucz publiczny użytkownika, jego dane i podpis cyfrowy CA.
3. **Rozpowszechnianie certyfikatów:** Certyfikaty są rozpowszechniane w celu używania ich przez inne osoby lub systemy w celu potwierdzenia tożsamości danego użytkownika. Te certyfikaty są przesyłane i przechowywane w zaufanych miejscach, takich jak serwery, przeglądarki internetowe, itp.
4. **Weryfikacja:** Kiedy ktoś chce sprawdzić czyjaś tożsamość w PKI, używa klucza publicznego z certyfikatu. Jeśli podpis w certyfikacie można zweryfikować za pomocą klucza publicznego CA, tożsamość jest uznawana za wiarygodną.
5. **Unieważnianie:** Jeśli klucz prywatny zostanie skompromitowany lub certyfikat straci ważność, CA może unieważnić certyfikat, informując o tym wszystkie systemy, które go posiadają.

# Funkcje PKI

```mermaid
graph LR
	funkcje_PKI[PKI Functions<br>Funkcje PKI]
    A[Authentication<br>Autoryzacja<br>Means of identification<br>Środek identyfikacji]
    C[Non repudiation<br>Niepodważalność<br>Sender cannot disown sent information<br>Nadawca nie może zaprzeczyć wysłanym danym]
    E[Confidentiality<br>Poufność<br>Secure transmission over networks<br>Bezpieczna transmisja w sieciach]
    G[Integrity<br>Integralność<br>wyklucza wprowadzenie zmian<br>w nieautoryzowany sposób<br>Data should not be altered<br>Dane nie mogą być modyfikowane]
    I[Access Control<br>Kontrola dostępu<br>Only people with security privileges<br>Tylko osoby z uprawnieniami]

	B[Cyfrowe certifikaty]
	D[Cyfrowe podpisy]
	F[Algorytmy szyfrowania]
	H[Skróty wiadomości]
	J[Pary kluczy<br>publicznych i prywatnych]

    funkcje_PKI --> A --> B
    funkcje_PKI --> C --> D
    funkcje_PKI --> E --> F
    funkcje_PKI --> G --> H
    funkcje_PKI --> I --> J

	A --> D
	G --> D
```

# Certyfikat SSL

https://www.youtube.com/watch?v=33VYnE7Bzpk

Certyfikat SSL to certyfikat danego serwera web, przyznany przez CA. Weryfikuje tożsamość i jego klucz publiczny.

```mermaid
sequenceDiagram
	autonumber
	participant C as Klient
	participant S as Server

	C ->> S: Request do komunikacji za pomocą HTTPS
	S ->> C:Server wysyła swój certyfikat SSL zawierający jego klucz publiczny

	Note left of S: Certyfikat jest podpisany<br>przez Certificate Authority
	Note over C: Podpis cyfrowy na certyfikacie SSL<br>jest stworzony przy użyciu<br>klucza prywatnego CA
	Note over C: Przeglądarka zawiera wiele wbudowanych<br>kluczy publicznych większych CA
	Note right of C: Sprawdza podpis cyfrowy
	%% zielona kłódka oznacza tyle, że przeglądarka ma pewność, że certyfikat napewno należy do servera go wysyłającego
	Note right of C: Przeglądarka generuje klucz symetryczny<br>do komunikacji z serverem
	Note right of C: Zaszyfrowanie wygenerowanie klucza symetrycznego<br>pubicznym kluczem servera

	C ->> S: Przekazanie klucza symetrycznego do servera

	Note over S: Odszyfrowanie zaszyfrowanego klucza symetryczego<br>za pomocą klucza prywatnego servera
	Note over S, C: Cały ruch od teraz szyfrowany jest za pomocą klucza symetrycznego
```

![[Pasted image 20240103095805.png]]

# Digital Signature (Cyfrowy Podpis)

https://www.youtube.com/watch?v=TmA2QWSLSPg
Elektroniczna weryfikacja wysyłającego.
Używa asymetrycznej kryptografii.

```mermaid
sequenceDiagram
	autonumber
	actor Bob
	actor Alice

	Note over Bob: Bob generuje parę kluczy<br>publiczny i prywatny
	Note over Bob: Bob zatrzymuje klucz prywatny

	Bob->> Alice :  Bob przekazuje klucz publiczny Alice<br>przez publicznie dostępny sejf

	Note over Bob: Bob tworzy wiadomość
	Note over Bob: Bob tworzy skrót wiadomości
	Note over Bob: Bob szyfruje hash<br>za pomocą klucza prywatnego

	Bob->> Alice : Bob wysyła wiadomośc (Plain Text)<br>i zaszyfrowany hash do Alice

	Note over Alice: Alice pobiera klucz publiczny<br>Boba z sejfu
	Note over Alice: Alice odszyfrowuje<br>kluczem publicznym zaszyfrowny hash
	Note over Alice: Tylko klucz autora wiadomości<br>może odszyfrować zaszyfrowany skrót
	Note over Alice: Alice sprawdza integralność wiadomości:<br>generuje skrót otrzymanej wiadomości<br>porównuje wygenerowany hash<br>z otrzymanym po odszyfrowaniu
```

![[Pasted image 20240103095927.png]]
## Atak MitM

```mermaid
sequenceDiagram
	actor Bob
	actor Attacker
	actor Alice

	Note over Bob:...

	Bob ->> Attacker:Bob wysyła wiadomośc (Plain Text)<br>i zaszyfrowany hash do Alice
	Note over Attacker: Atakujący przechwytuje podpisaną wiadomość<br>i ją usuwa
	Note over Attacker:Atakujący tworzy własną wiadomość<br>i podpisuje własnym kluczem prywatnym
	Note over Attacker:Atakujący przekazuje swój klucz publiczny<br>do przechowania w publicznym sejfie
	Attacker ->> Alice: Atakujący wysyła swoją wiadomość do Alice<br>przedstawiając sie jako Bob

	Note over Alice: Alice odszyfrowuje<br>kluczem publicznym zaszyfrowny hash
	Note over Alice: ...
```

Lack of Authentication
W ataku MitM, atakujący może udawać zarówno nadawcę, jak i odbiorcę. Atakujący może podać swój własny klucz publiczny jako zastępczy dla prawdziwego klucza odbiorcy i użyć własnego klucza prywatnego do podpisania fałszywego dokumentu.

# Digital Certificate

https://www.youtube.com/watch?v=UbMlPIgzTxc  
https://help.webex.com/pl-pl/article/WBX42278/Czym-jest-certyfikat-cyfrowy-X.509
Creating a rogue CA certificate - http://www.win.tue.nl/hashclash/rogue-ca/
Certyfikaty cyfrowe (Digital Certificates) to elektroniczne dane uwierzytelniające:

- wydawane przez zaufaną trzecią stronę
- weryfikuje tożsamość właściciela
- sprawdza, czy właściciel jest właścicielem klucza publicznego

Zapobiega podszywaniu się przy użyciu podpisu cyfrowego [[Public_Key_Infrastructure#Atak MitM]].
Bazuje na zaufaniu do wystawiającego certyfikat (Certification Authority)

```mermaid
sequenceDiagram
	autonumber
	actor Bob
	actor Alice


	Note over Bob: Bob generuje parę kluczy<br>publiczny i prywatny
	Note over Bob: Bob zatrzymuje klucz prywatny
	Note over Bob: Bob jest w posiadaniu certyfikatu<br>weryfikującego jego tożsamość


	Note over Bob: Bob tworzy wiadomość
	Note over Bob: Bob tworzy skrót wiadomości
	Note over Bob: Bob szyfruje hash<br>za pomocą klucza prywatnego

	Bob->> Alice : Bob wysyła wiadomośc,<br>zaszyfrowany hash, klucz publiczny<br>oraz certyfikat bezpośrednio Alice

	Note over Alice: Alice odszyfrowuje<br>kluczem publicznym zaszyfrowny hash
	Note over Alice: Tylko klucz autora wiadomości<br>może odszyfrować zaszyfrowany skrót
	Note over Alice: Alice sprawdza integralność wiadomości<br>generuje skrót otrzymanej wiadomości<br>porównuje wygenerowany hash<br>z otrzymanym po odszyfrowaniu
```

![[Pasted image 20240103095619.png]]