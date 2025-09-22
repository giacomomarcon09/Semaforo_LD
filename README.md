# 🚦 Progetto Semaforo (CODESYS)

Questo progetto implementa la gestione di due semafori:  
- **Semaforo Auto**  
- **Semaforo Pedoni**

---

##  Funzionamento normale
- Il semaforo **Auto** è **verde**.  
- Il semaforo **Pedoni** è **rosso**.  
- Quando i pedoni premono il pulsante:
  1. Il semaforo Auto passa **verde → giallo → rosso**.  
  2. Il semaforo Pedoni diventa **verde** per un tempo impostato (es. `5s`).  
  3. Alla scadenza del tempo, il semaforo Pedoni torna **verde → giallo → rosso**, mentre semaforo Auto torna **verde**.

---

##  Modalità Notte
- Attivabile con un pulsante **ritentivo**.
- Entrambi i semafori lampeggiano **giallo** con una periodo impostabile (es. `0.5s`).  
- Se durante la modalità notte viene premuto il pulsante Pedoni:
  - Il semaforo Auto diventa **rosso**.  
  - Il semaforo Pedoni diventa **verde** per la durata impostata.  
  - Alla fine del tempo, i due semafori tornano in **lampeggio giallo**.

---

##  Struttura dati

- **`Enum_stoplight`**  <img width="157" height="98" alt="Enum" src="https://github.com/user-attachments/assets/27db544d-b196-4dc4-b6e0-f6ac8850552a" align="right"/>
  Enumeratore che definisce gli stati possibili di un semaforo:  
  `Red`, `Yellow`, `Green`, `Off`.
  Usato per evitare il caso di più stati (luci) nello stesso istante <br clear="all">

- **`Struct_stoplight`**   <img width="139" height="97" alt="Struct" src="https://github.com/user-attachments/assets/35be4dd5-5b30-4c00-8afa-05184e29f033" align="right"/>
  Struttura con variabili (vedi stati Enum_stoplight) BOOL. (Solo una TRUE in qualsiasi istante)
  utile nella **visualizzazione** per comandare le singole luci. <br clear="all">

- **`EnumToStruct` (Function)**  <img width="275" height="300" alt="EnumToStruct" src="https://github.com/user-attachments/assets/39880493-fc52-4dba-a1f0-907a13f11986" align="right"/>
  Funzione con in input variabile `Enum_stoplight` e output Struct  `Struct_stoplight` "corrispettiva".  
  - Input: variabile Enum (es. `Enum_carSL`)  
  - Output: variabile Struct con `TRUE` sul campo corrispondente 
    (es. se `Enum_carSL = Enum_stoplight.Green` → `Struct_carSL.Green = TRUE`) <br clear="all">

---

##  Logica di controllo
- Implementata interamente in **Ladder (LD)**. <img width="500" height="300" alt="PRG" src="https://github.com/user-attachments/assets/115cc397-d946-425b-8d73-8dca9cf84a93" align="right"/>
- Uso di:
  - **Timer** per la gestione delle durate delle varie luci.  
  - **Blocchi `MOVE`** per impostare il valore delle variabili enum dei due semafori (cambio stato) <br clear="all">
<img width="1739" height="630" alt="ld1" src="https://github.com/user-attachments/assets/e791b0d3-83a2-4ceb-b154-f1df5fbf8554" />
<img width="1752" height="728" alt="ld22" src="https://github.com/user-attachments/assets/415b4e0a-1d3a-4f48-a15b-2ea8f2100446" />





