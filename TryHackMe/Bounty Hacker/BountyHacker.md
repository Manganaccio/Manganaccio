# Bounty Hacker

_Difficoltà: Easy_
__________________

# Task 1 - Living up to the title. 

# Deploy the machine.
    Answer: No answer needed


# Find open ports on the machine
    Answer: No answer needed

- _sudo nmap -p0- --open -sCV -sS -A -T5 -Pn TARGET-IP_

![Istantanea_2023-08-18_12-31-17](https://github.com/Manganaccio/Manganaccio/assets/137283468/824502ab-8dbf-4614-b61e-2661a6c93cfe)

- la porta 21 consente di accedere tramite FTP attraverso l'username Anonymous e senza necessità di usare una password
- ftp anonymous@TARGET-IP

![Screenshot_2023-10-20_08-46-11](https://github.com/Manganaccio/Manganaccio/assets/137283468/966496ea-e5cd-40a6-9f8f-5f2c2250963d)

- scarichiamo i file di testo _task.txt_ e _locks.txt_; leggendoli si potrà rispondere alle due domande successive 

- # Task.txt

![Istantanea_2023-08-18_12-35-09](https://github.com/Manganaccio/Manganaccio/assets/137283468/378099cf-7a55-4d4d-b11e-75cae27261e4)


# Who wrote the task list? 
    Answer: Lin

- # Locks.txt

![Istantanea_2023-08-18_12-35-39](https://github.com/Manganaccio/Manganaccio/assets/137283468/3a7e0aba-4a85-47b7-bef8-bce79b99d481)

# What service can you bruteforce with the text file found?
    Answer: SSH

- attraverso la lista trovata nel file _Locks.txt_ si potrà fare il bruteforce con hydra per accedere attraverso la porta 22, trovata aperta mediante la scansione con nmap
- _hydra -l lin -P locks.txt ssh://TARGET-IP_  

![Istantanea_2023-08-18_12-38-47](https://github.com/Manganaccio/Manganaccio/assets/137283468/5549e4ed-dd13-43b7-b5e2-44d1b5db16d5)

# What is the users password?
    Answer: RedDr4gonSynd1cat3

- _ssh lin@TARGET-IP_
- una volta effettuato l'accesso si potrà leggere l aprima flag nel file _user.txt_

![Istantanea_2023-08-18_12-41-17](https://github.com/Manganaccio/Manganaccio/assets/137283468/c07ca046-1ddf-4764-8b32-9fb0e014737f)

# user.txt
    Answer: THM{CR1M3_SyNd1C4T3}

- per ottenere la seconda flag sarà necessario fare una scalata dei privilegi
- _sudo -l_

![Istantanea_2023-08-18_12-42-14](https://github.com/Manganaccio/Manganaccio/assets/137283468/48f98c1a-e77e-4ea6-9d64-a1fa3f507824)

- navigare su GTFOBins e nella pagina di _tar_ cercare la voce SUDO
- inserire i comandi suggeriti per scalare i privilegi di root e ottenere la flag

![Istantanea_2023-08-18_12-44-55](https://github.com/Manganaccio/Manganaccio/assets/137283468/496f48a2-1c73-46fa-b20f-bfe537f3a71f)

# root.txt
    Answer: THM{80UN7Y_h4cK3r}


