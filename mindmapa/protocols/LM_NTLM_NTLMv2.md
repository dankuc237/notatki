NTLM (U:389,445, T:139, 88)
NT LAN Manager
U:389 - LDAP services
U:445 - Microsoft-DS services (SMB over TCP)
T:139 - NetBIOS Session services
T:88 - Kerberos services

```mermaid
graph TD
    subgraph NTLM_Application[NTLM Application]
        SecurityProvider[Security Provider<br>- Authentication<br>- Integrity<br>- Confidentiality<br>.]
        SessionManager[Session Manager<br>- Establishes and maintains sessions<br>- Manages user credentials<br>.]
    end

```

```mermaid
graph TD

    Kerberos --> NTLM_Auth[NTLM Authentication]
    NetBIOS_Session --> NTLM_Auth
    NTLM_Auth --> Kerberos_Auth[Kerberos Authentication]
	Response --> Response_Types
	Response --> Response_Schema

    subgraph _[Transport Layer &lpar;ISO/OSI 4 Layer&rpar;]
        TCP
        UDP
    end
    subgraph NTLM_over_TCP_IP[NTLM over TCP/IP]
        TCP -->|TCP:139| NetBIOS_Session[NetBIOS Session<br>Allows two names<br>to establish connection<br>.] 
        TCP -->|TCP:88| Kerberos[Kerberos<br>Authentication services<br>.]
        UDP -->|UDP:389| LDAP[LDAP<br>Directory services<br>.]
        UDP -->|UDP:445| Microsoft_DS[Microsoft-DS<br>SMB over TCP<br>.]
    end
    subgraph NTLM_Auth[NTLM Authentication]
        Challenge[Challenge]
        Response[Response]
    end
    subgraph Kerberos_Auth[Kerberos Authentication]
	    direction LR 
        TGT[TGT]
        TGS[TGS]
        ServiceTicket[Service Ticket]
    end

	subgraph  Response_Types[LM/NTLM Response Types]
		direction LR 
        Challenge[Challenge]
        Response_Type1[Type 1 Response<br>- Initial negotiation by the client.]
        Response_Type2[Type 2 Response<br>- Sent by the server in response to Type 1. Contains a challenge.]
        Response_Type3[Type 3 Response<br>- Sent by the client in response to Type 2. Contains authentication data.]
    end
    subgraph  Response_Schema[Response Schema Ewolution]
        LM --> NTLM --> NTLMv2 --> kerberos
    end

```

Protokół NTLM obejmuje usługi autentykacyjne (Challenge-Response), które są używane do uwierzytelniania użytkowników w środowiskach Windows. 
NTLM może być używany razem z innymi usługami, takimi jak:
* LDAP (do dostępu do katalogu), NetBIOS Session (do komunikacji na poziomie sesji), 
* SMB over TCP (do udostępniania plików i drukarek)
* Kerberos (do bardziej zaawansowanych usług bezpieczeństwa). 
NTLM zapewnia mechanizmy bezpieczeństwa, takie jak uwierzytelnianie użytkowników, integralność danych i poufność.


is used either when the client is authenticating to a server using an IP address or, when the client is authenticating to a server that does not belong to the same domain

NTLM authentication is a challenge/response protocol and consists of three messages:
* Type 1 (negotiation), 
* Type 2 (challenge),
* Type 3 (authentication).


NTLM response is sent together with the LM response, most of the time .