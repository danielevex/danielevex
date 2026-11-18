# Cozy Paw Worlds — Sirenette WebGPU V1

Data: 18 novembre 2026. Stato: **anteprima sperimentale**, non pubblicazione finale.

## Obiettivo e implementazione
- Preservare il renderer WebGPU, acqua, luce, fondale, piante e profondità della variante basata su Abyssal Garden.
- Aggiungere **6 figure originali di sirenette stilizzate 3D** generate con primitive geometriche a runtime e animate con WGSL (coda, capelli, galleggiamento).
- Aggiungere **6 santuari/oggetti perla 3D** con shader illuminati, posizionamento variabile tramite seed e una breve missione di raccolta persistita sul dispositivo in localStorage.
- Due draw call per frame aggiuntive, una GPU pipeline e un buffer 341 KB. Geometria aggiuntiva verificata: 8.736 vertici sorgente e 17.472 triangoli instanziati per tutti e sei i personaggi e le sei perle.
- Mostrare l'interazione **Raccogli la perla** se entro 5,5 metri dal punto e permettere F da tastiera.
- Collegare la pagina dalla piazzetta su ramo separato senza modificare il sito pubblico.

## Implementato versus pianificato
Il mondo subacqueo resta derivato da Abyssal Garden (MIT, copyright Maksymilian Dendura 2026), con palette e UI Cozy Paw. La scena **non è ancora un oceano infinito con biomi e grotte costruiti da seed**: nel renderer sorgente il terreno è guidato da set-piece e le decorazioni sono procedurali; in questa versione cambia la distribuzione deterministica di alcuni elementi, e alcuni posizionamenti dei nuovi personaggi/tesori.

L'originalità appena introdotta sono le figure 3D create in questa versione, i santuari perla, la piccola meccanica di raccolta e la presentazione Coral Reef Besties. Le sirenette sono *placeholder stilizzati*, non ancora i personaggi illustrati canonici dei libri.

## Sicurezza e compatibilità
- Non altera cozypawstudio.com.
- Il ramo precedente `cozy-worlds-preview-m1` e il file WebGPU iniziale sono conservati.
- Se la pipeline aggiuntiva fallisce, un try/catch salta i nuovi oggetti e il mondo originale resta navigabile; è previsto messaggio di errore in console.
- La pagina è WebGPU e richiede Chrome/Edge/altro browser che supporti navigator.gpu. Nessun download.
- Non vengono inviati dati della missione a servizi esterni. Le perle raccolte sono salvate localmente, separate per seed.

## Verifiche effettuate
- Entrambi i blocchi JavaScript analizzati senza errori sintattici.
- Shader WGSL verificato staticamente nel sorgente, **non compilato e collaudato sul telefono reale**.
- Generazione CPU delle nuove mesh verificata: nessuna coordinata NaN/Infinity.
- Link nel repository verificato. FPS su Android, rendering del nuovo pipeline ed esperienza touch **non ancora verificati**.

## Prossimi test / sviluppi
1. Avvio WebGPU reale su Android, presentazione almeno di una sirenetta e di una perla.
2. Collezione perle e persistenza dopo il reload.
3. Benchmark vs versione precedente: FPS mediani, 1% low, tempo d'avvio, consumi e memoria.
4. Nuovo terreno procedurale deterministico/chunk e nuove zone davvero originali.
5. Character art canonica, animazioni migliorate, interazioni narrativa e audio.

## Attribuzioni
Base grafica: Abyssal Garden, © 2026 Maksymilian Dendura, licenza MIT. Il file HTML include la licenza MIT. Gli asset 3D aggiunti sono realizzati con geometria generata da codice originale in questa versione.
