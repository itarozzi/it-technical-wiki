# it-technical-wiki

## Introduzione
Ho spesso la necessità di appuntarmi procedure, annotare cose e crearmi mini-documentazione.

Ho provato nel tempo vari strumenti, sia offline che online, ma non sono mai riuscito a trovare lo strumento perfetto che coniughi velocità nell'editing con la disponibilità online. E che permetta di trovare facilmente quello che cerco.

Per uso privato utilizzo da tempo DokuWiki, del quale ho installato un'instanza nel mio server casalingo (su virtual machine).
Accedere però a tale wiki (e soprattutto editare i contenuti) dal di fuori della mia LAN casalinga risulta lento.

Ho quindi pensato di sperimentare questa "nuova" modalità, per i contenuti tecnici lavorativi, e magari se funziona lo utilizzerò anche per altro.

Siccome Dokuwiki non utilizza un DB per i contenuti ma dei semplici file di testo, ho deciso (anche ispirato da alcuni tutorial e blog) di creare un repository su github contenente le pagine del wiki (e i media) e poi utilizzare delle istanze locali di dokuwiki sui PC dove lavoro, sincronizzate con esso.
Questo si traduce nel vantaggio di avere un editing piuttosto veloce (su localhost), un frontend piuttosto piacevole (soprattutto utilizzando il template bootstrap) e un sistema di ricerca abbastanza efficiente.

Per le istanze locali utilizzo *docker*, che permette di rendere le installazioni di Dokuwiki semplici e riproducibili.

## Sincronizzazione via GIT
Per i commit e i push/pull verso github inizialmente ho provato il plugin Gitbacked, la cui configurazione è documentata all'interno del wiki stesso.
Però ho avuto diversi problemi (forse legati alla configurazione del plugin o al fatto che sull'immagine docker le directory di lavoro sono link ad uno storage diverso), e non avendo molto tempo per indagare ho adottato una strada differente.

Ho quindi creato una directory nella mia home contenente le sotto-directory pages e media. 

Poi ho fatto in modo di fare utilizzare tali directory all'istanza di docker che realizza il server dokuwiki. In questo modo, docker monta le directory del mio filesystem e le utilizza per piazzarci i contenuti.

Il tutto è realizzato attraverso il seguente comando:
``
docker run  -d -p 8001:80 -v ~/dokuwiki-data/it-technical-wiki/pages:/var/dokuwiki-storage/data/pages -v ~/dokuwiki-data/it-technical-wiki/media:/var/dokuwiki-storage/data/media --name dokuwiki-it01 istepanov/dokuwiki
``

## Workflow
  * Eseguire il clone del presente repository
  * Installare DokuWiki (tramite docker) eseguendo il mount del repository git nei path di lavoro (vedi sopra)
  

  
  
  


