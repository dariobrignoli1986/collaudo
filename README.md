# Fogli di Collaudo — Warcom

Suite di **moduli di collaudo digitali** per le macchine Warcom: compilano il foglio di collaudo,
validano i campi e generano il PDF finale. Sostituiscono l'Excel libero con moduli guidati e ripristinabili.
Tutti condividono lo stesso "motore" (struttura, salvataggio, PDF, foto, CSV): cambiano i contenuti
(componenti e checklist) in base alla macchina.

## I fogli (struttura repo)
`index.html` è la **home/menu** che apre i singoli fogli. Ogni foglio è un file HTML autonomo:

| File | Macchina | Versione |
|---|---|---|
| `italo.html` | Laser tubo (Fibertube Italo) | **V1.12** — pronto |
| `laser-piano.html` | Laser piano | **V1.10** — pronto |
| `plasma.html` | Plasma | V0.9 (bozza) |
| `cesoie.html` | Cesoie | V0.9 (bozza) |
| `presse-piegatrici.html` | Presse piegatrici | V1.3 |
| `automazione-laser-piano.html` | Automazione laser piano | **V1.4** — pronto · **doppio esito FAT/SAT**, tipo impianto Carico-Scarico/Magazzino |
| `automazione-laser-tubo.html` | Automazione laser tubo | **V1.9** — pronto |

> I fogli in **bozza** sono per ora copie dell'ITALO con identità propria: vanno adattati alla loro
> macchina (componenti + checklist). Lo stato d'avanzamento è in `TODO.md` (interno, non pubblicato).

Ogni foglio ha una **chiave di salvataggio propria** (`LS_KEY`): i moduli non si sovrascrivono
l'autosave a vicenda anche se aperti sullo stesso sito. Lo **sblocco password è condiviso**
(entri una volta, valgono tutti).

## Deploy (GitHub Pages)
Repo `dariobrignoli1986/collaudo`, pubblicato su https://dariobrignoli1986.github.io/collaudo/.
Per aggiornare: carica i file modificati nella **root del repo** (Add file ▸ Upload files ▸ Commit).
La home è `index.html`; non c'è più la cartella `dist/`. Pages si rigenera in ~1 minuto.

---

## Come funziona un foglio (vale per tutti)

## Come si usa
1. **Apri** il foglio della tua macchina (es. `italo.html`) con doppio clic — o dal menu `index.html`.
2. Compila: Testata → Assi → Componenti → Checklist → Prove di taglio → Note.
3. A fine collaudo: **Genera PDF** → nella finestra di stampa scegli *"Salva come PDF"*.

## Salvataggio (spegni e riaccendi)
- **Autosave**: il lavoro si salva da solo nel browser a ogni modifica. Se riapri il file sullo stesso
  PC e stesso browser, ritrovi tutto.
- **Salva .json**: scarica un file con *tutti* i dati del collaudo → è il backup vero, portabile.
- **Carica .json**: riprende un collaudo salvato, anche su un altro PC.
- **Nuovo**: azzera per iniziare un collaudo da zero.

> Il `.json` è la fonte di verità. Per non perdere lavoro tra una sessione e l'altra, salva un `.json`
> a fine giornata (l'autosave del browser può essere cancellato dalla pulizia cache).

## Assi configurabili
Nella sezione **Assi** aggiungi/rimuovi gli assi della macchina: drive, motori e "Prima movimentazione"
si rigenerano da soli e il **numero assi in testata si aggiorna automaticamente**.
Default precaricato sulla configurazione Italo (U, C1, C2, X, Z, Y, RC1-4, SC, RS1-4).

## Foto dei tagli (da telefono)
Nelle **Prove di taglio**, su ogni scheda: **📷 Aggiungi foto** apre la fotocamera (su telefono).
Ogni foto viene **rinominata in automatico** coi dati della prova (`matricola_materiale_spessore_N.jpg`,
con N progressivo) e ri-codificata in **JPEG (.jpg)** qualunque sia il formato di partenza (anche HEIC iPhone).

Le foto finiscono in **due posti**:
- **Nel PDF**: sezione finale *"Allegato fotografico"* con le foto grandi raggruppate per prova → il PDF è
  un file autonomo che contiene già le foto.
- **In un archivio `.zip`**: il bottone **🗜 Foto .zip** crea un unico archivio con tutte le foto, organizzate
  in cartelle `prova-1/`, `prova-2/`, … (file a risoluzione migliore, per l'archivio separato).

> Nota: `.rar` non è producibile da un file offline (formato proprietario), quindi si usa `.zip`. Le miniature
> pesano sul file: con molte foto salva spesso il `.json`.

## Password d'accesso (cancelletto)
All'apertura l'app chiede una password. È un **deterrente** (tiene fuori i curiosi), **non sicurezza reale**:
chi è tecnico può aggirarla. Password attuale: **`warcom`**. Una volta entrato, il dispositivo resta
sbloccato (non la richiede più).

**Per cambiare la password**: apri una pagina, premi `F12` (Console), scrivi `lockHash('nuova-password')`,
copia il valore stampato e incollalo al posto di `PW_HASH` in **ogni** foglio (è ripetuto in ciascun file).

## Da telefono
La pagina è responsive: aprila nel browser del telefono (puoi anche caricare un `.json` salvato dal PC).

## Campi espandibili
Tutti i campi di testo si **allargano da soli** man mano che scrivi, e il testo lungo è interamente
visibile anche nel PDF.

## Caratteristiche tecniche
- **Un solo file, 100% offline**: nessuna installazione, nessuna connessione di rete, nessun dato esce dal PC.
  Adatto a PC aziendale gestito da IT (non è un eseguibile, non apre porte, non è un servizio).
- Nessuna libreria esterna: il PDF si genera con la stampa del browser.

## Campi da compilare (giallo pastello)
I campi **non ancora compilati** sono evidenziati in **giallo pastello**: colpo d'occhio immediato su cosa
manca. Il giallo si spegne da solo appena scrivi nel campo. Nella checklist, una riga **senza esito**
(OK/KO/NA) si accende tutta di giallo; le righe **NA** o **"non presente"** contano come compilate.

- **I campi *Note* non sono mai evidenziati**: sono sempre facoltativi, in testata, in checklist e nelle prove
  di taglio. Stesso trattamento per *Note fibra ottica* e gli *indirizzi secondari*.
- **La sezione 2 (Assi)** è giallina finché non premi *Conferma assi*; a conferma fatta torna neutra come
  tutte le altre sezioni.
- **Il giallo non finisce nel PDF**: è un aiuto a video, la stampa esce pulita.
- **Il rosso vince sul giallo**: un campo obbligatorio mancante al momento del PDF resta rosso.
- Il bottone **👁 Da compilare** in barra accende/spegne l'evidenziazione, giallo della sezione assi compreso
  (la scelta la ricorda il browser).

## Doppio esito FAT / SAT — solo `automazione-laser-piano.html`
Gli impianti di automazione si collaudano **due volte**: **FAT** in officina, **SAT** dal cliente dopo
l'installazione. Solo questo foglio ha quindi **due esiti per riga**, indipendenti fra loro (nella scheda
storica una voce poteva essere `FAT: OK` e `SAT: N/A`).

- In testata: **eseguito da + data inizio + data fine** separati per FAT e SAT. Il blocco SAT è facoltativo.
- Il selettore **`FAT officina` / `SAT cliente`** in barra dice quale campagna stai compilando: sposta il
  **giallo** dei campi da compilare e decide **cosa il PDF pretende**. Il FAT non chiede i dati del SAT.
- La riga si blocca solo se è *"non presente"* o se è **N.A. in entrambe le fasi**.
- Il progresso mostra i due conteggi: `FAT 2/121 · SAT 3/121`.
- CSV: due colonne, `Esito FAT` ed `Esito SAT`. PDF: due righe di firma.

> Il vocabolario resta a tre valori (**OK / KO / N.A.**). Nella scheda storica c'era anche `DA TESTARE`:
> nel foglio digitale corrisponde a una **riga lasciata vuota**, che infatti si evidenzia in giallo.

## Note di collaudo: sempre aperte
La sezione **6 Note di collaudo** è l'unica **non soggetta al gating**: è disponibile fin dal primo istante,
anche a testata vuota, per annotare qualcosa al volo. Tutte le altre sezioni si sbloccano a cascata
(1 → 2 → 3 → 4/5).

## Campi obbligatori
Prima di **Genera PDF** l'app verifica i campi essenziali (**Modello, Matricola, Cliente, Commessa,
Collaudatore**): se ne manca qualcuno, mostra l'elenco, evidenzia i campi in rosso e ti porta sul primo.
L'evidenza sparisce appena scrivi. (I campi richiesti sono nell'array `REQUIRED` nel sorgente.)

## Collaudatore e firma
In testata ci sono **Collaudatore** e **Data collaudo**. Nel PDF, in fondo, compare la sezione
**Validazione collaudo** con nome, data e uno spazio per la **firma a penna**.

## Esportazione CSV
Il bottone **📊 CSV** scarica un riepilogo (testata + checklist + prove di taglio) apribile in Excel
(separatore `;`, accenti corretti). Utile per filtrare gli esiti o incollare i dati altrove. Il `.json`
resta comunque la fonte di verità completa (foto incluse).

## Da fare / migliorabile (v3)
- Eventuale condivisione del `.json` su cartella aziendale (se l'IT mette a disposizione M365/SharePoint).
