# Cambio Fornitore — comparatore bollette luce e gas

Web-app (PC e smartphone) per consulenti energia:

1. **Offerte CTE**: carica i PDF/foto delle Condizioni Tecnico Economiche degli operatori. L'app estrae operatore, tipo (luce/gas), segmento (domestico/business/entrambi), prezzo fisso o indice+spread, fasce F1/F2/F3, quota fissa, validità. Si controlla e si salva.
2. **Analizza bolletta**: carica la bolletta del cliente (PDF o foto). L'app riconosce luce/gas (POD/PDR, kWh/Smc), privato/azienda (uso domestico vs altri usi/P.IVA), fornitore attuale (escludendo il distributore), consumi, prezzo e quota fissa.
3. **Confronto**: mostra **solo offerte di operatori diversi dall'attuale** (opzionalmente anche diversi dallo stesso gruppo, es. Enel/SEN, A2A/NeN, Eni/Plenitude), dello stesso tipo e segmento, non scadute, con spesa annua **uguale o minore**.

## Novità
- **Rilevamento automatico privato/business** con punteggio sugli indizi (tipologia d'uso, BTA/MTA, categoria gas C/T, P.IVA o codice fiscale dell'intestatario, forma societaria, potenza, IVA) e grado di certezza.
- **Risparmio medio annuo in %** per ogni offerta e come media delle alternative proponibili.
- **Compensi agente** (opzionale): tabelle provvigionali da PDF/foto/Excel/CSV trasformate in regole (gettone, €/MWh o €/1000 Smc, ricorrente, fasce di consumo). Visibili solo all'agente, mai nel riepilogo per il cliente.

## Calcolo
Si confrontano le voci decise dal venditore: `prezzo × consumo annuo + quota fissa × 12` (+ eventuale quota potenza dell'offerta), IVA inclusa. Trasporto, oneri di sistema e accise sono regolati e uguali per tutti, quindi non cambiano il risparmio. Le offerte variabili usano PUN/PSV impostati in *Impostazioni*.

## Come funziona
- File unico `index.html`, nessun backend. PDF letti con pdf.js nel browser.
- Pubblicata come Artifact claude.ai: la lettura di bollette e CTE usa Claude (anche per foto e scansioni) e le offerte sono salvate in un archivio condiviso tra i dispositivi.
- Aperta fuori da claude.ai funziona in modalità ridotta: lettura a regole (solo PDF con testo) e offerte salvate nel browser locale.

I dati della bolletta del cliente non vengono salvati: restano solo nella pagina aperta.
