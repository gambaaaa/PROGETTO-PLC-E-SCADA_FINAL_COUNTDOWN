# Controllo Condizionamento - Sistema PLC

Un sistema completo di controllo e monitoraggio per un impianto di condizionamento sviluppato con **TiaPortal 16** (linguaggio SCL) e **PLCSim Advanced**, integrato con **OPC UA** e **Node-RED** per visualizzazione e gestione allarmi su browser.

---

## 📋 Descrizione del Progetto

Questo progetto implementa un sistema PLC per il controllo di un impianto di condizionamento. La logica di controllo è sviluppata in linguaggio **SCL** (Structured Control Language) su TiaPortal 16. Il sistema è diviso in componenti hardware (simulati tramite PLCSim Advanced) e componenti software di frontend per il monitoraggio e la gestione degli allarmi tramite OPC UA.

### Caratteristiche Principali

- **Programmazione PLC**: Logica di controllo sviluppata in **linguaggio SCL** con TiaPortal 16 per SIMATIC S7-1500
- **Simulazione Hardware**: Utilizzo di PLCSim Advanced per simulare il funzionamento del PLC
- **Protocollo OPC UA**: Comunicazione standardizzata tra PLC e applicazioni client
- **Dashboard Node-RED**: Interfaccia web interattiva per monitoraggio e gestione allarmi
- **Gestione Allarmi**: 5 allarmi implementati con livelli di gravità
- **Sequenze di Funzionamento**: Documentation completa del comportamento normale e in caso di allarme

---

## 📁 Struttura del Progetto

### `Simulazione/` - Progetto PLCSim
Contiene la simulazione del programma PLC e la documentazione del funzionamento:

- **`Simulazione.sim16`**: File principale della simulazione PLCSim Advanced
- **`Logs/`**: Sequenze di funzionamento esportate in formato Excel:
  - `tabella_sequenza_base_naturale.xlsx` - Sequenza di funzionamento normale
  - `tabella_sequenza_base_naturale_1.xlsx`, `_2.xlsx` - Varianti della sequenza normale
  - `tabella_sequenza.xlsx` - Tabella della sequenza con valori parametri
  - File aggiuntivi con log di esecuzione e allarmi
- **`AdditionalFiles/`**: File di supporto e configurazione

### `screenshots/` - Documentazione Visuale
Raccolta di screenshot che documentano il funzionamento del sistema:

- **`allarmi_dashboard.png`** - Dashboard Node-RED con visualizzazione allarmi
- **`flowcharts.png`** - Diagrammi di flusso della logica di controllo
- **`opc_UA.png`** - Configurazione protocollo OPC UA
- **`server_opcua.png`** - Server OPC UA in esecuzione
- **`sequenza_corretta.png`** - Sequenza di funzionamento corretto
- **`sequenza_allarme_sottopressione.png`** - Sequenza durante allarme di sottopressione
- **`tabella_sim.png`** - Tabella di simulazione parametri

### `PROGETTO PLC E SCADA.ap16`
Progetto principale TiaPortal 16 contenente:
- Programma PLC in linguaggio **SCL** (Structured Control Language)
- Simboli e variabili del progetto
- Configurazione hardware (SIMATIC S7-1500)
- Interfacce OPC UA

### `client_serbatoio.uap`
Configuration file per **UA Expert**:
- Permette la connessione al server OPC UA del PLC
- Visualizzazione in tempo reale dei parametri:
  - Livello del serbatoio
  - Pressione dell'impianto
  - Temperatura di funzionamento
  - Stato della macchina
  - **Stato delle valvole** (apertura/chiusura e posizioni)
  - **Stato degli allarmi** (attivi/inattivi con timestamp e livello di gravità)
- Interfaccia user-friendly per monitoraggio dati in tempo reale

### `allarmi_flows.json`
Configurazione di **Node-RED** contenente:
- **Flow di visualizzazione**: Dashboard interattiva per monitoraggio
- **5 Allarmi implementati**:
  1. **Abilitazione**: Lo stato di abilitazione della macchina
  2. **Temperatura**: Allarme quando il valore supera il limite
  3. **Livello**: Allarme quando il livello supera il limite massimo
  4. **Pressione alta**: Allarme per sovrapressione
  5. **Sottopressione**: Allarme per bassa pressione
- **Livelli di gravità**: Classificazione degli allarmi per priorità
- **Informazioni generali**: 
  - Stato corrente della macchina
  - Valore istantaneo di livello, pressione e temperatura

---

## ⚙️ Tecnologie Utilizzate

| Componente | Tecnologia | Versione |
|-----------|-----------|---------|
| **PLC Programming** | TiaPortal V16 | 16.0 |
| **Simulazione Hardware** | PLCSim Advanced | - |
| **PLC Target** | SIMATIC S7-1500 | - |
| **Protocollo Comunicazione** | OPC UA | - |
| **Frontend Monitoraggio** | Node-RED | - |
| **Interfaccia Client** | UA Expert + Browser | - |

---

## 📊 Descrizione dei Parametri Monitorati

| Parametro | Unità | Descrizione |
|-----------|-------|------------|
| **Livello** | L | Percentuale di riempimento del serbatoio |
| **Pressione** | bar | Pressione dell'impianto |
| **Temperatura** | °C | Temperatura di funzionamento |
| **Stato Macchina** | - | Vedasi la struttura della macchina a stati |
| **Allarme** | - | Tipo e gravità dell'allarme attivo |

---

## 🔐 Allarmi Implementati

### 1. **Abilitazione** (Enable Alarm)
- Stato: Macchina abilitata/disabilitata
- Gravità: Informativa

### 2. **Temperatura** (Temperature Alarm)
- Trigger: Superamento soglia massima configurata
- Gravità: Alta

### 3. **Livello** (Level Alarm)
- Trigger: Superamento livello massimo serbatoio
- Gravità: Alta

### 4. **Pressione Alta** (Overpressure Alarm)
- Trigger: Superamento pressione massima
- Gravità: Critica

### 5. **Sottopressione** (Underpressure Alarm)
- Trigger: Pressione al di sotto del minimo
- Gravità: Alta

---

## 📈 Sequenze di Funzionamento

Le sequenze di funzionamento sono documentate in file Excel nella cartella `Simulazione/`:

- **Sequenza Naturale**: Funzionamento senza interventi (`sequenza_base_naturale.xlsx` e `sequenza_base_forzata.xlsx`)
- **Sequenze Variate**: Varianti della sequenza normale per diversi scenari di test
- **Allarmi**: Comportamento del sistema durante condizioni di allarme

I file `.xlsx` contengono timestamp, valori istantanei dei parametri, stato della macchina e attivazione degli allarmi, permettendo l'analisi completa del funzionamento del sistema PLC.

---

## 🖼️ Screenshot del Sistema

![Dashboard Allarmi](screenshots/allarmi_dashboard.png)

![Configurazione OPC UA](screenshots/opc_UA.png)

![Server OPC UA](screenshots/server_opcua.png)

![Sequenza Corretta](screenshots/sequenza_corretta.png)

![Allarme Sottopressione](screenshots/sequenza_allarme_sottopressione.png)

---

## 📚 Documentazione Completa

Per una documentazione tecnica dettagliata, consultare il documento:
**`Progetto 07 - Controllo Condizionamento.pdf`**

Questo documento contiene:
- Specifiche tecniche complete
- Diagrammi del sistema
- Descrizione dettagliata della logica di controllo
- Istruzioni di installazione e configurazione
- Manuale operativo

---

## 📝 Note Implementative

- Il sistema utilizza comunicazione **OPC UA** per garantire interoperabilità e sicurezza
- La simulazione è completamente virtuale, nessun hardware fisico richiesto
- Le soglie di allarme sono configurabili nel programma PLC
- Il sistema supporta logging dei dati per analisi successive
- Dashboard Node-RED è responsiva e accessibile da qualsiasi dispositivo sulla rete