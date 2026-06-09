Nel form di creazione del content type è possibile selezionare alcune opzioni come:
- Published: per specificare se i contenuti di questo content type devono essere pubblicati di default
- Promoted to front page: per specificare se i contenuti devono essere mostrati nella home page
- Sticky at top of lists: per specificare se i contenuti dvono essere mostrati all'inizio di una lista
- Create new revision: per specificare se i contenuti devono memorizzare le versioni precedenti ogni volta che il contenuto viene modificato
- Display author and date information: per specificare se devono essere mostrati autore e data dei contenuti
- Available menus: per specificare i menu a cui è possibile aggiungere i contenuti

Vi sono alcuni tipi di campi predefiniti che possono essere usati per la costruzione di un content type: Plain Text, Formatted Text, Number, Reference, File upload, Selection list, Date and time, Boolean, Comments, Email e Link. E' possibile installare dei moduli che permettono di estendere la funzionalità di aggiunta dei campi, ad esempio: Field Group, Conditional Fields, Inline Entity Form.

I campi di tipo Reference rappresentano una relazione tra un'entità e una o più altre entità, che possono appartenere allo stesso tipo o a tipi diversi. I tre campi di riferimento più comunemente utilizzati sono Content Reference, Tanonomy term e User.

I termini di tassonomia sono utilizzati per classificare i contenuti di un sito web e possono essere organizzati in diversi vocabolari.

Per i campi immagine è possibile impostare diversi tipi di visualizzazione, ritagliando e/o ridimensionando l'immagine di partenza.

Per i campi testuali è possibile impostare diversi formati di testo, composti da una serie di filtri , ognuno dei quali trasforma il testo. Quando gli utenti creano contenuti, a questi viene associato un formato di testo e il testo originale completo viene memorizzato nel database. Il contenuto viene quindi elaborato dai filtri nel formato di testo prima di essere visualizzato sul sito. A ciascun formato di testo è associato un permesso, in modo da poter consentire l'utilizzo dei formati di testo permissivi solo agli utenti attendibili riducendo il rischio di cross-site scripting (XSS).