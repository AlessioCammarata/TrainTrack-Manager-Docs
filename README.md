# 🚂 TrainTrack Manager

> [cite_start]Sistema integrato per il controllo, il monitoraggio e l'automazione di un plastico ferroviario tramite Arduino e Python[cite: 334, 356].

![Cover Image](media/cover-image.jpg)
[cite_start]*Il sistema in funzione presso la stazione "Termini" del plastico[cite: 348].*

---

## 📝 Descrizione del Progetto
[cite_start]TrainTrack Manager è un'applicazione sviluppata per gestire un plastico ferroviario domotico[cite: 334]. [cite_start]Il sistema permette di comandare le locomotive tramite protocollo DCC, gestire i deviatoi attraverso una scheda relè e monitorare la posizione dei treni mediante sensori RFID[cite: 14, 406].

[cite_start]L'obiettivo principale è garantire la sicurezza del circuito attraverso un sistema di automazione che previene le collisioni tra le locomotive[cite: 405, 571].

---

## 🏗️ Architettura Hardware
[cite_start]Il progetto utilizza un'architettura a doppio microcontrollore per separare la gestione della potenza dalla logica di tracciamento[cite: 413, 416].

### Controllo Locomotive e Potenza (Arduino Mega 2560)
* [cite_start]**Arduino Mega 2560**: Gestisce la generazione del segnale DCC e l'invio dei comandi ai decoder delle locomotive[cite: 421].
* [cite_start]**Motor Shield Rev3**: Montato sull'Arduino Mega, si occupa della modulazione della corrente per trasmettere i messaggi ai binari[cite: 152, 422].
* [cite_start]**Protocollo DCCpp**: Permette di nascondere i pacchetti di comando all'interno della corrente alternata di alimentazione[cite: 142, 483].

![Motor Shield](media/MotorShield.jpg)
[cite_start]*Dettaglio dell'Arduino Mega con Motor Shield Rev3 installato[cite: 431].*

### Gestione Scambi e Protezione Circuitale
* [cite_start]**Scheda Relè Optoisolata**: Utilizzata per comandare i deviatoi a 18V garantendo l'isolamento fisico dai circuiti logici di Arduino[cite: 186, 439].
* [cite_start]**Sicurezza**: Sono stati implementati diodi e LED polarizzati per assorbire i segnali di ritorno causati dalle bobine dei relè[cite: 192, 440].

![Optoisolator Turnouts](media/OptoisolatorTurnouts.jpg)
[cite_start]*Modulo relè optoisolato per la gestione dei deviatoi[cite: 95, 171].*

### Sistema di Rilevamento (Arduino Uno Rev 3)
* [cite_start]**Tracking RFID**: Una rete di 8 sensori MFRC522 identifica univocamente ogni locomotiva al suo passaggio[cite: 210, 456].
* [cite_start]**Cablaggio**: Utilizzo di cavi di diametro tra 2 e 3 mm per ridurre le cadute di tensione lungo il circuito[cite: 457].

![RFID Detector](media/RFIDdetector.jpg)
[cite_start]*Sensore RFID posizionato in un punto sensibile del tracciato per il monitoraggio[cite: 256, 408].*

---

## 💻 Architettura Software
[cite_start]L'interfaccia grafica (GUI) è stata sviluppata in **Python** utilizzando il paradigma della programmazione orientata agli oggetti (OOP)[cite: 392, 545].

### Tecnologie Utilizzate
* [cite_start]**Tkinter**: Utilizzata per la realizzazione dell'interfaccia grafica standard[cite: 604].
* [cite_start]**Threading & Queue**: Gestione della programmazione concorrente per leggere i dati dai sensori in background senza bloccare la GUI[cite: 614, 622].
* [cite_start]**OpenCV**: Implementata per l'integrazione di una videocamera per il monitoraggio visivo del circuito[cite: 608, 609].
* [cite_start]**pySerial**: Gestisce la comunicazione bidirezionale con i microcontrollori tramite porta seriale[cite: 606].

### Struttura Logica
[cite_start]Il software è diviso in classi specializzate per massimizzare la modularità[cite: 546, 591]:

![Logic Structure](media/logic-structure.png)
[cite_start]*Diagramma delle dipendenze logiche tra i moduli del programma[cite: 631, 648].*

---

## 🤖 Algoritmo di Automazione
[cite_start]Il sistema di automazione intelligente opera costantemente per prevenire incidenti[cite: 985]:
1. [cite_start]**Acquisizione**: I dati dei tag RFID vengono processati in ordine FIFO tramite la libreria Queue[cite: 880].
2. [cite_start]**Analisi**: L'algoritmo calcola i "punti critici", ovvero le intersezioni tra i percorsi assegnati alle locomotive[cite: 893].
3. [cite_start]**Intervento**: Se viene rilevato un rischio di collisione, il sistema devia automaticamente il percorso o arresta la locomotiva interessata[cite: 896, 990].

---

## 📂 Layout del Circuito
![High Ground View](media/highground.jpg)
[cite_start]*Vista zenitale completa del plastico ferroviario TrainTrack Manager[cite: 166, 794].*

---

## 📝 Riferimenti Tecnici
* [cite_start]**Arduino DCCpp Library**: Utilizzata per la gestione delle locomotive[cite: 1118].
* [cite_start]**MFRC522 Library**: Utilizzata per l'interfaccia con i sensori RFID[cite: 1119].
* [cite_start]**Comunicazione SPI**: Protocollo utilizzato per il collegamento tra sensori e Arduino Uno[cite: 318].

**Autore:** Alessio Cammarata  
**Progetto realizzato per:** Corso di Informatica e Telecomunicazioni, A.S. [cite_start]2023/2024 [cite: 326-327].