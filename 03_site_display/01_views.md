Una View è uno strumento di site building che serve per mostrare un elenco dinamico di contenuti (in realtà di qualsiasi entity), filtrarli, ordinarli e mostrarli in diversi formati. In modo più tecnico possiamo dire che una View permette di costruire una query al database tramite interfaccia grafica, senza scrivere SQL a mano. Ad esempio se sto facendo una vista di contenuti Article, pubblicati, ordinata per data di creazione discendente e limitata a 10 risultati, più o meno sto facendo una query del tipo:
```
SELECT * -- tutti i campi
FROM node_field_data -- è una vista di nodes
WHERE type = 'article' -- i nodes sono di tipo Article
AND status = 1 -- i nodes sono pubblicati
ORDER BY created DESC -- i nodes sono ordinati dal più recente
LIMIT 10; -- prendo solo i primi 10 risultati
```

Vi sono alcune modalità di visualizzazione predefinite (tabella, griglia, unformatted list) ma possono essere installati dei moduli che forniscono altri tipi di visualizzazione.

Rimane sempre la pssibilità di personalizzare il markup della vista con l'appropriato template Twig.

E' possibile visualizzare interi contenuti, anche selezionando un determinato view mode, oppure scegliere i singoli campi.

@TODO fare approfondimento sulle opzioni dei campi (exclude form display, rewrite results, replacement patterns, token ecc...)

L'opzione display invece permette di definire se la vista sarà mostrata come una pagina a sè, un blocco, un feed RSS oppure come attachment in modo che possa essere usata dentro un'altra vista. Un display Page crea una pagina raggiungibile tramite un path da noi dfinito, un display Block produce un blocco che può essere posizionato nelle regioni del tema da Structure > Block layout. Ogni vista può avere più display. 

I contenuti possono essere ordinati in base a diversi criteri: data di creazione o di ultima modifica oppure valore di uno specifico campo.

I filtri limitano i dati visualizzati in base a diversi criteri: stato di pubblicazione, tipo di contenuto, valore di un campo ecc... e possono essere impliciti oppure esposti all'utente. Un filtro normale è configurato dal site builder dentro la View e viene applicato sempre, senza che l'utente possa modificarlo (solo contenuti pubblicati, solo contenuti di tipo Article, solo contenuti in lingua italiana ecc....). Un filtro esposto invece viene mostrato all'utente nel frontend, di solito come campo di ricerca, select, checkbox o altro input, e permette all'utente di filtrare i risultati (filtrare per categoria, parola chiave, data ecc....).

Alcuni filtri sono detti contestuali perchè il loro valore dipende dal contesto, ad esempio l'URL completo della pagina visualizzata, la data o l'ora corrente, o l'utente loggato. Tipicamente i filtri contestuali sono usati per mostrare i contenuti correlati al nodo corrente, ad esempio:
- creo una View di nodi con display Block e filtrata per contenuti pubblicati e del content type interessato
- uso un contextual filter o una relationship per confrontare i termini di tassonomia del nodo corrente con quelli degli altri contenuti, in modo da mostrare contenuti che condividono almeno un tag
- escludo il nodo corrente dai risultati, limito il numero di elementi e li ordino per data o rilevanza
- decido come gestire il caso in cui il nodo corrente non abbia tag oppure non ci siano altri nodi con lo stesso tag
- piazzo il blocco nella pagina del node

Le relazioni permettono di espandere ciò che viene visualizzato nella vista, collegando il contenuto di base visualizzato ad altre entità di contenuto, tipicamente si crea una relazione con l'utente che ha creato il contenuto.

Altre opzioni di configurazione sono la paginazione dei risultati, l'aggiunta di un header e un footer alla vista, la limitazione dell'accesso a determinati ruoli o permessi, la gestione dei casi in cui la vista non ritorna risultati.