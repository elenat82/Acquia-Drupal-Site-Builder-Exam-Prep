Lo schema di numerazione delle versioni del core di Drupal è: Major.Minor.Patch, ad esempio 8 (Major).8(Minor).5(Patch). Il numero di versione principale indica la compatibilità, il numero di versione secondaria indica nuove funzionalità significative e il numero di patch indica correzioni di bug e miglioramenti minori.

Per quanto riguarda i moduli il numero di versione indica la versione del core di Drupal con cui il modulo è compatibile, se si tratta di una versione stabile o di sviluppo e quale specifico "livello di patch" del codice rappresenta, nella forma: CoreCompatibility-Major.PatchLevel[-Extra].
Dalla versione 8 in poi, un modulo compatibile con una certa versione del core potrebbe non essere compatibile con le versioni precedenti del core, mentre invece per la versione 7 un modulo compatibile con una certa versione del core funzionerà anche con le altre.
L'alpha release di un modulo è la prima quindi la meno stabile, poi c'è la beta release in cui sono stati risolti i bugs ma il modulo potrebbe ancora essere modificato, la release candidate è appunto candidata ad essere rilasciata come versione ufficiale .0 del modulo.

Le nuove versioni del core sono rilasciate con un calendario prestbilito:
- Il rilascio di una patch è previsto per il primo mercoledì di ogni mese.
- Il rilascio per motivi di sicurezza è previsto il terzo mercoledì di ogni mese.
- Le uscite minori sono programmate all'incirca ogni sei mesi, di solito il primo o il terzo mercoledì di quel mese.

Per sapere quale versione del core è in uso si può andare alla pagina admin/reports/status, per sapere le versioni dei moduli si può andare ala pagina admin/reports/updates.