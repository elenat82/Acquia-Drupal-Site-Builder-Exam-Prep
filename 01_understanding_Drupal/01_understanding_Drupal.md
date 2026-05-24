@TODO spiegare la differenza tra Drupal e Drupal CMS

## Che differenza c'è tra content type, node, field ed entity?

L'elemento alla base di Drupal è il nodo, cioè un insieme di informaioni correlati, ad esempio quando si crea un nuovo post di un blog, non si definisce solo il testo, ma anche il titolo, il contenuto, il link al profilo dell'autore, la data di creazione, la tassonomia (tag), ecc. 

In Drupal una entity è un oggetto strutturato gestito dal sistema, per esempio un node, un user, un termine di tassonomia, un file o un media.
Un node è un tipo specifico di content entity usato per i contenuti editoriali del sito, come articoli, pagine o news.
Il content type è la configurazione che definisce la struttura di un certo tipo di node: ad esempio il content type “Article” stabilisce quali campi ha un articolo, come titolo, body, immagine, categoria, data, ecc.
Un field è un campo associato a un'entità o a un bundle, e serve a memorizzare un'informazione specifica, per esempio testo, immagine, booleano, riferimento a un'altra entità o data.

## Quando useresti un Paragraph, un Block, un View mode o Layout Builder?

Userei i Paragraph quando ho bisogno di dare agli editor la possibilità di comporre una pagina con componenti strutturati e ripetibili, per esempio testo + immagine, accordion, card, gallery o call to action. Sono utili quando il contenuto ha una struttura flessibile, ma voglio comunque mantenere controllo sui tipi di componenti disponibili.

Userei un Block per contenuti o funzionalità riutilizzabili e posizionabili in aree diverse del sito, per esempio una call to action, un menu contestuale, un box newsletter, un elenco generato da una View o un blocco custom.

Userei un View mode quando lo stesso contenuto deve essere visualizzato in modi diversi a seconda del contesto: per esempio un articolo in versione teaser in una lista, full nella pagina di dettaglio, oppure compact in una card.

Userei Layout Builder quando voglio configurare la struttura visiva di una pagina o di un tipo di contenuto tramite sezioni e blocchi, soprattutto per landing page o pagine dove il site builder/editor deve avere più controllo sulla disposizione degli elementi. NON usare Layout builder automaticamente per tutto, ma solo quando serve flessibilità di composizione del layout.

- Paragraph = struttura interna del contenuto.
- Block = elemento riutilizzabile/posizionabile nella pagina.
- View mode = modo diverso di visualizzare la stessa entità.
- Layout Builder = composizione del layout della pagina con sezioni e blocchi.

## Come faresti un listing di contenuti filtrabile?

Creerei una View sul tipo di entità che devo elencare, per esempio contenuti di tipo Article o News. Aggiungerei un display Page se il listing deve avere una pagina propria, oppure un display Block se deve essere inserito dentro un'altra pagina.
Configurerei i filter criteria, per esempio content type, stato pubblicato, lingua o categoria, e renderei esposti all'utente i filtri che deve poter usare, come ricerca testuale, taxonomy term, data o autore.
Imposterei anche ordinamento, paginazione, campi o view mode da usare per il rendering, e controllerei permessi (accessibile a tutti se è un listing pubblico, oppure limitata per ruolo o permission se espone contenuti gestionali) e cache (@TODO approfondire discorso sulla cache). Se il filtro dipende dal contesto della pagina, valuterei un contextual filter invece di un filtro esposto.

## Come porteresti una modifica di configurazione da locale a staging?

Porterei la modifica usando il Configuration Management di Drupal. In locale farei la modifica, per esempio un nuovo campo, una View o una configurazione di un content type. Poi esporterei la configurazione in YAML, la versionerei nel repository Git, farei commit/pull request e la porterei su staging con il deploy del codice. Su staging importerei la configurazione e verificherei che la modifica funzioni correttamente. Prima di importare controllerei il git diff.

- drush config: export (sull'ambiente di sviluppo esporta la configurazione nella directory di sync)
- drush config: import (sull'ambiente di staging importa nel database Drupal la configurazione presente nei file YAML della config directory)

Esempio pratico: aggiunta di un campo subtitle al content type Article:

In ambiente locale:
- git checkout -b feature/article-subtitle
- git pull origin develop
- composer install (perchè dopo il pull potrebbero essere variati i files composer.json e composer.lock)
- drush updatedb (per applicare eventuali update del db definiti da Drupal core o dai moduli, si può anche fare prima drush updatedb:status)
- drush config:import
- drush cr
- fare l'aggiunta del campo nel content type
- drush config:export
- git status
- git diff
- git add config/sync
- git commit -m "Aggiunto campo subtitle su content type Article"
- git push origin feature/article-subtitle

In ambiente di staging:
- git pull origin develop
- composer install --no-dev (per evitare di installare pacchetti necessari solo allo sviluppo)
- drush updatedb
- drush config:import
- drush cr

## Come crei un modulo custom minimale?

Per creare un modulo custom minimale potrei usare drush generate per generare il boilerplate, oppure crearlo manualmente in modules/custom. Il minimo indispensabile è una cartella con il machine name del modulo e un file .info.yml, che permette a Drupal di riconoscere il modulo. Poi, a seconda della funzionalità, aggiungerei altri file: per esempio un .routing.yml e un controller se devo creare una pagina custom, un plugin se devo creare un blocco, oppure un .module se devo implementare degli hook. Il file .info.yml è essenziale perché comunica a Drupal l'esistenza del modulo e contiene metadati come nome, tipo e compatibilità con la versione di core.
Dopo la creazione del modulo questo deve essere attivato con drush en nome_del_modulo e drush cr.
- .routing.yml e controller: il file di routing dice a Drupal: quando arriva questo URL esegui questo codice, nel controller viene definito il codice da eseguire
- plugin: per creare blocchi custom (@TODO approfondire block plugin e questione dependency injection)

## Come definisci una route e un controller?

Definisco una route nel file nome_modulo.routing.yml. In quella route indico un nome macchina, il path, cioè l'URL, i defaults, tra cui il controller da chiamare e il titolo della pagina, e i requirements, per esempio il permesso necessario per accedere.
Il controller è una classe PHP, di solito in src/Controller, con un metodo che viene richiamato dalla route e che restituisce una risposta, spesso un render array. Dopo aver aggiunto o modificato una route, fare sempre un drush cr.

## Come crei un blocco custom?

Dipende dal tipo di blocco. Se devo mostrare una lista di contenuti, userei una View con display Block e poi posizionerei il blocco nella region desiderata da Structure > Block layout, configurando eventualmente le condizioni di visibilità.
Se devo creare un contenuto statico gestibile da editor, tipo box testo/immagine, creerei un custom block dalla UI di Drupal.
Se invece devo creare un blocco custom da codice, creerei un Block plugin in un modulo custom, dentro src/Plugin/Block, estendendo BlockBase. Nel metodo build() restituirei un render array. Dopo un cache rebuild, il blocco comparirebbe nella UI "Place block" e potrei posizionarlo nelle regioni del tema.

## Come alleghi CSS e JS in un tema Drupal?

In Drupal CSS e JS non vengono caricati automaticamente ovunque, ma devono essere definiti come librerie e poi agganciati dove servono, anche per motivi di performance.
In nome_tema.libraries.yml vengono definite le librerie CSS e JS, in nome_tema.info.yml vngono indicate le librerie da agganciare globalmente al tema, per caricarle su tutte le pagine.
Se invece si vuole agganciare in un template si può usare {{ attach_library('nme_tema/nome_file') }}

## Come fai override di un template Twig?

Per fare override di un template Twig, prima individuo il template di base e le template suggestions disponibili, di solito abilitando Twig debug in ambiente locale. Poi copio il template nel mio tema custom, rispettando la struttura/naming suggerita. Per esempio, per tutti i node posso usare node.html.twig, per il content type Article posso usare node--article.html.twi,; per Article in view mode Teaser posso usare node--article--teaser.html.twig. Dopo aver aggiunto o modificato il template fare sempre drush cr.
E' possibile abilitare il Twig debug, cioè dei suggerimenti nel file html che indicano i template disponibili e quello che è in uso al momento, da Administration > Configuration > Development settings oppure impostando twig.config.debug: true.

## Cosa sono cache tags, cache contexts e max-age?

https://www.drupal.org/docs/develop/drupal-apis/cache-api

## Differenza tra configurazione e contenuto?

La configurazione riguarda la struttura e il comportamento del sito: content type, fields, views, form display, view mode, ruoli, permessi, image style, configurazioni dei moduli, ecc. È qualcosa che posso esportare in YAML, versionare con Git e portare da locale a staging e produzione tramite Configuration Management.
Il contenuto invece sono i dati editoriali veri e propri: node, testi, immagini, media, termini di tassonomia usati editorialmente, utenti, commenti, ecc. In sviluppo posso usare contenuti fittizi o placeholder tipo lorem ipsum, mentre in produzione saranno gli editor a gestire i contenuti reali.
Alcune cose sono un po' ibride dal punto di vista pratico: per esempio taxonomy terms o menu link possono essere usati come struttura del sito, ma spesso sono trattati come contenuto e quindi non rientrano automaticamente nel classico export/import della configurazione (@TODO approfondire modulo Content as Configuration).

## Come gestiresti un bug su un sito Drupal che non conosci?

Farei prima queste queste domande:
- hai provato a cancellare la cache?
- il bug è solo in prod o anche negli ambienti inferiori?
- si verifica per tutti gli utenti o solo alcuni (oppure solo alcuni ruoli)?
- si verifica con tutti i browser? sia da desktop che da mobile?
- nei log c'è qualche informazione utile?
- quali sono gli ultimi commit?

Casi possibili:
- pagina 403 non prevista: verificare prmessi, ruoli e access control
- pagina 404 non prevista: verificare path alias, contenuti non pubblicati, se il sito è multilingua potrebbe mancare la traduzione
- un blocco non compare: verificare condizioni di visibiità del blocco
- una view mostra risultati sbagliati: verificare contextual filters, relationships
- un campo non appare: verificare view mode, field formatter, Twig override
- layout rotto: verificare template Twig, librerie CSS/JS e hook preprocess
- errore dopo deploy: verificare config import, drush updatedb, composer.json e composer.lock

Una volta trovato il problema:
- eseguire fix puntuale
- test test test!!!
- verificare di non aver introdotto regressioni
- commit con spiegazione di cosa è successo

## Come valuti se usare un modulo contrib o sviluppare custom?

Prima valuterei se il requisito può essere soddisfatto con Drupal core o con configurazione, senza aggiungere nuovo codice.
Se serve una funzionalità non coperta dal core, cercherei un modulo contrib. Guarderei se è compatibile con la mia versione del core, se ha passato il controllo di sicurezza, se ha tante issue aperte e in base a queste informazioni valuto.
Poi valuterei quanto il modulo risponde davvero al requisito: se copre bene il caso d'uso ed è mantenuto allora lo uso, se invece introduce troppa complessità, è poco mantenuto o richiede molte alterazioni, valuterei una soluzione custom più piccola.

## Come controlli la sicurezza di un sito Drupal?

- verificare che il core e i moduli siano aggiornati
- verificare ruoli e permessi (chi ha i permessi di admin? chi può creare nuovi utenti? chi può usare Full HTML nel CKEditor? chi può fare upload dei files?)
- verificare policy password corretta, magari 2FA per ruoli admin, protezione dei form con Honeypot, permessi di files e cartelle sul server
- lanciare composer audit per verificare vulnerabilità note nelle dipendenze PHP
- verificare file settings.php: non deve essere modificabile, deve indicare trusted host patterns
- verificare che funzioni il backup
