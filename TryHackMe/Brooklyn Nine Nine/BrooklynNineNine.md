# Brooklyn Nine Nine

_Difficoltà: Easy_
__________________

# Task 1 - Deploy and get hacking

-  _nmap -p- --open -sC -sV -sS -A -T 5 -Pn -oN scan_brooklyn.txt TARGET-IP_

![Istantanea_2023-08-04_10-28-46](https://github.com/Manganaccio/Manganaccio/assets/137283468/59c9f54b-138a-412a-9541-d49a7a71f29e)

-  la scansione con nmap ci mostra 3 porte aperte:
    -  la 21 su cui gira il servizio FTP e si può accedere autenticandosi come "anonymous" senza la necessità di inserire alcuna password;
    -  la 22 su cui gira il servizio SSH;
    -  la 80 web server che ci consente di accedere al sito web.
 
-  accedendo attraverso la porta 21, si può scaricare il file presente mediante il comando: _get "nome_file"_

![Istantanea_2023-08-04_15-41-56](https://github.com/Manganaccio/Manganaccio/assets/137283468/8b71eab5-1f95-42d4-83a8-587559223ab8)

-  il file di testo fornisce informazioni relative gli utenti ed in particolare la possibilità di ottenere la password di Jake essendo molto debole
-  queste informazioni saranno utili per ottenere la sopra menzionata password di Jake con l'uso del tool hydra per accedere al suo profilo attraverso "SSH"
-  _hydra -l jake -P /usr/share/wordlists/rockyou.txt ssh://TARGET-IP_ (non è necessario inserire la porta in quanto hydra considera di default la porta 22)

![Istantanea_2023-08-04_10-43-04](https://github.com/Manganaccio/Manganaccio/assets/137283468/8edb16c5-b5cd-4b4b-b2b6-b91fd9190a75)

-  trovata la password si può ora accedere al profilo di jake
-  _ssh jake@TARGET-IP_

# User flag

-  navigando nella cartella home si può accedere alla directory di holt nel quale è presente la prima flag

![Istantanea_2023-08-04_10-44-54](https://github.com/Manganaccio/Manganaccio/assets/137283468/e5168ddf-06f8-45eb-b4d1-45e63b90e066)

    Answer: ee11cbb19052e40b07aac0ca060c23ee

# Root flag

-  per ottenere la seconda flag sarà necessario fare una scalata dei privilegi;
-  _sudo -l_

![Istantanea_2023-08-04_10-45-33](https://github.com/Manganaccio/Manganaccio/assets/137283468/6bb9ad14-6dc0-4a26-b3a2-b3b8b9dffa75)

-  navigare su [GTFOBins](https://gtfobins.github.io/) e nella pagina di less cercare la voce SUDO 
-  inserire i comandi suggeriti per scalare i privilegi di root e ottenere la flag

![Istantanea_2023-08-04_10-47-58](https://github.com/Manganaccio/Manganaccio/assets/137283468/744c80ea-d46e-420d-a639-8a68305aecec)

    Answer: 63a9f0ea7bb98050796b649e85481845
