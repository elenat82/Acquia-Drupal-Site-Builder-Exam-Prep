 Il Configuration Management System è il sistema che permette di esportare, versionare e importare la configurazione del sito in file YAML. In questo modo le opzioni di configurazione non sono più nel database ma sono in un file testuale tracciato su Git.
 
 La sync directory si configura nel file settings.php mentre nel file settings.local.php è possibile sovrascrivere valori di configurazione a runtime senza modificare il db, utile per differenziare tra ambienti. Questi override non vengono esportati con drush config:export. Il modulo Config Split permette di avere configurazioni diverse per ambiente, ad esempio potrei volere il modulo Devel attivo solo negli ambienti di sviluppo.

 **Attenzione**: quando si fa config:import, se qualcosa che è presente nella mia configurazione attiva (solo nella tabella config) non è presente nel file YAML, verrà eliminata senza avvertimenti preventivi, quindi meglio fare sempre prima drush config:status.

 Per evitare rischi prima di importare config da un altro ambiente, esportare la prpria config attiva e controllare le differenze con Git.

 Fare anche un dump del database per uteriore sicurezza.

 Usare il modulo Environment indicator per avere un indicatore visivo dell'ambiente in cui ci si trova.