# One Piece

_Difficoltà: Medium_

_____________________

# Task 1 - Set Sail

  # Deploy the machine and hoist the sail
    No Answer needed

_____________________

# Task 2 - Road Poneglyphs

-  sudo nmap -sS -sVC -Pn -p0- -A --open -T5 -vvv onepiece.thm

![1](https://github.com/Manganaccio/Manganaccio/assets/137283468/f22bc135-b3c4-4fa7-8246-a15545337781)

- la porta 21 consente di accedere tramite FTP attraverso l'username Anonymous e senza necessità di usare una password

- ftp Anonymous@onepiece.thm

![2](https://github.com/Manganaccio/Manganaccio/assets/137283468/2dd5a78f-92a9-413c-b0fa-4c3fc37f2a1b)

![3](https://github.com/Manganaccio/Manganaccio/assets/137283468/1b15d9f8-c500-4ad0-8e12-cf25170804f8)

- scarichiamo il file di testo welcome.txt ed accediamo alla directory -the_whale_tree, all'interno di quest'ultima scarichiamo i due file .road_poneglyph.jpeg e .secret_room.txt
- # welcome.txt
  _Welcome to Zou. It is an island located on the back of a massive, millennium-old elephant named Zunesha that roams the New World.
  Except this, there is not much to say about this island._

- # .secret_room.txt
  _Inuarashi: You reached the center of the Whale, the majestic tree of Zou.
  Nekomamushi: We have hidden this place for centuries.
  Inuarashi: Indeed, it holds a secret.
  Nekomamushi: Do you see this red stele ? This is a Road Poneglyph.
  Luffy: A Road Poneglyph ??
  Inuarashi: There are four Road Poneglyphs around the world. Each of them gives one of the key to reach Laugh Tale and to find the One Piece.
  Luffy: The One Piece ?? That's my dream ! I will find it and I will become the Pirate King !!!
  Nekomamushi: A lot have tried but only one succeeded over the centuries, Gol D Roger, the former Pirate King.
  Inuarashi: It is commonly known that both Emperors, Big Mom and Kaido, own a Road Poneglyph but no one knows where is the last one.
  Nekomamushi: The other issue is the power of Big Mom and Kaido, they are Emperor due to their strength, you won't be able to take them down easily.
  Luffy: I will show them, there can be only one Pirate King and it will be me !!
  Inuarashi: There is another issue regarding the Road Poneglyph.
  Nekomamushi: They are written in an ancient language and a very few people around the world can actually read them._

  # What is the name of the tree that contains the 1st Road Poneglyph?
      the whale

- l'immagine .road_poneglyph.jpeg contiene dei dati che possiamo estrarre attraverso il comando steghide extract -sf .road_poneglyph.jpeg
- i dati estratti sono una serie di caratteri che possiamo decodificare prima in Base32, poi in codice morse, poi in binary ed infine in hex
- unavolta decodificato si ottiene una serie di caratteri in Base64, essendo questo il primo di quattro Poneglyph anche a seguito di decodifica non si ottiene alcuna informazione utile
  
- visitiamo ora la pagina web essendo la porta 80 aperta
- guardando il codice sorgente si può notare un'altra frase da decodificare

![4](https://github.com/Manganaccio/Manganaccio/assets/137283468/948750ac-9db9-4765-b726-3f13c885266c)

- è necessario decodificarla prima in Base32, poi in Base64 ed infine in Base85
- _Nami ensures there are precisely 3472 possible places where she could have lost it._

(il suggerimento fornito da TryHackMe per rispondere alla domanda successiva è: Only Sea, It's Not Terrible, guardando bene le lettere maiuscole la parola è OSINT quindi sarà apportuno fare delle ricerche su google per ottenere una wordlist utile per trovare Nami)

- provvediamo ad eseguire due scansioni delle directories con gobuster, una con una wordlist già presente nel sistema (common.txt va benissimo), l'altra scansione invece con la wordlist trovata tramite OSINT (LogPose.txt)

- gobuster dir -u http://onepiece.thm/  -w /usr/share/wordlists/dirb/common.txt

![5](https://github.com/Manganaccio/Manganaccio/assets/137283468/ed5bb2a1-65c9-43a7-b802-50f96597f0bf)

- le directories trovate ci saranno utili più avanti

- gobuster dir -u http://onepiece.thm/  -w LogPose.txt   --no-error -x html

![6](https://github.com/Manganaccio/Manganaccio/assets/137283468/9fe35ef8-a693-4f11-ae6e-1dc4929ac8a5)

- visitiamo la directory trovata, possiamo ora rispondere alla seconda domanda

# What is the name of the 1st pirate you meet navigating the Apache Sea?
    Donquixote Doflamingo

- nella stessa pagina c'è un'immagine nera che al passaggio del mouse scopre un'altra immagine con una serie di informazioni poco chiare, visitiamo quindi il codice sorgente e troviamo l'immagine in chiaro denominata        rabbit_hole.png

- una volta aperta troviamo tre codici, il primo in esadecimale, il secondo in Base91 ed il terzo è cifrato in Vigenere

- decifrato il primo ed il secondo codice otteniamo la chiave decodificare l'ultimo... _Doflamingo is still standing_! Come suggerito dal nome dell'immagine siamo in un vicolo cieco, nessuna informazione utile!

- 







  
