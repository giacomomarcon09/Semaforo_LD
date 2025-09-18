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
  3. Alla scadenza del tempo, il semaforo Pedoni torna **verde → giallo → rosso**, mentre semaforo Auto torna **verde**.

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
  Usato per evitare il caso di più stati (luci) nello stesso istante

- **`Struct_stoplight`**  
  Struttura con variabili (vedi stati Enum_stoplight) BOOL. (Solo una TRUE in qualsiasi istante)
  utile nella **visualizzazione** per comandare le singole luci.

- **`EnumToStruct` (Function)**  
  Funzione con in input variabile `Enum_stoplight` e output Struct  `Struct_stoplight` "corrispettiva".  
  - Input: variabile Enum (es. `Enum_carSL`)  
  - Output: variabile Struct con `TRUE` sul campo corrispondente (es. `Struct_carSL`)  
    (es. se `Enum_carSL = Enum_stoplight.Green` → `Struct_carSL.Green = TRUE`)

---

## ⚙️ Logica di controllo
- Implementata interamente in **Ladder (LD)**.
- Uso di:
  - **Timer** per la gestione delle durate delle varie luci.  
  - **Blocchi `MOVE`** per impostare il valore delle variabili enum dei due semafori (cambio stato)
