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

- gobuster dir -u http://10.10.156.167/sitemap -w /usr/share/wordlists/dirb/big.txt  --no-error -t 200 -x php,html

![4](https://github.com/Manganaccio/Manganaccio/assets/137283468/fa5a9ca9-ecde-44db-9eba-52ed7e9d9972)

- si noti tra le nuove directories ".ssh", accedendo troviamo un file denominato _id_rsa_ utile per fare l'accesso tramite SSH
- salviamo il contenuto in un file di testo e settiamo i permessi tramite il comando _chmod 600 id_rsa_
- facciamo l'accesso al servizio SSH con il nome utente trovato in precedenza eseguendo il seguente comando
- ssh jessie@10.10.156.167 -i id_rsa

# User flag

- una volta eseguito l'accesso nella directory Documents troviamo la prima flag

      Answer: 057c67131c3d5e42dd5cd3075b198ff6 
