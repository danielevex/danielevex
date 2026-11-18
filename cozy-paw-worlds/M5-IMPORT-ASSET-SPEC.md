# Cozy Paw Worlds — Milestone 5: import di un vero asset 3D di sirenetta

Stato: **prototipo di importazione WebGPU, non modello già integrato** (18 novembre 2026).

## Modello scelto e diritti
- Autore: **xidingart**
- Opera: [Cute Mermaid](https://sketchfab.com/3d-models/cute-mermaid-56374592aeac491387159c67a48c917c)
- Licenza: **[Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/)**.
- Sketchfab indica circa **15.800 triangoli**.
- L'autore contrassegna il modello **NoAI**: il file non deve essere inserito in dataset o input di modelli AI generativi. La presente pipeline importa/renderizza tradizionalmente glTF e non invia il modello ad alcuna IA generativa.
- Nel progetto definitivo, rispettare attribuzione, link e dichiarazione delle modifiche estetiche. Non presentare il modello come originalmente realizzato da Cozy Paw Studio.

## Perché il modello non è già visibile
Lo strumento ufficiale di download Sketchfab richiede l'accesso di un utente autenticato. L'accesso pubblico alla pagina e all'anteprima **non** concede un URL del file GLB pronto per integrarsi nel gioco. Non è stato effettuato alcun download non autorizzato né estratta la mesh dal visualizzatore.

## Consegna M5
- Anteprima `cozy-paw-worlds/mermaid-asset-m5.html` sul ramo `cozy-worlds-m5-asset-import`.
- Importazione manuale tramite file locale **GLB 2.0**, **ZIP glTF ufficiale** (inclusi buffer e texture) e **glTF** con risorse incorporate.
- Lo ZIP viene decompresso dal browser mediante `DecompressionStream('deflate-raw')` — senza estrazione manuale. Limiti preventivi per dimensione/memoria.
- Il modello viene convertito in mesh WebGPU nella **stessa scena**, con depth test, nebbia e illuminazione coerenti con la Laguna. Un import fallito non sostituisce il fondale con un pupazzo.
- Lettura di mesh triangolari, gerarchia glTF, normali, UV, baseColorFactor, texture diffuse; ridimensionamento e centratura all'altezza di ~3,6 unità.
- Comandi tocco: **Seguimi, Aspetta, Gioca, Ruota 180°**. La posa al momento è quella di default glTF; movimento e oscillazione subacquea sono proceduralmente applicati in shader.

## Limiti NON risolti
- Il file originale `Cute Mermaid` **non è ancora stato scaricato/importato né collaudato**; serve l'archivio ottenuto legalmente.
- Animazioni scheletriche, morph, texture PBR complete, materiali traslucidi speciali e compressione Draco/Meshopt **non ancora supportati**; serve un GLB o ZIP glTF non compresso in quei formati.
- Le animazioni originali dell'eventuale rig non sono riprodotte; la sirenetta è un modello completo ma si muove mediante traslazioni e deformazione semplice della parte inferiore. Rig completo si implementerà dopo aver ispezionato l'asset reale.
- Il modello importato viene conservato **solo nella RAM del browser** durante la sessione: ricaricando la pagina è necessario reimportarlo. L'archivio dell'utente non viene inviato a server terzi.
- Nessuna dichiarazione di FPS reali su Android, fedeltà all'illustrazione o prova video finché non confermata dall'utente.
- Rigging di Cute Mermaid sconosciuto: va verificato al momento dell'importazione.
- Programmazione del caricatore è originale; world renderer sottostante deriva da Abyssal Garden © Maksymilian Dendura, MIT, attribuito nell'HTML.

## Collaudi
1. Parser JS: sintassi verificata.
2. Test semantico GLB costruito con fixture triangolare: importato 1 triangolo e dati finiti.
3. ZIP standard con `scene.gltf` e `mesh.bin` testato: 1 triangolo.
4. Non ancora collaudati: ZIP compresso deflate con Safari/Android, compilazione WebGPU importer, file Sketchfab vero, texture e performance.
5. Dopo upload dell'archivio Sketchfab: ispezionare glTF (skin, animations, extensions, bufferViews), aggiornare supporto, esportare GLB ottimizzato, pubblicarlo con attribuzione e testare animazione e interazione.

## Passaggi per l'utente
1. Aprire il modello [Cute Mermaid](https://sketchfab.com/3d-models/cute-mermaid-56374592aeac491387159c67a48c917c) e accedere a Sketchfab.
2. Scegliere **Download 3D Model** e preferire **glTF**. Scaricare l'archivio ufficiale.
3. Aprire la pagina M5 nel browser sullo smartphone e premere **Importa il modello 3D**: selezionare l'archivio direttamente, senza estrarlo.
4. In alternativa, allegare l'archivio scaricato in ChatGPT per ottimizzazione/integrazione definitiva su GitHub con attribuzione.
