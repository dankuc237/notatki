# SNMP
protokół wymiany danych między urządzeniami sieciowymi

snmpwalk -v (1/2c/3) -c public IP
snmpbulkwalk -||- . - kropka na końcu jest ważna


## dalesze szukanie danych
w tym co znalazł snmpbulkwalk zastosować 
grep -Eo ":[a-zA-Z0-9]*\." | sort | uniq
pokaże poszczególne dane i można tam znaleć procesy i inne ciekawe rzeczy
