# Cozy Paw Worlds — M4: Sirenetta Viola, primo personaggio 3D reale

Data: 18 novembre 2026. Stato: **prototipo originale sperimentale** da collaudare sullo smartphone.

## Fonte visiva e licenze
Riferimento: retrocopertina «Explore. Color. Find. Have Fun!», presente nella libreria Cozy Paw dell'utente. Il prototipo reinterpreta **la sirenetta dai capelli viola con stella marina rosa**, grandi occhi turchesi, conchiglie rosa e coda rosa. Non sono disponibili tavole ortografiche né turntable approvati: il modello NON può essere dichiarato identico al personaggio canonico da ogni angolazione.
Il motore sottomarino deriva da Abyssal Garden di Maksymilian Dendura, con licenza MIT conservata nella pagina HTML. Geometria del personaggio, shader, animazioni e controlli aggiunti in questa M4 sono implementazione originale.

## Architettura
- Mesh completa **3D** generata proceduralmente in JavaScript al caricamento; non è un billboard.
- 50.448 vertici non indicizzati (16.816 triangoli); ~1,93 MiB per il buffer vertex RGBA normale/colore/flag. 1 draw call per istanza.
- Un solo personaggio instanziato, materiali a colori per-vertice e illuminazione/fog WGSL nello stesso pass HDR WebGPU del fondale.
- Coda, pinne e boccoli animati nel vertex shader; comportamento di galleggiamento.
- Movimento con easing e target relativi alla camera:
  * Seguimi: rimane avanti, leggermente a destra, per essere visibile in prima persona
  * Aspetta: mantiene la posizione acquisita
  * Gioca: percorre un piccolo giro attorno al giocatore
  * Saluta: messaggio breve
- Orientamento geometrico reale verso la camera. Depth test e depth write attivi per integrarsi con rocce e piante.
- Nessun download di modelli, nessun frame di animazione immagine e nessun motore aggiuntivo.

## Controlli eseguiti
- Parsing JavaScript dei due script HTML: superato.
- Generazione CPU del modello: 50.448 vertici, 16.816 triangoli; coordinate finite e limiti della geometria rispettati.
- Controllo della presenza di un unico pass addizionale e di un solo personaggio: superato.
- Link GitHub e ramo separato: verificati.
- **Non eseguiti**: compilazione dello shader WGSL in browser reale, test visivo Android, misure FPS, test GPU mobile, raffronto dettagliato e approvazione canonica. Non promettere qualità finale o assenza di bug.

## Criteri di accettazione
1. Avvio in Chrome Android e presenza del personaggio con coda, capelli, occhi e conchiglie.
2. Ruotando la visuale il personaggio cambia prospettiva: nessun billboard.
3. La coda oscilla e capelli si muovono.
4. Seguimi / Aspetta / Gioca devono funzionare con touchscreen.
5. Fondale, mante e pesci come nella precedente Laguna WebGPU.
6. FPS raccolti sullo stesso dispositivo con FPS indicator; benchmark confrontabile con la Laguna senza personaggio.
7. Confronto con illustrazioni del libro: proporzioni e accessori da approvare/rifinire. Non creare altri personaggi finché questo non è verificato.

## Pubblicazione
Ramo isolato `cozy-worlds-mermaid3d-m4`. File `cozy-paw-worlds/mermaid3d-m4.html`. Il sito pubblico `cozypawstudio.com` non è alterato.
