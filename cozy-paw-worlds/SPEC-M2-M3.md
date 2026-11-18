# Cozy Paw Worlds — Specifica M2 + M3

**Stato: prototipo sperimentale, 18 novembre 2026.** Il progetto non modifica il sito produttivo `cozypawstudio.com`. Le parti in M3 sono la **prima alpha generativa**, non un mondo completo né un prodotto finale.

## Visione e regole di prodotto

- Esperienza **facoltativa**: il sito tradizionale, i libri, Amazon KDP e Color Lab restano raggiungibili senza dover avviare WebGL.
- **Mobile-first**: si parte dal budget di una GPU integrata, poi si scala verso PC più potenti.
- Direzione artistica: **storybook 3D / cozy fantasy**. Il dettaglio è ottenuto con silhouette, colori, vegetazione e composizione, non con post-processing costoso o fotorealismo.
- Nessun asset esterno obbligatorio nel prototipo: codice e geometria originali, shader compatti, niente download di librerie terze al primo avvio.

## M2 — The Little Crossroads, restyling piazzetta

- Piazza centrale stabile, progettata a mano e percorsi chiaramente leggibili.
- Dettagli aggiunti: coperture decorate, bordi in pietra, piante da giardino, fiori, arredi e segnaletica.
- Quattro ingressi: Thais, Micio, Pip, Coral Reef Besties. Il mondo sottomarino ha ora un collegamento diretto al prototipo M3.
- Conservati i controlli touch/desktop, la regolazione dinamica della risoluzione, gli FPS indicativi e il percorso verso il sito pubblico.

## M3 — Coral Reef Besties: La Laguna delle Perle (alpha)

### Generazione

- `seed` numerico in URL: stesso seed + stesse coordinate => stessi posizionamenti **all'interno della stessa versione del generatore**.
- Griglia di **chunk di 27 unità**; la alpha conserva **3 × 3 chunk** attorno alla posizione corrente e rigenera la geometria solo al cambio di chunk.
- Terreno con campionamento di rumore deterministico, senza cuciture tra chunk adiacenti.
- Biomi collegati in modo morbido dal campo di rumore: **Laguna luminosa**, **Giardino dei coralli**, **Foresta delle alghe**.
- Distribuzione guidata di coralli a rami, coralli a tavola, alghe ondeggianti, anemoni, ventagli, rocce e gruppi di pesci.
- Landmark iniziale fisso: **Santuario della Perla**. Serve a dare identità narrativa senza rendere tutto casuale.
- Movimento leggero delle alghe e dei pesci calcolato nella GPU, bolle sintetiche, caustiche simulate e nebbia subacquea.

### Architettura e prestazioni

- **WebGL** (WebGL2, fallback al contesto WebGL1), senza motore o texture esterne: una batch mesh del fondale + una sky pass + una pass di bolle.
- Il generatore compone geometria in CPU **solo sui confini dei chunk**, la trasferisce alla GPU e rilascia il buffer temporaneo.
- Risoluzione adattiva in modalità Auto: varia la scala interna dopo periodi prolungati di rallentamento o margine prestazionale.
- Evitare ombre dinamiche per ogni oggetto, riflessi screen-space, geometrie complesse, grandi texture e luci multiple sul dispositivo mobile.
- Le performance reali **non sono state misurate**: non interpretare gli FPS di una simulazione JavaScript come benchmark GPU.

### Backlog necessario prima di chiamarlo mondo completo

1. Design canonico delle sirenette, personaggi 3D coerenti con i libri e animazioni.
2. Percorsi, landmark aggiuntivi e transizioni bioma più curate con varianti artistiche.
3. Raccolta di perle, obiettivi e piccoli enigmi verificabili, stato di sessione e seed condivisibili.
4. Gestione del dettaglio secondo fascia GPU (non soltanto la risoluzione), frustum culling, telemetria e degradazione termica.
5. Test reali su Android/iOS: FPS, tempi di primo rendering, RAM, consumo, temperatura, orientamento, qualità touch, WebGL1/2 e fallback HTML.
6. Verifica grafica su browser vero e ottimizzazioni dopo misurazioni.
7. Collegamento al sito reale solo dopo approvazione di Katya e Daniele.

## Criteri di accettazione del prossimo test

- Apertura HTTPS senza ZIP né installazione.
- Android: orientamento landscape e portrait; entrata/uscita dalla Laguna; joystick a sinistra, vista trascinabile a destra.
- 3 minuti di navigazione continua senza blocchi né crash; osservare il contatore FPS.
- Provare almeno 2 seed e verificare che il paesaggio cambi; ricaricare un seed per verificare che rimanga coerente.
- Cambiare modalità qualità in Auto/Bassa/Alta; verificare la leggibilità dei tasti e la possibilità di tornare al sito tradizionale.
- **Obiettivi, non garanzie**: 30 FPS minimi su fascia economica e 60 FPS desiderati su fascia media; richiedono misurazioni reali.

## Rischi noti

- Il prototipo M3 è un esperimento originale. La qualità di un intero gioco 3D, personaggi canonici e un mondo proceduralmente ricco richiede ulteriori iterazioni.
- Browser automatico del laboratorio bloccato da policy di navigazione: controlli di sintassi e generazione della scena superati, ma mancano screenshot/render test affidabili.
- L'anteprima usa un URL HTTPS temporaneo su un servizio che serve file GitHub. Non è un deployment ufficiale stabile o l'integrazione del sito produttivo.