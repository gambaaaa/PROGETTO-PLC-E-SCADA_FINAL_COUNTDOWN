# Controllo Condizionamento - Sistema SCADA PLC

Un sistema completo di controllo e monitoraggio per un impianto di condizionamento sviluppato con **TiaPortal 16** e **PLCSim Advanced**, integrato con **OPC UA** e **Node-RED** per visualizzazione e gestione allarmi su browser.

---

## 📋 Descrizione del Progetto

Questo progetto implementa un sistema SCADA (Supervisory Control and Data Acquisition) per il controllo di un impianto di condizionamento. Il sistema è diviso in componenti hardware (simulata tramite PLCSim) e componenti software di frontend per il monitoraggio e la gestione degli allarmi.

### Caratteristiche Principali

- **Programmazione PLC**: Logica di controllo sviluppata in TiaPortal 16 per SIMATIC S7-1200
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
- **`Logs/`**: Log delle sequenze di funzionamento esportate:
  - `tabella_sequenza_base_naturale.xml` - Sequenza di funzionamento normale
  - `tabella_sequenza_base_naturale_1.xml`, `_2.xml` - Varianti della sequenza normale
  - `sequenza_base_forzata.xml` - Sequenza con forzamento valori
  - `sequenza_base_forzata_1.xml`
  - `tabella_sequenza.xml`, `sequenza_*.xml` - Log di esecuzione e allarmi
  - `MassDataHandlerLogFile.xsl` - Stylesheet per visualizzazione log
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
- Programma PLC in linguaggio IEC 61131-3 (STL/LAD)
- Simboli e variabili del progetto
- Configurazione hardware (SIMATIC S7-1200)
- Interfacce OPC UA

### `client_serbatoio.uap`
Configuration file per **UA Expert**:
- Permette la connessione al server OPC UA del PLC
- Visualizzazione in tempo reale dei parametri:
  - Livello del serbatoio
  - Pressione dell'impianto
  - Temperatura di funzionamento
  - Stato della macchina (On/Off, Running, Alarm)
- Interfaccia user-friendly per monitoraggio dati

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
  - Storico e trends

---

## ⚙️ Tecnologie Utilizzate

| Componente | Tecnologia | Versione |
|-----------|-----------|---------|
| **PLC Programming** | TiaPortal V16 | 16.0 |
| **Simulazione Hardware** | PLCSim Advanced | - |
| **PLC Target** | SIMATIC S7-1200 | - |
| **Protocollo Comunicazione** | OPC UA | - |
| **Frontend Monitoraggio** | Node-RED | - |
| **Interfaccia Client** | UA Expert + Browser | - |

---

## 🚀 Come Utilizzare il Progetto

### 1. Eseguire la Simulazione PLC

```bash
# Aprire TiaPortal 16
# File > Open > PROGETTO PLC E SCADA.ap16

# Oppure eseguire la simulazione direttamente
# Aprire Simulazione/Simulazione.sim16 in PLCSim Advanced
```

### 2. Visualizzare i Dati tramite OPC UA

**Metodo A - UA Expert:**
```bash
# Aprire UA Expert
# File > Open > client_serbatoio.uap
# Questa configurazione mostrerà tutti i parametri in tempo reale
```

**Metodo B - Browser (Node-RED):**
```bash
# Importare il flow da allarmi_flows.json in Node-RED
# Accedere alla dashboard all'indirizzo: http://localhost:1880/ui
```

### 3. Monitorare gli Allarmi

Nel dashboard Node-RED saranno visualizzati:
- **Stato della macchina**: Running / Stopped / Alarm
- **5 Allarmi**: Con indicatori di stato e gravità
- **Parametri istantanei**: Livello, Pressione, Temperatura
- **Informazioni sistema**: Timestamp, stato generale

---

## 📊 Descrizione dei Parametri Monitorati

| Parametro | Unità | Descrizione |
|-----------|-------|------------|
| **Livello** | % | Percentuale di riempimento del serbatoio (0-100%) |
| **Pressione** | bar | Pressione dell'impianto |
| **Temperatura** | °C | Temperatura di funzionamento |
| **Stato Macchina** | - | Off, Running, Alarm |
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
- Gravità: Critica

---

## 📈 Sequenze di Funzionamento

Le sequenze di funzionamento sono documentate in file Excel/XML nella cartella `Simulazione/Logs/`:

- **Sequenza Naturale**: Funzionamento senza interventi
- **Sequenza Forzata**: Simulazione con valori forzati per test allarmi
- **Allarmi**: Comportamento del sistema durante condizioni di allarme

I file `.xml` contengono timestamp, valori dei parametri e state machine del sistema.

---

## 🖼️ Screenshot del Sistema

### Dashboard di Monitoraggio
![Dashboard Allarmi](screenshots/allarmi_dashboard.png)

### Configurazione OPC UA
![Configurazione OPC UA](screenshots/opc_UA.png)

### Server OPC UA Attivo
![Server OPC UA](screenshots/server_opcua.png)

### Sequenza Corretta di Funzionamento
![Sequenza Corretta](screenshots/sequenza_corretta.png)

### Sequenza Durante Allarme
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

## 🔧 Requisiti di Sistema

### Hardware Minimo
- **CPU**: Dual-core 2.0 GHz
- **RAM**: 4 GB (8 GB consigliato)
- **Disco**: 500 MB spazio disponibile
- **Rete**: Ethernet per OPC UA

### Software Richiesto
- Windows 7/10/11 o Linux
- **TiaPortal V16** (per modificare il programma PLC)
- **PLCSim Advanced** (per eseguire la simulazione)
- **UA Expert** (per visualizzazione OPC UA)
- **Node-RED** (per dashboard browser)
- Browser web moderno (Chrome, Firefox, Edge)

---

## 📝 Note Implementative

- Il sistema utilizza comunicazione **OPC UA** per garantire interoperabilità e sicurezza
- La simulazione è completamente virtuale, nessun hardware fisico richiesto
- Le soglie di allarme sono configurabili nel programma PLC
- Il sistema supporta logging dei dati per analisi successive
- Dashboard Node-RED è responsiva e accessibile da qualsiasi dispositivo sulla rete

---

## 👤 Autore

**Stefano RINALDI**

---

## 📄 Licenza

Questo progetto è fornito per scopi educativi e didattici.

---

## 📞 Supporto

Per domande tecniche specifiche, consultare la documentazione PDF allegata o contattare l'autore del progetto.

---

**Ultima modifica**: Novembre 2025  
**Versione**: 1.0
