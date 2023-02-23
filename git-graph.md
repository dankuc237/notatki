# FULL WORKFLOW
## BASIC WORKFLOW
```mermaid
graph TB
        CHECK_GIT["Sprawdź wersję git<br><code>$ git --version</code>"]
        FIRST_SETTING_GIT["Konfiguracja git po raz pierwszy, można dodać nick i mail<br><code>$ git config --global user.name Your_Name<br>$ git config --global user.email Your-Email<br>Zobacz wszystkie dostępne pola<br>$ git config --list</code>"]
        INITIALIZE_GIT_REPO["Inicjalizacja repozytorium<br>LOKALNIE w folderze tworzy folder .git<br><code>$ git init</code>"]
        CREATE_GITIGNORE["Stwórz plik .gitignore<br><code>$ touch .gitignore</code>"]
        FILE_CREATION["Stworzenie pliku"]
        ADD_FILE_TO_STAGING_AREA["Dodanie pliku do staging area (jest śledzony)<br><code>$ git add nazwa_pliku #konkretny plik<br>$ git add . #wszystkie pliki w folderze</code>"]
        CHECK_IF_FILES_ADDED_TO_TRACKING["Wyświetl jakie zmiany zostały wprowadzone<br>i czekają na commit w danym branchu<br><code>$ git status</code>"]    
        CHANGES_IN_FILE["Wprowadzenie zmian w kodzie"]
        COMMIT_CHANGES_TO_LOCAL_REPO["Commit zmian, z opisem commita, do obecnego brancha<br><code>$ git commit -m #quot;opis_commita#quot;</code>"]
        PRINT_COMMIT_HISTORY["Wyświetlenie historii<br/>commitów<br><code>$ git log</code>"]
        REVERT_COMMIT["Cofnięcie zmian dokonanych w wybranym commicie poprzez<br>stworzenie nowego commita, który będzie zawierał odwrócone zmiany<br><code>$ git revert commit_hash</code>"]
        
        CHECK_GIT --> FIRST_SETTING_GIT
        FIRST_SETTING_GIT --> INITIALIZE_GIT_REPO
        INITIALIZE_GIT_REPO --> FILE_CREATION
        INITIALIZE_GIT_REPO --> CREATE_GITIGNORE
        INITIALIZE_GIT_REPO --> CHECK_IF_FILES_ADDED_TO_TRACKING
        INITIALIZE_GIT_REPO --> ADD_FILE_TO_STAGING_AREA
        FILE_CREATION --> ADD_FILE_TO_STAGING_AREA
        ADD_FILE_TO_STAGING_AREA --> CHECK_IF_FILES_ADDED_TO_TRACKING
        CHECK_IF_FILES_ADDED_TO_TRACKING --> COMMIT_CHANGES_TO_LOCAL_REPO
        FILE_CREATION --> CHANGES_IN_FILE
        CHANGES_IN_FILE --> ADD_FILE_TO_STAGING_AREA
        ADD_FILE_TO_STAGING_AREA --> COMMIT_CHANGES_TO_LOCAL_REPO 
        COMMIT_CHANGES_TO_LOCAL_REPO --> PRINT_COMMIT_HISTORY
        COMMIT_CHANGES_TO_LOCAL_REPO --> REVERT_COMMIT
```
## GITHUB
```mermaid
graph TB
        CREATE_GITHUB_REPO["Należy stworzyć repozytorium<br>na github.com, przez przeglądarkę, na github.com"]
        ADD_FILE_TO_REMOTE_REPO["Push istniejącego lokalnie repozytorium do github<br><code>$ git remote add origin https://github.com/GH_username/GH_reponame.git</code><br>- <code>git remote add</code> służy do dodania odnośnika do zdalnego repozytorium, którego nazwa jest <code>origin</code><br>- adres ten wskazuje na repozytorium na GitHubie,"]
        PUSH_TO_GITHUB["Przesyłanie zmian do repozytorium zdalnego<br><code>$ git push https://GITHUB_ACCESS_TOKEN@github.com/GITHUB_USERNAME/REPOSITORY_NAME.git</code><br>origin -domyślna adres URL zdalnego repozytorium,(skonfigurowany <code>git remote add</code>)<br>main -nazwa głównej gałęzi (ang. main branch) w repozytorium"]
        RENAME_MAIN["zmień nazwę głównego brancha na main<br><code>$ git branch -M main</code>"]
        UPDATE_LOCAL_REPOSITORY["Pobranie (synchronizacja)<br>zmian z repozytorium zdalnego<br><code>$ git pull origin main</code>"]

        ADD_FILE_TO_REMOTE_REPO --> UPDATE_LOCAL_REPOSITORY
        ADD_FILE_TO_REMOTE_REPO --> RENAME_MAIN
        RENAME_MAIN --> PUSH_TO_GITHUB
        CREATE_GITHUB_REPO --> ADD_FILE_TO_REMOTE_REPO

        COMMIT_CHANGES_TO_LOCAL_REPO --> PUSH_TO_GITHUB
```
        CHANGES_IN_FILE --> CHECK_IF_FILES_ADDED_TO_TRACKING
        CHECK_IF_FILES_ADDED_TO_TRACKING-->FILE_CREATION
---
## BRANCH
```mermaid
graph TB
        DELETE_BRANCH["Usuwanie branchy lokalnych<br><code>$ git branch -d nazwa_brancha</code><br>Usuwanie branchy zdalnych<br><code>$ git push origin --delete crazy-experiment<br>lub<br>$ git push origin :crazy-experiment</code>"]
        CREATE_NEW_BRANCH["Tworzenie nowego brancha<br><code>$ git branch nazwa_nowego_brancha</code>"]
        LIST_ALL_BRANCHES["Wyświetlenie listy branchy<br><code>$ git branch #lokalnie dostępne branche<br>$ git branch -a #wszystkie branche, nawet w GH</code>"]
        SWITCH_BRANCH["Przełączanie na inny branch<br><code>$ git checkout nazwa_brancha</code><br>Przełączanie na główny branch<br><code>$ git checkout main</code>"]
        CREATE_BRANCH_AND_SWITCH["Stwórz nowy branch na podstawie obecnego i przejdź do niego<br><code>$ git checkout -b nazwa_nowego_brancha</code><br>Stwórz nowy branch na podstawie existing_branch i przejdź do niego<br><code>$ git checkout -b new_branch existing_branch</code>"]
        PRINT_CHECKOUT_OPERATION_HISTORY["Historia checkout (skakania po branchach)<br><code>$ git reflog</code>"]
        RENAME_BRANCH["Zmień nazwę aktualnego brancha na nowy<br><code>git branch -m new_name</code>"]
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
        CREATE_BRANCH_AND_SWITCH --> FILE_CREATION
        CREATE_BRANCH_AND_SWITCH --> CHANGES_IN_FILE
        SWITCH_BRANCH --> CHANGES_IN_FILE
        SWITCH_BRANCH --> FILE_CREATION
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