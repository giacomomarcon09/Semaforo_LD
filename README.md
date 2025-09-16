# 🚦 Progetto Semaforo (CODESYS)

Questo progetto implementa la gestione di due semafori:  
- **Semaforo Auto**  
- **Semaforo Pedoni**

---

## 🔧 Funzionamento normale
- Il semaforo **Auto** è **verde**.  
- Il semaforo **Pedoni** è **rosso**.  
- Quando i pedoni premono il pulsante:
  1. Il semaforo Auto passa **verde → giallo → rosso**.  
  2. Il semaforo Pedoni diventa **verde** per un tempo impostato (es. `5s`).  
  3. Alla scadenza del tempo, il semaforo Pedoni torna **verde → giallo → rosso**, mentre l’Auto torna **verde**.

---

## 🌙 Modalità Notte
- Attivabile con un pulsante **ritentivo**.  
- Entrambi i semafori lampeggiano **giallo** con una frequenza impostabile (es. `0.5s`).  
- Se durante la modalità notte viene premuto il pulsante Pedoni:
  - Il semaforo Auto diventa **rosso**.  
  - Il semaforo Pedoni diventa **verde** per la durata impostata.  
  - Alla fine del tempo, i due semafori tornano in **lampeggio giallo**.

---

## 📐 Struttura dati

- **`Enum_stoplight`**  
  Enumeratore che definisce gli stati possibili di un semaforo:  
  `Red`, `Yellow`, `Green`, `Off`.

- **`Struct_stoplight`**  
  Struttura che converte lo stato dell’enum in variabili booleane:  
  utile per la **visualizzazione** e per comandare le singole lampade.  

- **`EnumToStruct` (Function)**  
  Funzione che converte un valore `Enum_stoplight` in una `Struct_stoplight`.  
  - Input: variabile Enum (es. `Enum_carSL`)  
  - Output: variabile Struct con `TRUE` sul campo corrispondente  
    (es. se `Enum_carSL = Green` → `Struct_carSL.Green = TRUE`)

---

## ⚙️ Logica di controllo
- Implementata interamente in **Ladder (LD)**.  
- Uso di:
  - **Timer** per la gestione delle durate dei segnali.  
  - **Blocchi `MOVE`** per cambiare il valore delle variabili enum dei semafori.  

---

## 📂 Contenuto del repository
- **`/ProjectBackup`** → File `.project` completo per riaprire il progetto in CODESYS.  
- **`/Source`** → Export in formato PLCopenXML.  
  - `project_full.xml` → progetto completo in un file unico.  
  - `/POU/` → singoli blocchi del programma (Main, FB, ecc.).  
