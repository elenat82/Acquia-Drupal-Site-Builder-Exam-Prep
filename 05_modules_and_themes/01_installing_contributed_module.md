@TODO spiegare differenza tra hook ed eventi

Il metodo consigliato per aggiungere un modulo è tramite [Composer](https://getcomposer.org/doc/01-basic-usage.md), soprattutto per i moduli che hanno dipendenze. Diversi moduli non funzioneranno se si aggiunge solo il file zip/tar.gz.

Per scaricare un modulo contrib insieme alle sue dipendenze, andare alla pagina del progetto e copiare il comando Composer sotto "Releases", ad esempio per il modulo Admin Toolbar: composer require drupal/admin_toolbar.

Eseguire il comando dalla riga di comando, una volta completato il comando, verrà visualizzato un messaggio che indica che il modulo è stato aggiunto al file composer.json del progetto come dipendenza e che il codice correlato è stato scaricato.

Per attivare il modulo usare Drush con il comando drush install admin_toolbar.

Per motivi di sicurezza, i permessi non vengono inizialmente installati, dopo l'aggiunta di un nuovo modulo, per nessun utente tranne l'amministratore.

Drupal cercherà i moduli in diverse posizioni: la directory principale /modules (preferibile) o qualsiasi directory /sites/*/modules . All'interno di queste posizioni, Drupal analizzerà ricorsivamente tutte le sottodirectory alla ricerca dei moduli.

Una pratica comune è quella di aggiungere tutti i moduli scaricati da Drupal.org alla directory /modules/contrib e tutti i moduli contenenti codice personalizzato specifico del progetto alla directory /modules/custom.

## Composer

Per iniziare a usare Composer nel tuo progetto, ti basta un file composer.json. Questo file descrive le dipendenze del tuo progetto e può contenere anche altri metadati. In genere, dovrebbe trovarsi nella directory principale del tuo progetto.

La prima cosa che specifichi nel composer.json è la chiave require. Stai dicendo a Composer da quali pacchetti dipende il tuo progetto. La chiave require accetta un oggetto che mappa i nomi dei pacchetti ai vincoli di versione. Il nome del pacchetto è composto dal nome del fornitore e dal nome del progetto, spesso questi due nomi coincidono, il nome del fornitore serve solo a evitare conflitti di denominazione.

Nel file composer.lock sono specificate le specifiche versioni dei pacchetti in modo che in fase di deploy vengano installate le versioni corrette.

Il comando install permette di scaricare nella cartella vendor del progetto i pacchetti specificati nel file composer.lock (o in altre cartelle specificate nella chiave installer-paths del file composer.json, ad esempio web/modules/contrib o web/themes/contrib). Esiste anche il comando update che aggiorna le dipendenze alla versione più recente compatibile con i vincoli di composer.json e modifica composer.lock, quindi in deploy o in produzione si usa composer install, in sviluppo si usa composer update.

Composer può anche creare da zero un progetto Drupal con il comando composer create-project drupal/nome-template nome-progetto.

Per installare un modulo tramite Composer:
- composer require drupal/nome_modulo
- drush en nome_modulo
- drush cr

Per disinstallare un modulo:
- drush pm:uninstall nome_modulo (pm è un namespace che sta per Project Manager)
- composer remove drupal/nome_modulo
- drush cr

Per aggiornare un modulo:
- composer update drupal/nome_modulo --with-all-dependencies
- drush updb
- drush cr

Per aggiornare il core (ma non si intende da Drupal 10 a Drupal 11, si intendono i pacchetti):
- composer update "drupal/core-*" --with-all-dependencies
- drush updb
- drush cr

Significati dei simboli nei numeri di versione:
- ^1.2.3      dalla 1.2.3 in su ma meno della 2.0.0
- ~1.2.3      dalla 1.2.3 in su ma meno della 1.3.0
- 1.2.*       dalla 1.2.0 ma meno della 1.3.0

Altri comandi utili:
- composer show --> pr vedere cosa è installato
- composer show "drupal/*" --> per vedere solo i pacchetti relativi a Drupal
- composer outdated --> per vedere quali pacchetti hanno aggiornamenti disponibili
- composer diagnose --> per verificare se ci sono problemi
- composer audit --> per verificare vulnerabilità note

Se si riceve l'errore "Your requirements could not be resolved" significa che i vincoli di versione sono incompatibili, ad esempio un modulo contrib non è compatibile con la versione core, in quel caso si possono usare i comandi:
- composer why-not nome_pacchetto versione
- composer prohibits nome_pacchetto versione
- composer update nome_pacchetto --with-all-dependencies

Se si riceve l'errore "Package not found" significa che il pacchetto richiesto non è stato trovato, magari perchè si è digitato male il nome.

Se si riceve l'errore "Plugin blocked by allow-plugins" significa che Composer ha bloccato l'esecuzione di un plugin non ancora autorizzato nella configurazione allow-plugins.