# FULL WORKFLOW
## BASIC WORKFLOW
```mermaid
graph TB
        SPRAWDZ_WERSJE_GIT["Sprawdź wersję git<br><code>$ git --version</code>"]
        PIERWSZA_KONFIGURACJA_GIT["Konfiguracja git po raz pierwszy, można dodać nick i mail<br><code>$ git config --global user.name Your_Name<br>$ git config --global user.email Your-Email<br>Zobacz wszystkie dostępne pola<br>$ git config --list</code>"]
        INICJALIZACJA_LOKALNEGO_REPO["Inicjalizacja repozytorium<br>LOKALNIE w folderze tworzy folder .git<br><code>$ git init</code>"]
        STWÓRZ_PLIK_.GITIGNORE["Stwórz plik .gitignore<br><code>$ touch .gitignore</code>"]
        STWÓRZ_JAKIS_PLIK["Stworzenie pliku"]
        DODAJ_PLIK_DO_STAGING_AREA["Dodanie pliku do staging area (jest śledzony)<br><code>$ git add nazwa_pliku #konkretny plik<br>$ git add . #wszystkie pliki w folderze</code>"]
        SPRAWDZ_ZMIANY_W_REPO["Wyświetl jakie zmiany zostały wprowadzone<br>i czekają na commit w danym branchu<br><code>$ git status</code>"]    
        ZMIANA_KODU["Wprowadzenie zmian w kodzie"]
        COMMIT_ZMIAN_DO_LOKALNEGO_REPO["Commit zmian, z opisem commita, do obecnego brancha<br><code>$ git commit -m #quot;opis_commita#quot;</code>"]
        POKAZ_COMMIT_HISTORY["Wyświetlenie historii<br/>commitów<br><code>$ git log</code>"]
        COFNIJ_COMMIT["Cofnięcie zmian dokonanych w wybranym commicie poprzez<br>stworzenie nowego commita, który będzie zawierał odwrócone zmiany<br><code>$ git revert commit_hash</code>"]
        
        SPRAWDZ_WERSJE_GIT --> PIERWSZA_KONFIGURACJA_GIT
        PIERWSZA_KONFIGURACJA_GIT --> INICJALIZACJA_LOKALNEGO_REPO
        INICJALIZACJA_LOKALNEGO_REPO --> STWÓRZ_JAKIS_PLIK
        INICJALIZACJA_LOKALNEGO_REPO --> SPRAWDZ_ZMIANY_W_REPO
        INICJALIZACJA_LOKALNEGO_REPO --> DODAJ_PLIK_DO_STAGING_AREA
        STWÓRZ_JAKIS_PLIK --> STWÓRZ_PLIK_.GITIGNORE
        STWÓRZ_JAKIS_PLIK --> ZMIANA_KODU
        STWÓRZ_JAKIS_PLIK --> DODAJ_PLIK_DO_STAGING_AREA
        DODAJ_PLIK_DO_STAGING_AREA --> SPRAWDZ_ZMIANY_W_REPO
        SPRAWDZ_ZMIANY_W_REPO --> COMMIT_ZMIAN_DO_LOKALNEGO_REPO
        ZMIANA_KODU --> DODAJ_PLIK_DO_STAGING_AREA
        DODAJ_PLIK_DO_STAGING_AREA --> COMMIT_ZMIAN_DO_LOKALNEGO_REPO 
        COMMIT_ZMIAN_DO_LOKALNEGO_REPO --> POKAZ_COMMIT_HISTORY
        COMMIT_ZMIAN_DO_LOKALNEGO_REPO --> COFNIJ_COMMIT
        STWÓRZ_JAKIS_PLIK --> SPRAWDZ_ZMIANY_W_REPO
        ZMIANA_KODU --> SPRAWDZ_ZMIANY_W_REPO
```
## GITHUB
```mermaid
graph TB
        STWORZ_REPO_NA_GH["Należy stworzyć repozytorium<br>na github.com, przez przeglądarkę, na github.com"]
        POWIAZ_LOKALNE_I_ZDALNE_REPO["Push istniejącego lokalnie repozytorium do github<br><code>$ git remote add origin https://github.com/GH_username/GH_reponame.git</code><br>- <code>git remote add</code> służy do dodania odnośnika do zdalnego repozytorium, którego nazwa jest <code>origin</code><br>- adres ten wskazuje na repozytorium na GitHubie,"]
        PUSH_DO_GITHUB["Przesyłanie zmian do repozytorium zdalnego<br><code>$ git push https://GITHUB_ACCESS_TOKEN@github.com/GITHUB_USERNAME/REPOSITORY_NAME.git</code><br>origin -domyślna adres URL zdalnego repozytorium,(skonfigurowany <code>git remote add</code>)<br>main -nazwa głównej gałęzi (ang. main branch) w repozytorium"]
        ZMIEN_NAZWE_BRANCH_NA_MAIN["zmień nazwę głównego brancha na main<br><code>$ git branch -M main</code>"]
        UPDATE_LOKALNEGO_REPO_Z_GH["Pobranie (synchronizacja)<br>zmian z repozytorium zdalnego<br><code>$ git pull origin main</code>"]

        POWIAZ_LOKALNE_I_ZDALNE_REPO --> UPDATE_LOKALNEGO_REPO_Z_GH
        POWIAZ_LOKALNE_I_ZDALNE_REPO --> ZMIEN_NAZWE_BRANCH_NA_MAIN
        ZMIEN_NAZWE_BRANCH_NA_MAIN --> PUSH_DO_GITHUB
        STWORZ_REPO_NA_GH --> POWIAZ_LOKALNE_I_ZDALNE_REPO

        COMMIT_ZMIAN_DO_LOKALNEGO_REPO --> PUSH_DO_GITHUB
```
        SPRAWDZ_ZMIANY_W_REPO-->STWÓRZ_JAKIS_PLIK
---
## BRANCH
```mermaid
graph TB
        LIST_ALL_BRANCHES["Wyświetlenie listy branchy<br><code>$ git branch #lokalnie dostępne branche<br>$ git branch -a #wszystkie branche, nawet w GH</code>"]
        DELETE_BRANCH["Usuwanie branchy lokalnych<br><code>$ git branch -d nazwa_brancha</code><br>Usuwanie branchy zdalnych<br><code>$ git push origin --delete crazy-experiment<br>lub<br>$ git push origin :crazy-experiment</code>"]
        RENAME_BRANCH["Zmień nazwę aktualnego brancha na nowy<br><code>git branch -m new_name</code>"]
        CREATE_NEW_BRANCH["Tworzenie nowego brancha<br><code>$ git branch nazwa_nowego_brancha</code>"]
        CREATE_BRANCH_AND_SWITCH["Stwórz nowy branch na podstawie obecnego i przejdź do niego<br><code>$ git checkout -b nazwa_nowego_brancha</code><br>Stwórz nowy branch na podstawie existing_branch i przejdź do niego<br><code>$ git checkout -b new_branch existing_branch</code>"]
        SWITCH_BRANCH["Przełączanie na inny branch<br><code>$ git checkout nazwa_brancha</code><br>Przełączanie na główny branch<br><code>$ git checkout main</code>"]
        PRINT_CHECKOUT_OPERATION_HISTORY["Historia checkout (skakania po branchach)<br><code>$ git reflog</code>"]
        MERGE_BRANCHES["Łączenie wybranego brancha z aktualnym<br>aktualny zostanie merge-receiving branch<br><code>$ git merge nazwa_brancha_z_którego_pobrać_commity</code>"]
        
        LIST_ALL_BRANCHES --> DELETE_BRANCH
        LIST_ALL_BRANCHES --> CREATE_NEW_BRANCH
        CREATE_NEW_BRANCH --> SWITCH_BRANCH
        SWITCH_BRANCH --> PRINT_CHECKOUT_OPERATION_HISTORY
        LIST_ALL_BRANCHES --> SWITCH_BRANCH
        SWITCH_BRANCH --> MERGE_BRANCHES
        MERGE_BRANCHES --> DELETE_BRANCH
        LIST_ALL_BRANCHES --> CREATE_BRANCH_AND_SWITCH
        LIST_ALL_BRANCHES --> RENAME_BRANCH
        CREATE_BRANCH_AND_SWITCH --> STWÓRZ_JAKIS_PLIK
        CREATE_BRANCH_AND_SWITCH --> ZMIANA_KODU
        SWITCH_BRANCH --> ZMIANA_KODU
        SWITCH_BRANCH --> STWÓRZ_JAKIS_PLIK
```
    
# BASIC WORKFLOW
# BRANCHES
<!--https://www.atlassian.com/git/tutorials/using-branches/git-merge -->
# GITHUB


# GITHUB ACCES_TOKEN AND HOW TO PUSH TO GITHUB
1. git push using GitHub token --> Create a token in GitHub

   - Log in to GitHub and navigate to the Settings page
   - Click on Developer Settings
   - Click on Personal Access Tokens
   - Click on Generate new token
   - Skonfiguruj token

2. How to git push using GitHub token on the command line  
`$ git push https://<GITHUB_ACCESS_TOKEN>@github.com/<GITHUB_USERNAME>/<REPOSITORY_NAME>.git`

1. Automatic token authentication