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

- scarichiamo i file di testo _task.txt_ e _locks.txt_
- # Task.txt
  _1.) Protect Vicious.
  2.) Plan for Red Eye pickup on the moon.
  -lin_

# Who wrote the task list? 
    Answer: Lin


