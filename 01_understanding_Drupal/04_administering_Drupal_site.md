L'Utente 1 ha tutti i prvilegi per la gestione del sito, quindi è preferibile creare account separati per ogni utente amministratore, assegnando loro il ruolo di Amministratore, piuttosto che far accedere tutti gli utenti amministrativi con l'account Utente 1.
E' possibile installare il modulo [Paranoia](https://www.drupal.org/project/paranoia) per disabilitare l'editing dell'Utente 1.

## Checklist per il lancio del sito

### Sicurezza
- Verificare che il core e i moduli sino aggiornati
- Abilitare il modulo Gestione aggiornamenti e configuralo assicurandosi di utilizzare un indirizzo email reale e non un indirizzo di prova
- Controllare il report sullo stato e assicurarsi che non ci siano avvisi o errori
- Controllare i log per individuare errori e avvisi, come file o URL mancanti
- Verificare che la password dell'amministratore sia sicura
- Disattivare la segnalazione degli errori a schermo
- Verificare le autorizzazioni per gli utenti anonimi e autenticati
- Verificare che le impostazioni di creazione dell'account siano configurate come desiderato (gli utenti possono creare i propri account o necessitano di approvazione?)
- Installare moduli aggiuntivi per audit di sicurezza (@TODO stilare lista)
- Controllare permessi di files e cartelle (@TODO approfondire)

### Prestazioni
-  Impostare "Età massima della cache del browser e del proxy" su un intervallo di tempo che funzioni correttamente e verificare che le viste siano memorizzate nella cache
-  Abilitare "Aggrega e comprimi i file CSS" e "Aggrega i file JavaScript"
- Installare il modulo [Webprofiler](https://www.drupal.org/project/webprofiler) per verificare le prestazioni
- Disinstallare i moduli di sviluppo come Devel

### Interazione con l'utente
- Verificare di avere protetto i form aperti agli utenti anonimi con moduli come [Honeypot](https://www.drupal.org/project/honeypot) o [CAPTCHA](https://www.drupal.org/project/captcha)
- Verificare che gli indirizzi email esposti siano offuscati con il modulo [Obfuscate Email](https://www.drupal.org/project/obfuscate_email)
- Verificare gli indirizzi email nei moduli che inviano notifiche
- Verificare il testo dei messaggi email generati dal tuo sito

### Dominio
- Verificare che funzioni sia l'indirizzo con www che senza
- Aggiornare le chiavi API per i moduli che le utilizzano

### Backup, manutenzione e monitoraggio
- Impostare backup automatici del db
- Impostare monitoraggio del sito e delle sue prestazioni

### SEO e indicizzazione
- Verificare di avere creato la sitemap con il modulo [Simple XML Sitemap](https://www.drupal.org/project/simple_sitemap)
- Verificare canonical link, metatag e description
- Verificare l'attributo hreflang se il sito è multilingue
- Verificare l'anteprima delle OpenGraph/Twitter Cards
- Verificare che l'indice di ricerca sia aggiornato e al 100%.

### Qualità
- Rimuovere i contenuti di prova, come il testo "lorem ipsum", gli utenti fittizi o i contenuti generati dal modulo Devel