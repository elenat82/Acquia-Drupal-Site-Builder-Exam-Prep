Nei tempate Twig tutto ciò che è racchiuso tra {{}} è automaticamente sanificato, quando si tratta di attributi è consigliato racchiuderli tra virogolette, quindi class="{{ class }}".

Per sanitizzare le stringhe nei moduli si possono usare la funzione t() oppure Html::escape(), Xss::filter(), o Xss::filterAdmin().

Nell'ambito del frontend si può usare Drupal.checkPlain() per sanitizzare la stringa.

Nell'ambito della costruzione di una query è necessario sanitizzare le variabili che verranno utilizzate nella where.

## Configurazioni di sicurezza

- non pemettere agli utenti anonimi di creare account e richiedere sempre la verifica dell'indirizzo email
- mettere in sicurezza lo User 1
- fare periodicamente check sui vari ruoli verificando che abbiano solo i permessi necessari e restringere l'accesso alla pagina di assegnazione dei permessi
- installare subito gli aggiornamenti di sicurezza
- disabilitare il modulo Simpletest e in generale i moduli che servono solo per lo sviluppo
- concedere Full HTML solo agli utenti fidati e non concedere agli utenti anonimi troppi tag
- non abilitare l'opzione di assegnare all'utente anonimo i contenuti creati da uno user cancellato
- rimuovere i messaggi di errore perchè potrebbero fornire informazioni come path del filesystem e struttura delle tabelle
- in alcuni casi può essere utile consentire l'accesso solo da determinati indirizzi IP (modulo Restrict Login or Role Access by IP Address)
- moduli utili per la gestione delle password: Password Strength, Password Expire, Password Policy, Restrict Password Change, Login Security
- non scrivere direttamente API keys nel file settings.php ma tenerle in un file esterno e recuperarle con file_get_contents('file.txt')
- moduli utili per session management: Session Limit, Auto Log Out, Persistent Login, User Session Management and Monitoring

@TODO approfondimento sui metodi di login

