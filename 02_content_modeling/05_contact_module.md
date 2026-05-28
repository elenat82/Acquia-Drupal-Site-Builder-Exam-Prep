Con il modulo core Contact è possibile inserire nel sito dei form di contatto, sia site-wide (ad esempio in una pagina Contatti) sia per contatare un altro utente registrato. I form site-wide inviano email a indirizzi configurati, mentre i form personali permettono agli utenti di contattarsi mantenendo nascosto l'indirizzo email finché il destinatario non risponde.

Il Contact form è una configuration entity (quindi esportabile) e posso definire configurazioni come id, labels, destinatari, auto-reply, messaggio, redirect e campi.
Il Contact message è una content entity usata per rappresentare il messaggio inviato. Ha campi base come nome del mittente email del mittente, subject, message, opzione "send copy to sender" ed eventuale recipient per i form personali.
Questi campi sono definiti nel core nella classe Message.

Quando un utente invia il form, Drupal crea un contact message e lo passa al sistema mail.

Se però è necessario raccogliere le submissions sarebbe meglio usare Webform perchè il modulo Contact non le salva, a meno che non si aggiunga il modulo Contact Storage.

In ogni caso è necessario configurare i parametri per l'invio SMTP (metterli nel file settings.php).

Avere un form nel sito comporta tutta la parte di gestione della privacy: link all'informativa completa di tutti i dati sul trattamento, checkbox "Dichiaro di aver preso visione dell'informativa privacy", verificare di raccogliere solo i dati minimi necessari e per il tempo necessario (cancellazione periodica delle submissions), verificare i ruoli che hanno accesso alle submissions.

Checklist GDPR:
- Quali dati vengono raccolti? 
    - art. 4 Definizioni --> per verificare se i dati che stiamo raccogliendo sono considerati personali
- Per quale finalità vengono raccolti? 
    - art. 5 Principi del trattamento --> raccogliere solo i dati necessari, conservarli per un tempo definito e proteggerli. 
    - art. 6 Base giuridica --> Per un form contatti spesso non serve "consenso" specifico, se la finalità è rispondere a una richiesta può bastare una base diversa, da valutare caso per caso. 
    - art. 21 Opposizione --> Rilevante soprattutto se la base giuridica è il legittimo interesse o se il form è collegato a marketing diretto.
    - art. 18 Limitazione del trattamento --> L'utente può chiedere di limitare l'uso dei dati in certi casi
- L'informativa è visibile e comprensibile?
    - art. 12 Trasparenza e modalità di comunicazione --> L'informativa deve essere chiara, comprensibile e facilmente accessibile
    - art. 13 Informazioni da fornire quando i dati sono raccolti presso l'interessato --> dato che è l'utente che compila direttamente il form, bisogna informarlo su titolare, finalità, base giuridica, destinatari, conservazione, diritti, reclamo, ecc...
- Serve consenso separato o basta informativa?
    - art. 7 Condizioni del consenso --> Il consenso, se è richiesto coma base giuridica, ad esempio per finalità di marketing, deve essere dimostrabile, libero, specifico, informato e revocabile
- I dati vengono salvati nel database o solo inviati via email?
    - art. 15 Diritto di accesso --> L'utente può chiedere quali dati sono conservati su di lui, quindi se le submissions vengono salvate nel database, devono essere recuperabili
    - art. 16 Rettifica --> L'utente può chiedere correzione dei dati inesatti
    - art. 17 Cancellazione --> L'utente può chiedere la cancellazione dei suoi dati (salvo obblighi o basi che giustifichino la conservazione)
- Chi può accedere alle submission o alla mailbox?
    - art. 28 Responsabili del trattamento --> Verificare chi è designato come responsabile del trattamento
    - art. 24 Responsabilità del titolare --> Il titolare deve poter dimostrare di aver adottato misure adeguate
    - art. 25 Privacy by design e by default --> Evitare checkbox marketing preselezionate,  campi inutili, salvataggio a tempo indefinito
- Ci sono provider terzi, per esempio SMTP, hosting, CRM, antispam?
    - art. 44 Principio generale sui trasferimenti --> Rilevante se i dati del form vanno fuori dall'UE, per esempio tramite provider email, hosting o antispam extra UE
- Il form è protetto da HTTPS, anti-spam e permessi corretti?
    - art. 32 Sicurezza del trattamento --> HTTPS, accessi limitati, permessi corretti, protezione SMTP, backup sicuri, log, aggiornamenti, anti-spam, protezione da accessi non autorizzati
- Esiste una procedura in caso di data breach?
    - art. 33 Notifica data breach all'autorità --> Se le submission del form o la mailbox vengono compromesse, può esserci obbligo di notifica al Garante entro i termini previsti.
    - art. 34 Comunicazione data breach agli interessati --> Se il breach comporta rischio elevato per gli utenti, può essere necessario comunicarlo anche agli interessati


Sul lato della sicurezza è importante verificare che l'area del messaggio non abbia Full HTML abilitato e che il form abbia una protezione anti-spam.