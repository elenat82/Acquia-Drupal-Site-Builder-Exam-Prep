Se si sta creando un sito non in inglese, già in fase di installazione è possibile scegliere la lingua che si desidera utilizzare.

La funzionalità multilingua è già fornita dal core senza bisogno di installare moduli aggiuntivi
- modulo Language: consente agli utenti di configurare le lingue
- modulo Locale: consente di tradurre l'interfaccia di Drupal, dei moduli e dei temi (è necessario importare le traduzioni dal server dell traduzioni di Drupal)
- modulo Content translation: consente agli utenti di tradurre le entities
- modulo Config translation: consente di tradurre il testo che fa parte della configurazione, come le etichette dei campi, il testo utilizzato nelle viste ecc...

Quando si traduce un nodo non viene creato un altro nodo nella seconda lingua, ma i singoli campi possono essere tradotti. Una volta designati come traducibili determinati campi e installate almeno due lingue sul sito, è possibile tradurre gli elementi di contenuto. Gli utenti con permessi di traduzione visualizzeranno i link "Traduci" accanto ai link "Modifica" che si trovano normalmente, e potranno aggiungere traduzioni per ciascuna lingua configurata.

Il rilevamento della lingua avviene sulla base della valutazione di una serie di regole, la prima regola che applicata ottiene un risultato positivo viene utilizata. E' possibile definire l'ordine di applicazione delle regole: impostazione nella pagina di amministrazione dell'account, parametro linguistico nell'URL, preferenza dell'utente loggato, lingua del browser utilizzato, lingua selezionata manualmente.
