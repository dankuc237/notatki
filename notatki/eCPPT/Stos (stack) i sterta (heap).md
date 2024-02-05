to dwa główne obszary pamięci w programach komputerowych, które służą do przechowywania danych w różny sposób.

# Stos (stack)
Stos (stack) jest to obszar pamięci, w którym przechowywane są lokalne zmienne oraz kontekst wywołań funkcji. Jest zarządzany automatycznie przez system operacyjny i rośnie i kurczy się w trakcie wykonywania programu w odpowiedzi na wywołania i zakończenia funkcji. Dane na stosie są przechowywane w sposób LIFO (Last In, First Out), co oznacza, że ostatnio dodane elementy są pierwsze do usunięcia.
# Sterta (heap)
Sterta (heap) jest to obszar pamięci, który jest używany do dynamicznego alokowania pamięci podczas działania programu. W przeciwieństwie do stosu, zarządzanie stertą jest bardziej elastyczne, a alokacja oraz zwalnianie pamięci może być kontrolowane przez programistę. Dane na stercie są przechowywane w sposób bardziej dowolny, a dostęp do nich jest bardziej skomplikowany, ponieważ program musi zarządzać alokacją i zwalnianiem pamięci ręcznie.
# Podsumowanie
Podsumowując, stos jest wykorzystywany głównie do przechowywania lokalnych zmiennych oraz kontekstu wywołań funkcji, jest zarządzany automatycznie i działa w sposób uporządkowany (LIFO). Natomiast sterta jest obszarem pamięci do dynamicznego alokowania danych, który jest zarządzany bardziej ręcznie i umożliwia elastyczne zarządzanie pamięcią w trakcie działania programu.