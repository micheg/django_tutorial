# Django Workshop.

Django è un framework web ad alto livello per il linguaggio di programmazione Python, progettato per facilitare la creazione di applicazioni web complesse.
Ecco una panoramica di come funziona Django e del rapporto tra applicazioni e progetti.

## Intro

Questo tutorial introdurrà i concetti fondamentali di Djano e poi presenterà una piccola applicazione pratica (con i realtivi test).
Un piccolo servizio di accorciamento degli URL.

### Versione:

- 1.0 RC, ITA (una versione in lingua seguirà si spera prima o poi)

### Struttura di Django

1. **Progetto Django**:
   - Un progetto Django è una raccolta di configurazioni e impostazioni per un'istanza di Django.
   - Include configurazioni globali come il database da utilizzare, le impostazioni di sicurezza, il middleware e le applicazioni installate.
   - Un progetto rappresenta un sito web o un insieme di siti web che condividono una configurazione comune.

2. **Applicazioni Django**:
   - Un'applicazione Django è una componente autonoma che esegue una funzionalità specifica. Ad esempio, un'applicazione potrebbe gestire il blog, un'altra i forum, un'altra l'autenticazione degli utenti, e così via.
   - Un progetto può contenere più applicazioni, ognuna delle quali è indipendente ma può interagire con le altre.
   - Le applicazioni sono progettate per essere riutilizzabili in altri progetti Django, permettendo una modularità e una manutenibilità del codice migliori.

In Django, è necessario aggiungere le applicazioni (apps) installate al file `settings.py` per diversi motivi fondamentali legati al modo in cui il framework gestisce e organizza le sue funzionalità. Ecco perché è importante includere le applicazioni in `settings.py`:

### 1. Configurazione delle Applicazioni

Il file `settings.py` in Django è il punto centrale per configurare tutte le impostazioni del tuo progetto. Includere le applicazioni qui permette a Django di sapere quali applicazioni sono attive nel tuo progetto e di caricare le configurazioni e le risorse necessarie per ciascuna di esse.

### 2. Gestione delle Dipendenze

Le applicazioni in Django sono progettate per essere modulari e riutilizzabili. Ogni applicazione può avere modelli, viste, URL, template, ecc. Includere un'applicazione in `INSTALLED_APPS` segnala a Django di cercare i componenti di quella specifica applicazione durante la fase di avvio del progetto. Questo facilita la gestione delle dipendenze interne al progetto.

### 3. Caricamento Automatico delle Configurazioni

Quando un'applicazione è inclusa in `INSTALLED_APPS`, Django carica automaticamente le configurazioni definite all'interno di ciascuna applicazione. Questo include, ad esempio, i seguenti file che Django cerca in ogni applicazione:
- `models.py`: Contiene i modelli di database definiti per l'applicazione.
- `views.py`: Contiene le funzioni di view che gestiscono la logica delle richieste HTTP per l'applicazione.
- `admin.py`: Contiene la configurazione per l'interfaccia di amministrazione di Django per i modelli definiti nell'applicazione.
- `apps.py`: Configura l'applicazione stessa, se necessario.

### 4. Struttura Modulare e Riutilizzabile

Django promuove una struttura modulare dove ogni applicazione dovrebbe concentrarsi su un aspetto specifico del progetto. Questo approccio modulare semplifica lo sviluppo, il testing e la manutenzione del codice, consentendo anche il riutilizzo di applicazioni in diversi progetti.

### Come Aggiungere un'Applicazione in `settings.py`

Per aggiungere un'applicazione in `settings.py`, segui questi passaggi:

1. Apri il file `settings.py` nel tuo progetto Django.
2. Trova la variabile `INSTALLED_APPS`, che è una lista di stringhe.
3. Aggiungi il nome dell'applicazione come stringa a questa lista. Ad esempio, se hai un'applicazione chiamata `myapp`, aggiungi `'myapp'` alla lista.
   
   ```python
   INSTALLED_APPS = [
       ...
       'myapp',
   ]
   ```

4. Salva il file `settings.py`.

Una volta aggiunta correttamente, l'applicazione sarà pronta per essere utilizzata nel tuo progetto Django. Django si occuperà di cercare le configurazioni e i componenti di `myapp` quando necessario durante l'esecuzione del progetto.

### Rapporto tra Progetti e Applicazioni

- **Organizzazione**: Un progetto Django è come un contenitore generale che gestisce e coordina diverse applicazioni. Ogni applicazione è progettata per risolvere un problema specifico all'interno del progetto.
  
- **Configurazione**: Nel file di configurazione principale del progetto (solitamente chiamato `settings.py`), si elencano le applicazioni installate nel progetto. Questo consente al progetto di sapere quali applicazioni utilizzare e come integrarle.

- **Isolamento e Riutilizzabilità**: Le applicazioni sono isolate le une dalle altre. Questo significa che un'applicazione può essere sviluppata, testata e mantenuta indipendentemente dalle altre. Inoltre, poiché sono modulari, possono essere facilmente riutilizzate in altri progetti Django.

- **Routing e URL**: Ogni applicazione può definire le proprie URL, gestite tramite un file di configurazione degli URL specifico per l'applicazione. Il progetto ha un file di configurazione principale degli URL che include e indirizza le richieste alle varie applicazioni.

- **Database e Modelli**: Ogni applicazione può definire i propri modelli di database. Il progetto gestisce la configurazione del database complessivo e coordina le migrazioni per applicare le modifiche del database in tutte le applicazioni.

### Esempio Pratico

Supponiamo di creare un sito web di e-commerce con Django. Potresti avere un progetto chiamato "EcommerceProject" che include diverse applicazioni:

1. **UserAuth**: Gestisce l'autenticazione e la registrazione degli utenti.
2. **ProductCatalog**: Gestisce l'elenco dei prodotti disponibili per la vendita.
3. **ShoppingCart**: Gestisce il carrello degli acquisti degli utenti.
4. **OrderManagement**: Gestisce il processo di checkout e gli ordini degli utenti.

- **UserAuth** sarà responsabile di tutto ciò che riguarda gli utenti, come login, registrazione, e gestione dei profili.
- **ProductCatalog** gestirà i prodotti, le categorie e le informazioni sui prodotti.
- **ShoppingCart** gestirà gli articoli aggiunti al carrello dagli utenti.
- **OrderManagement** si occuperà della gestione degli ordini, dei pagamenti e delle conferme.

In questo modo, il progetto "EcommerceProject" coordina tutte queste applicazioni per funzionare insieme come un sito web completo, mentre ogni applicazione è separata e gestibile autonomamente.

### Vantaggi del Modello di Django

- **Modularità**: Facilita lo sviluppo, il testing e la manutenzione del codice.
- **Riutilizzabilità**: Le applicazioni possono essere riutilizzate in altri progetti senza modifiche significative.
- **Isolamento**: Le modifiche a un'applicazione hanno meno probabilità di influenzare altre parti del progetto.
- **Collaborazione**: Più sviluppatori possono lavorare su diverse applicazioni contemporaneamente senza conflitti significativi.

Django è un framework web che segue il paradigma MTV (Model-Template-View) per organizzare il codice e facilitare lo sviluppo di applicazioni web. Ecco i concetti chiave di Django spiegati in dettaglio:

### 1. MTV: Model-Template-View

1. **Model (Modello)**:
   - Rappresenta la struttura e i dati dell'applicazione. Ogni modello è una rappresentazione di una tabella nel database.
   - Definisce i campi e i comportamenti dei dati che stai memorizzando.
   - Gestisce la logica aziendale e le interazioni con il database tramite l'ORM di Django.

2. **Template (Template)**:
   - Rappresenta la parte della presentazione dell'applicazione. Gestisce l'aspetto e il layout della pagina web.
   - Utilizza il linguaggio di template di Django per mescolare HTML con il contenuto dinamico.
   - Consente di separare la logica di presentazione dalla logica aziendale.

3. **View (Vista)**:
   - Controlla la logica dell'applicazione e decide quale modello e quale template utilizzare.
   - Riceve richieste HTTP, elabora i dati (se necessario), e restituisce una risposta HTTP.
   - Funziona come intermediario tra i modelli e i template.

### 2. URL Dispatcher

- Gestisce l'instradamento delle richieste HTTP alle viste appropriate.
- Utilizza un file di configurazione degli URL per mappare gli URL a specifiche viste.
- Consente di definire pattern di URL flessibili e leggibili.

### 3. ORM (Object-Relational Mapping)

- Consente di interagire con il database usando oggetti Python invece di scrivere query SQL manualmente.
- Gestisce la traduzione tra oggetti Python e tabelle del database.
- Facilita operazioni di creazione, lettura, aggiornamento e cancellazione (CRUD) sui dati del database.

### 4. Form e Validazione

- Gestisce la raccolta e la validazione dei dati degli utenti tramite moduli.
- I moduli possono essere utilizzati sia per i form HTML che per le API.
- Consente di definire regole di validazione e di mostrare errori di validazione agli utenti.

### 5. Middleware

- È una serie di componenti software che intervengono nel processo di gestione delle richieste e delle risposte.
- Ogni componente middleware può eseguire operazioni come la gestione dell'autenticazione, il controllo degli accessi, la registrazione delle richieste, o la compressione delle risposte.

### 6. Sistema di Autenticazione e Autorizzazione

- Fornisce un sistema integrato per gestire l'autenticazione degli utenti (login, logout, registrazione).
- Gestisce l'autorizzazione degli utenti per garantire che solo gli utenti autorizzati possano accedere a determinate risorse o eseguire determinate azioni.

### 7. Admin Interface

- Genera automaticamente un'interfaccia di amministrazione basata sui modelli definiti.
- Consente di gestire i dati dell'applicazione tramite una GUI senza dover scrivere codice personalizzato.
- Fornisce funzionalità di ricerca, filtraggio e ordinamento per facilitare la gestione dei dati.

### 8. Migrations (Migrazioni)

- Gestisce le modifiche alla struttura del database in modo sicuro e sistematico.
- Consente di creare, applicare e annullare le migrazioni per mantenere il database sincronizzato con i modelli.
- Facilita l'evoluzione del database durante lo sviluppo del progetto.

### 9. Signal (Segnali)

- Permettono di collegare eventi e azioni. Sono utilizzati per invocare determinate funzioni quando accadono eventi specifici (ad esempio, dopo la creazione di un oggetto).
- Forniscono un modo per disaccoppiare la logica dell'applicazione, migliorando la modularità.

### 10. Caching (Caching)

- Supporta il caching per migliorare le prestazioni dell'applicazione.
- Può memorizzare in cache risultati di query, viste o intere pagine.
- Integra vari backend di caching, come Memcached e Redis.

### 11. Gestione dei File Statici e dei Media

- Gestisce i file statici (CSS, JavaScript, immagini) e i file caricati dagli utenti.
- Fornisce strumenti per gestire la raccolta e la distribuzione dei file statici.
- Configura il salvataggio e il recupero dei file caricati dagli utenti in modo sicuro e scalabile.

### 12. Internationalization and Localization (I18N e L10N)

- Supporta la traduzione dell'interfaccia utente in diverse lingue.
- Consente di adattare le applicazioni per vari mercati internazionali.
- Gestisce la formattazione di date, orari e numeri secondo le convenzioni locali.

### Vantaggi Chiave di Django

- **Rapida Sviluppo**: Fornisce molti strumenti e librerie pronte all'uso, riducendo il tempo necessario per sviluppare applicazioni complesse.
- **Sicurezza**: Implementa automaticamente molte pratiche di sicurezza per proteggere le applicazioni da vulnerabilità comuni.
- **Scalabilità**: Supporta facilmente lo sviluppo di applicazioni che possono crescere e scalare con l'aumentare delle esigenze.
- **Comunità Attiva**: Ha una grande comunità di sviluppatori che contribuisce con plugin, estensioni e supporto.


### ORM

L'ORM (Object-Relational Mapping) di Django è uno dei componenti principali del framework e serve a facilitare l'interazione con i database relazionali utilizzando la sintassi e i concetti di Python piuttosto che SQL. Ecco una spiegazione dettagliata di come funziona:

### Concetti Fondamentali dell'ORM di Django

1. **Modelli (Models)**:
   - I modelli in Django sono classi Python che definiscono la struttura del database.
   - Ogni classe rappresenta una tabella nel database, e ogni attributo della classe rappresenta una colonna della tabella.
   - Django fornisce un'ampia gamma di tipi di campo (es. `CharField` per stringhe, `IntegerField` per numeri interi, `DateTimeField` per date e orari) che possono essere utilizzati per definire le colonne della tabella.

2. **Migrazioni**:
   - Le migrazioni sono un sistema per mantenere sincronizzato il database con le modifiche ai modelli.
   - Quando si modifica un modello (ad esempio, aggiungendo un nuovo campo), Django crea una migrazione che descrive la modifica da applicare al database.
   - Le migrazioni possono essere applicate al database tramite comandi gestiti da Django, garantendo che la struttura del database rifletta sempre la definizione dei modelli.

3. **QuerySet**:
   - Un QuerySet è una collezione di oggetti provenienti dal database. Un QuerySet può essere filtrato, ordinato e manipolato usando metodi Python.
   - Django traduce le operazioni sui QuerySet in comandi SQL, permettendo di interagire con il database in modo trasparente e idiomatico.

### Principali Operazioni con l'ORM di Django

1. **Creazione di Record**:
   - Si possono creare nuovi record (righe) nel database instanziando un oggetto del modello e chiamando il metodo `save()` su di esso.
   - L'ORM si occupa di tradurre questa operazione in un comando SQL `INSERT`.

2. **Lettura di Record**:
   - Si possono recuperare record dal database usando metodi come `all()`, `filter()`, e `get()`.
   - Questi metodi generano comandi SQL `SELECT` che vengono eseguiti sul database.

3. **Aggiornamento di Record**:
   - Per aggiornare un record esistente, si recupera l'oggetto, si modificano gli attributi desiderati e si chiama `save()` di nuovo.
   - Questo si traduce in un comando SQL `UPDATE`.

4. **Cancellazione di Record**:
   - Per cancellare un record, si recupera l'oggetto e si chiama il metodo `delete()` su di esso.
   - Questo si traduce in un comando SQL `DELETE`.

### Esempio di Funzionamento dell'ORM

Supponiamo di avere un modello che rappresenta un libro in una libreria. La classe `Book` potrebbe avere attributi come `title`, `author`, `published_date`, e `isbn`.

1. **Creazione di un Nuovo Libro**:
   - Si crea un'istanza della classe `Book` con i dettagli del libro e si chiama `save()`.
   - Django traduce questa azione in un comando SQL `INSERT INTO Book ...`.

2. **Recupero di Libri**:
   - Si può recuperare un elenco di tutti i libri usando `Book.objects.all()`.
   - Si possono filtrare i libri per autore usando `Book.objects.filter(author="Nome Autore")`.
   - Django traduce queste azioni in comandi SQL `SELECT * FROM Book ...`.

3. **Aggiornamento di un Libro**:
   - Si recupera il libro desiderato, si modifica un attributo (es. `title`), e si chiama `save()`.
   - Django traduce questa azione in un comando SQL `UPDATE Book SET title = ... WHERE id = ...`.

4. **Cancellazione di un Libro**:
   - Si recupera il libro desiderato e si chiama `delete()`.
   - Django traduce questa azione in un comando SQL `DELETE FROM Book WHERE id = ...`.

### Vantaggi dell'ORM di Django

- **Astrazione del Database**: Permette di scrivere codice che funziona con vari database senza cambiare il codice applicativo.
- **Sicurezza**: Protegge automaticamente dalle vulnerabilità comuni come SQL injection.
- **Facilità d'Uso**: Facilita la gestione del database con sintassi Python, riducendo la necessità di scrivere SQL manualmente.
- **Coerenza**: Garantisce che le modifiche ai modelli siano sempre sincronizzate con la struttura del database tramite le migrazioni.

### Sistema di URL in Django

Il sistema di URL in Django è responsabile di mappare le richieste HTTP agli appropriati gestori di vista. Questo processo è fondamentale per determinare quale codice deve essere eseguito quando un utente visita un URL specifico.

#### Concetti Chiave del Sistema di URL

1. **URLconf (URL Configuration)**:
   - È un file di configurazione che definisce le mappature tra URL e viste.
   - Ogni progetto Django ha un file principale `urls.py` che contiene le configurazioni degli URL.

2. **Pattern di URL**:
   - Gli URL sono definiti usando pattern, che possono includere stringhe statiche e parametri dinamici.
   - I pattern di URL possono utilizzare espressioni regolari per catturare parti variabili dell'URL e passarle alle viste come argomenti.

3. **Vista**:
   - Una vista è una funzione o una classe che riceve una richiesta HTTP e restituisce una risposta HTTP.
   - Il sistema di URL mappa un pattern di URL a una vista specifica.

4. **Namespace degli URL**:
   - I namespaces sono usati per organizzare e raggruppare gli URL, soprattutto quando si hanno molte applicazioni o quando si include un'applicazione in diversi progetti.

5. **Include**:
   - L'istruzione `include` permette di includere altre configurazioni di URL da altre applicazioni.
   - Questo permette una modularità e una gestione migliore degli URL, specialmente nei progetti di grandi dimensioni.

#### Come Funziona il Sistema di URL

1. **Richiesta Iniziale**:
   - Quando un utente visita un sito web Django, il server riceve una richiesta HTTP e la passa al gestore URL di Django.

2. **Matching dell'URL**:
   - Django confronta l'URL richiesto con i pattern definiti nel file `urls.py`.
   - Se trova una corrispondenza, Django estrae eventuali parametri dinamici e li passa alla vista associata.

3. **Chiamata della Vista**:
   - La vista corrispondente viene chiamata con i parametri della richiesta (inclusi eventuali parametri dinamici dell'URL).
   - La vista elabora la richiesta, interagisce con i modelli se necessario, e genera una risposta HTTP.

4. **Risposta**:
   - La vista restituisce una risposta HTTP, che può essere una pagina HTML, un JSON, un reindirizzamento, ecc.
   - Django invia questa risposta al client (es. il browser dell'utente).

### Segnali in Django

I segnali in Django sono un meccanismo per consentire a determinati componenti di notificare ad altre parti del sistema quando si verificano eventi particolari. Sono utilizzati per disaccoppiare la logica e migliorare la modularità.

#### Concetti Chiave dei Segnali

1. **Signal (Segnale)**:
   - È un tipo di evento che può essere inviato quando accade qualcosa di interessante (ad esempio, la creazione di un nuovo record in un modello).

2. **Emitter (Emettitore)**:
   - È il componente che invia il segnale. Può essere una funzione, un metodo o una classe che emette il segnale quando si verifica un determinato evento.

3. **Receiver (Ricevitore)**:
   - È una funzione o un metodo che riceve il segnale. Viene chiamato quando il segnale viene emesso e può eseguire qualsiasi logica necessaria in risposta all'evento.

4. **Connettere e Disconnettere**:
   - I segnali devono essere collegati ai ricevitori per funzionare. Questo processo è noto come "connettere" il ricevitore al segnale.
   - I segnali possono anche essere scollegati dai ricevitori, il che interrompe la notifica.

#### Come Funzionano i Segnali

1. **Definizione del Segnale**:
   - Un segnale è definito in modo che possa essere utilizzato in tutto il progetto o in una specifica applicazione.
   - Django include segnali predefiniti per eventi comuni come la creazione, la modifica e la cancellazione di un oggetto del modello.

2. **Connessione del Ricevitore**:
   - Si collega una funzione ricevitore al segnale. Questa funzione verrà eseguita ogni volta che il segnale viene emesso.
   - Il collegamento può essere fatto tramite decoratori o utilizzando una funzione di connessione.

3. **Emissione del Segnale**:
   - Quando si verifica l'evento per cui il segnale è stato definito, l'emettitore invia il segnale.
   - Tutti i ricevitori collegati vengono chiamati con i parametri forniti dall'emettitore.

4. **Ricezione e Azione**:
   - I ricevitori eseguono la loro logica in risposta al segnale. Ad esempio, potrebbero aggiornare altri modelli, inviare notifiche, o registrare eventi nei log.

### Esempio Pratico dell'Uso dei Segnali

Supponiamo di avere un modello `User` e di voler eseguire un'azione ogni volta che un nuovo utente viene creato.

1. **Creazione di un Nuovo Utente**:
   - Quando un nuovo utente viene creato nel database, Django emette un segnale `post_save` associato al modello `User`.

2. **Ricezione del Segnale**:
   - Un ricevitore precedentemente collegato al segnale `post_save` viene chiamato.
   - La funzione ricevitore potrebbe, ad esempio, inviare un'email di benvenuto al nuovo utente.

3. **Esecuzione della Logica del Ricevitore**:
   - La funzione ricevitore esegue la sua logica (es. invio dell'email) in risposta al segnale `post_save`.

### Vantaggi dei Segnali

- **Disaccoppiamento**: Consentono di separare la logica in componenti indipendenti, migliorando la manutenibilità.
- **Modularità**: Facilmente aggiungibili e rimovibili senza modificare il codice esistente.
- **Riutilizzabilità**: I ricevitori di segnali possono essere riutilizzati in diverse parti dell'applicazione.

### Concetti Chiave dei Form in Django

1. **Form (Modulo)**:
   - Un form è una rappresentazione di un modulo HTML che raccoglie e valida i dati dell'utente.
   - Django fornisce una classe `Form` che permette di definire i campi del modulo, le regole di validazione e il layout.

2. **Campi del Form**:
   - Ogni campo del form rappresenta un singolo input (es. testo, data, numero, ecc.).
   - Django offre una varietà di tipi di campi (es. `CharField` per testo, `DateField` per date, `EmailField` per email) che includono validazioni integrate.

3. **Validazione**:
   - I form di Django validano automaticamente i dati in ingresso per garantire che rispettino i criteri definiti.
   - La validazione può essere personalizzata per includere regole specifiche.

4. **Rendering del Form**:
   - I form possono essere resi come HTML usando i template di Django.
   - Django fornisce metodi per generare automaticamente il markup HTML per i form.

5. **Gestione degli Errori**:
   - Se i dati del form non sono validi, Django fornisce un meccanismo per restituire i messaggi di errore all'utente.
   - Gli errori di validazione vengono mostrati accanto ai rispettivi campi del form.

### Relazione tra Form e Modelli

1. **ModelForm**:
   - Django fornisce una classe `ModelForm` che crea automaticamente un form basato su un modello.
   - Un `ModelForm` mappa i campi del form ai campi del modello, semplificando la creazione e l'aggiornamento degli oggetti del database.
   - Questa classe gestisce la creazione e l'aggiornamento degli oggetti del modello in base ai dati del form.

2. **Sincronizzazione dei Dati**:
   - Quando un `ModelForm` viene inviato, i dati del form vengono convalidati e utilizzati per creare o aggiornare un'istanza del modello.
   - Se i dati sono validi, il `ModelForm` salva l'oggetto del modello nel database.

### Flusso di Lavoro dei Form

1. **Creazione del Form**:
   - Un form viene definito specificando i campi e le regole di validazione.
   - Per i form basati su modelli, si utilizza un `ModelForm` che mappa automaticamente ai campi del modello.

2. **Rendering del Form**:
   - Il form viene reso in un template HTML, dove gli utenti possono inserire i dati.
   - I campi del form sono resi come elementi HTML (es. `<input>`, `<textarea>`).

3. **Invio e Validazione**:
   - Quando l'utente invia il form, i dati vengono inviati al server.
   - Django raccoglie i dati e crea un'istanza del form popolata con i dati inviati.
   - Il form valida i dati per assicurarsi che rispettino le regole definite (es. formato corretto, campi obbligatori compilati).

4. **Gestione degli Errori (se presenti)**:
   - Se i dati non sono validi, il form riporta gli errori di validazione.
   - Gli errori vengono mostrati nel template HTML, consentendo all'utente di correggere i dati e reinviare il form.

5. **Salvataggio dei Dati**:
   - Se i dati sono validi, il form può creare o aggiornare un'istanza del modello.
   - Il `ModelForm` salva automaticamente l'oggetto del modello nel database, sincronizzando i dati del form con il modello.

### Esempio Pratico del Flusso di Lavoro

Supponiamo di avere un'applicazione per gestire un elenco di libri. Il modello `Book` ha campi come `title`, `author`, e `published_date`.

1. **Creazione del Form**:
   - Si definisce un `ModelForm` basato sul modello `Book`.
   - I campi del form includono `title`, `author`, e `published_date`.

2. **Rendering del Form**:
   - Il form viene mostrato in una pagina HTML dove l'utente può inserire i dettagli del libro.

3. **Invio e Validazione**:
   - L'utente compila il form e lo invia.
   - Django raccoglie i dati inviati, li popola nel form e valida i dati.

4. **Gestione degli Errori**:
   - Se, ad esempio, l'utente non compila il campo `title`, Django segnalerà un errore di validazione e mostrerà un messaggio di errore accanto al campo `title`.

5. **Salvataggio dei Dati**:
   - Se tutti i dati sono validi, Django utilizza il `ModelForm` per creare un nuovo oggetto `Book` e lo salva nel database.

### Vantaggi dei Form di Django

- **Sicurezza**: Django gestisce automaticamente la pulizia e la validazione dei dati, proteggendo contro vulnerabilità comuni come l'iniezione di codice.
- **Facilità d'Uso**: I form e i `ModelForm` semplificano il processo di creazione di moduli e di interazione con i modelli, riducendo la quantità di codice da scrivere.
- **Riutilizzabilità**: I form possono essere facilmente riutilizzati in diverse parti dell'applicazione.
- **Gestione degli Errori**: Forniscono un meccanismo integrato per mostrare errori di validazione agli utenti in modo chiaro e conciso.

Il `csrf_token` è una componente fondamentale della sicurezza delle applicazioni web in Django. CSRF sta per Cross-Site Request Forgery, un tipo di attacco in cui un utente malintenzionato induce un utente legittimo a eseguire azioni indesiderate su un sito web in cui è autenticato. Django utilizza il `csrf_token` per prevenire questi attacchi. Vediamo come funziona e come viene utilizzato in dettaglio.

### Cos'è il CSRF

Cross-Site Request Forgery (CSRF) è un attacco in cui un malintenzionato induce un utente autenticato a inviare richieste indesiderate al sito web in cui è autenticato, utilizzando la loro sessione attiva. Questo può portare a operazioni non autorizzate come modifiche di dati, trasferimenti di fondi, o altre azioni critiche.

### Cos'è il `csrf_token`

Il `csrf_token` è un token di sicurezza che viene utilizzato per proteggere i form HTML da attacchi CSRF. È un valore univoco e segreto generato dal server e associato alla sessione dell'utente. Ogni volta che un form viene inviato, il token viene incluso nella richiesta e il server verifica che il token inviato corrisponda a quello associato alla sessione dell'utente.

### Come Funziona il `csrf_token` in Django

1. **Generazione del Token**:
   - Quando un utente accede a una pagina con un form protetto da CSRF, Django genera un token univoco e lo associa alla sessione dell'utente.
   - Questo token viene incluso nel form come campo nascosto.

2. **Inclusione nel Form**:
   - Nei template Django, il token viene inserito nel form utilizzando il tag `{% csrf_token %}`.
   - Quando l'utente invia il form, il token viene inviato insieme ai dati del form.

3. **Verifica del Token**:
   - Quando il server riceve la richiesta POST con i dati del form, verifica che il token inviato corrisponda a quello associato alla sessione dell'utente.
   - Se il token è valido, la richiesta viene accettata e processata.
   - Se il token è mancante o non valido, Django rifiuta la richiesta e restituisce un errore di protezione CSRF.

### Utilizzo del `csrf_token` in Django

#### Nei Template

Quando si crea un form in un template Django, è necessario includere il token CSRF per garantire che la richiesta sia protetta. Questo viene fatto aggiungendo il tag `{% csrf_token %}` all'interno del form.

Esempio:
- Si crea un form HTML in un template.
- All'interno del form, si utilizza il tag `{% csrf_token %}` per inserire il token CSRF come campo nascosto.

#### Nei Form AJAX

Quando si utilizzano richieste AJAX per inviare dati al server, è necessario includere il token CSRF nell'intestazione della richiesta. Questo può essere fatto manualmente o utilizzando librerie JavaScript che supportano automaticamente l'invio del token CSRF.

Esempio:
- Si configura il client AJAX per inviare il token CSRF come parte dell'intestazione della richiesta.
- Il server verifica il token come farebbe con un form tradizionale.

### Vantaggi del `csrf_token`

- **Sicurezza**: Protegge contro attacchi CSRF, assicurando che solo le richieste legittime siano processate.
- **Semplicità**: Facile da implementare nei template e nelle richieste AJAX.
- **Integrità dei Dati**: Garantisce che le azioni critiche vengano eseguite solo dagli utenti legittimi.

### Cosa Succede se il `csrf_token` Non è Valido

Se Django riceve una richiesta POST senza un token CSRF valido o senza token, restituisce un errore di protezione CSRF. Questo impedisce all'attaccante di eseguire operazioni non autorizzate. Gli utenti legittimi vedranno un messaggio di errore e dovranno ripetere l'azione, assicurandosi di avere un token CSRF valido.

Il `csrf_token` è un meccanismo di sicurezza in Django che protegge le applicazioni web dagli attacchi CSRF. Funziona generando un token univoco associato alla sessione dell'utente, che deve essere inviato insieme a ogni richiesta POST. Django verifica il token e processa la richiesta solo se il token è valido. Questo assicura che le azioni critiche possano essere eseguite solo dagli utenti legittimi, proteggendo l'integrità e la sicurezza dell'applicazione.

### Hello world

Adesso è il momento di vedere da vicino un po' di codice. Andremo passo per passo nella creazione di un progetto Django "Hello World".

Useremo un "virtual environment" (ambiente virtuale), uno strumento standard in Python per creare ambienti isolati per progetti. Vediamo perché è utile e come usarlo con Django.

### Cos'è un Virtual Environment?

Un virtual environment è una directory che contiene un'installazione isolata di Python e librerie Python. Questo significa che puoi avere diverse versioni di librerie installate in differenti progetti senza che ci siano conflitti.

### Perché Usare un Virtual Environment?

1. **Isolamento dei Progetti**: Evita conflitti tra diverse versioni di librerie usate in progetti diversi.
2. **Gestione delle Dipendenze**: Ogni progetto può avere le proprie dipendenze specifiche.
3. **Facilità di Distribuzione**: Puoi facilmente replicare l'ambiente di sviluppo su altri sistemi (es. produzione) usando `requirements.txt`.

### Come Creare e Usare un Virtual Environment

1. **Installazione di `venv`**: È incluso nelle versioni recenti di Python (3.3+), quindi non è necessario installarlo separatamente.

2. **Creazione di un Virtual Environment**:
   Da terminale, naviga nella directory del tuo progetto e crea un virtual environment:

   ```sh
   python -m venv myenv
   ```

   Qui, `myenv` è il nome della directory che conterrà il virtual environment. Puoi chiamarla come preferisci.

3. **Attivazione del Virtual Environment**:
   - **Su Windows**:

     ```sh
     myenv\Scripts\activate
     ```

   - **Su MacOS/Linux**:

     ```sh
     source myenv/bin/activate
     ```

   Dopo l'attivazione, il prompt del terminale dovrebbe cambiare per indicare che l'ambiente virtuale è attivo (es. `(myenv)`).

4. **Installazione di Django**:
   Con l'ambiente virtuale attivo, puoi installare Django:

   ```sh
   pip install django
   ```

5. **Disattivazione del Virtual Environment**:
   Quando hai finito di lavorare, puoi disattivare l'ambiente virtuale con il comando:

   ```sh
   deactivate
   ```

### Riepilogo

Utilizzare un virtual environment per i tuoi progetti Django (e Python in generale) è una buona pratica per mantenere le dipendenze isolate e gestire meglio i progetti. Segui i passaggi sopra per creare, attivare e usare un virtual environment con Django, e sarai in grado di gestire facilmente le tue dipendenze senza conflitti.

### 1. Installazione di Django

Assicurati di avereun virtual env attivo, Poi, puoi installare Django utilizzando `pip`.

```sh
pip install django
```

### 2. Creazione del Progetto

Per creare un nuovo progetto Django, usa il comando:

```sh
django-admin startproject myproject
```

Questo comando creerà una directory `myproject` con la seguente struttura:

```
myproject/
    manage.py
    myproject/
        __init__.py
        settings.py
        urls.py
        wsgi.py
        asgi.py
```

### 3. Spiegazione della Struttura

- `manage.py`: Un'utilità per interagire con il progetto Django (es. avviare il server di sviluppo, creare app, ecc.).
- `myproject/`: La directory del progetto principale.
  - `__init__.py`: Rende `myproject` una Python package.
  - `settings.py`: Il file di configurazione del progetto.
  - `urls.py`: Il file di configurazione degli URL.
  - `wsgi.py`: Un punto di ingresso per i server web compatibili con WSGI.
  - `asgi.py`: Un punto di ingresso per i server web compatibili con ASGI.

### 4. Creazione di un'Applicazione

Dentro il progetto, crea una nuova applicazione:

```sh
cd myproject
python manage.py startapp hello
```

Questo comando creerà una directory `hello` con la seguente struttura:

```
hello/
    __init__.py
    admin.py
    apps.py
    models.py
    tests.py
    views.py
    migrations/
```

### 5. Spiegazione della Struttura dell'Applicazione

- `admin.py`: Configura l'interfaccia di amministrazione per i modelli dell'applicazione.
- `apps.py`: Configura alcune impostazioni specifiche dell'app.
- `models.py`: Definisce i modelli (le strutture dati) per l'app.
- `tests.py`: Contiene i test per l'app.
- `views.py`: Contiene le funzioni che determinano cosa verrà visualizzato agli utenti.
- `migrations/`: Contiene le migrazioni del database per i modelli.

### 6. Creazione della View "Hello World"

Modifica `hello/views.py` per aggiungere una semplice view che ritorna "Hello World":

```python
from django.http import HttpResponse

def hello_world(request):
    return HttpResponse("Hello World")
```

### 7. Configurazione degli URL

Dovrai configurare gli URL per poter accedere alla tua view. Modifica `myproject/urls.py`:

```python
from django.contrib import admin
from django.urls import path
from hello.views import hello_world

urlpatterns = [
    path('admin/', admin.site.urls),
    path('hello/', hello_world),
]
```

### 8. Aggiunta dell'Applicazione alle Impostazioni

Assicurati che la tua app sia inclusa nelle impostazioni del progetto. Modifica `myproject/settings.py` aggiungendo `'hello',` nella lista `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
    ...
    'hello',
]
```

### 9. Avvio del Server di Sviluppo

Avvia il server di sviluppo per vedere il risultato:

```sh
python manage.py runserver
```

Apri il browser e vai su `http://127.0.0.1:8000/hello/`. Dovresti vedere "Hello World".

### Riepilogo delle Relazioni tra le Parti

1. **Project (`myproject`)**: Contiene le configurazioni globali (settings, URLs, WSGI/ASGI).
2. **App (`hello`)**: Contiene la logica specifica dell'applicazione (views, models, admin, ecc.).
3. **View (`hello_world`)**: Una funzione che elabora una richiesta HTTP e restituisce una risposta HTTP.
4. **URL Configuration (`myproject/urls.py`)**: Mappa gli URL alle corrispondenti view.

Ora abbiamo una semplice applicazione Django "Hello World". Abbiamo visto come sono strutturate le directory e come sono relazionate tra loro le varie parti di un progetto Django.
Possiamo passare a qualcosa di leggermente più complesso.
Prenderemo in esame un progetto di short url.

Spendiamo due parole ancora sulla CLi.
Il comando `django-admin` è uno strumento della riga di comando fornito da Django, un popolare framework web per Python. Viene utilizzato per gestire vari aspetti di un progetto Django. Ecco una panoramica del funzionamento di `django-admin` e delle sue funzionalità principali:

### Uso di base di `django-admin`
Per utilizzare `django-admin`, devi avere Django installato nel tuo ambiente. Puoi eseguire il comando `django-admin` dalla riga di comando seguito dal sottocomando che desideri eseguire. Esempio:

```bash
django-admin startproject myproject
```

### Principali comandi di `django-admin`
Ecco una lista dei comandi più comuni e delle loro funzionalità:

1. **startproject**: Crea una nuova directory per il progetto Django con una struttura predefinita di file e directory.
   ```bash
   django-admin startproject nome_progetto
   ```

2. **startapp**: Crea una nuova applicazione all'interno del progetto.
   ```bash
   django-admin startapp nome_applicazione
   ```

3. **runserver**: Avvia il server di sviluppo per il progetto Django.
   ```bash
   django-admin runserver
   ```

4. **migrate**: Applica e sincronizza le migrazioni del database.
   ```bash
   django-admin migrate
   ```

5. **makemigrations**: Crea nuove migrazioni basate sui cambiamenti apportati ai modelli del database.
   ```bash
   django-admin makemigrations
   ```

6. **createsuperuser**: Crea un nuovo utente amministratore (superuser) per il progetto Django.
   ```bash
   django-admin createsuperuser
   ```

7. **collectstatic**: Raccoglie tutti i file statici delle app in un'unica directory (usato per la distribuzione).
   ```bash
   django-admin collectstatic
   ```

8. **flush**: Resetta il database eliminando tutti i dati e ricreando le tabelle.
   ```bash
   django-admin flush
   ```

9. **shell**: Avvia una shell interattiva Python con l'ambiente Django pre-caricato.
   ```bash
   django-admin shell
   ```

10. **dbshell**: Avvia una shell del database collegata al tuo database configurato.
    ```bash
    django-admin dbshell
    ```

11. **test**: Esegue i test definiti nelle applicazioni.
    ```bash
    django-admin test
    ```

12. **changepassword**: Cambia la password di un utente specificato.
    ```bash
    django-admin changepassword nome_utente
    ```

### Opzioni comuni
Molti comandi di `django-admin` accettano opzioni che modificano il loro comportamento. Alcune opzioni comuni includono:

- `--settings`: Specifica un modulo di impostazioni personalizzato.
  ```bash
  django-admin runserver --settings=myproject.settings
  ```

- `--pythonpath`: Aggiunge un percorso alla variabile di ambiente `PYTHONPATH`.
  ```bash
  django-admin runserver --pythonpath=/path/to/myproject
  ```

- `--verbosity`: Imposta il livello di verbosità dell'output del comando (0, 1, 2, 3).
  ```bash
  django-admin migrate --verbosity=2
  ```

### Personalizzazione
Puoi creare comandi personalizzati per `django-admin` creando script Python all'interno di una delle tue applicazioni Django. Questo è utile per automatizzare attività specifiche del tuo progetto.

Il comando `django-admin` è uno strumento potente e flessibile che facilita la gestione di un progetto Django. Conoscere e utilizzare efficacemente i vari comandi e opzioni disponibili può migliorare notevolmente il flusso di lavoro e la produttività durante lo sviluppo di applicazioni web con Django.

### Struttura del Progetto

Il progetto è suddiviso in vari componenti principali, ciascuno con uno scopo ben definito. Questo approccio garantisce una separazione chiara delle responsabilità e una maggiore manutenibilità del codice.

#### 1. **Progetto Django**

- **url_shortener/**: Questa cartella contiene il progetto principale Django, con le configurazioni globali e le impostazioni del progetto.
  - `settings.py`: File di configurazione del progetto. Contiene le impostazioni globali come il database, le app installate, i middleware, ecc.
  - `urls.py`: Configura le URL globali del progetto, includendo quelle definite nell'applicazione `shortener`.

#### 2. **Applicazione Django**

- **shortener/**: Questa cartella contiene l'applicazione specifica per la gestione degli URL corti.
  - `models.py`: Definisce i modelli del database, ossia le strutture dei dati che verranno salvate nel database.
  - `views.py`: Contiene la logica di business dell'applicazione, ossia le funzioni che gestiscono le richieste e restituiscono le risposte appropriate.
  - `forms.py`: Definisce i form utilizzati per l'input degli utenti, come la registrazione e la creazione degli URL.
  - `urls.py`: Configura le URL specifiche dell'applicazione, mappando le richieste HTTP alle funzioni delle viste.
  - `templates/`: Contiene i template HTML che definiscono la struttura delle pagine web visualizzate dagli utenti.

### Algoritmo di Generazione degli URL Corti

L'algoritmo per generare gli URL corti deve garantire che ogni URL corto sia univoco e sufficientemente breve. Ecco una spiegazione del processo senza entrare nel dettaglio del codice:

1. **Raccolta dei Dati**: Quando un utente inserisce un URL da accorciare, il sistema raccoglie l'URL originale e l'utente che lo ha inserito.

2. **Generazione dell'URL Corto**: Viene generato un codice casuale di lunghezza fissa utilizzando una combinazione di lettere maiuscole, minuscole e cifre. Questo codice viene poi utilizzato come parte dell'URL corto.

3. **Verifica dell'Unicità**: Prima di salvare l'URL corto nel database, il sistema verifica che il codice generato non esista già. Se esiste, viene generato un nuovo codice e si ripete il processo.

4. **Salvataggio nel Database**: Una volta ottenuto un codice univoco, l'URL originale e l'URL corto vengono salvati nel database associandoli all'utente.

### Scelte Progettuali

#### 1. **Separazione delle Responsabilità**

- **Modelli (Models)**: I modelli definiscono la struttura dei dati e rappresentano le entità principali dell'applicazione (ad es. utenti e URL). Questa separazione consente di gestire facilmente l'archiviazione e il recupero dei dati.
- **Viste (Views)**: Le viste contengono la logica di business e sono responsabili di gestire le richieste HTTP, elaborare i dati e restituire le risposte appropriate. Separare la logica di business dai modelli e dai template rende il codice più organizzato e manutenibile.
- **Form**: I form gestiscono l'input degli utenti, facilitando la validazione e la pulizia dei dati inseriti.

#### 2. **Autenticazione e Autorizzazione**

- **Registrazione e Login degli Utenti**: La gestione degli utenti è centrale nell'applicazione, permettendo a ciascun utente di avere il proprio spazio personale per gestire gli URL corti. Django fornisce funzionalità robuste per l'autenticazione e l'autorizzazione che vengono sfruttate per semplificare queste operazioni.


L'approccio utilizzato in questo progetto sfrutta al meglio le funzionalità offerte da Django, come la gestione delle sessioni e dei form, la separazione dei componenti MVC (Model-View-Controller); queste scelte progettuali non solo rendono l'applicazione più robusta e sicura, ma anche più facile da estendere e mantenere nel tempo.

### 1. Impostazione dell'Ambiente

#### Installazione di Django

Prima di tutto, assicurati di avere venv installato e attivato.
Tutti gli esempi da shell si riferiscono ad un ambiente di tipo *Unix* per seguire il tutorial su windows è necessario aggiustare alcuni comandi.

```sh
python3 -m venv .
. bin/activate
```


Poi, installa Django.

```sh
pip install django
```

#### Creazione del Progetto Django

Crea un nuovo progetto Django chiamato `url_shortener`.

```sh
django-admin startproject url_shortener
cd url_shortener
```

#### Creazione dell'Applicazione

Crea una nuova applicazione chiamata `shortener`.

```sh
python manage.py startapp shortener
```

Aggiungi `shortener` alle `INSTALLED_APPS` nel file `settings.py`.

```python
INSTALLED_APPS = [
    ...
    'shortener',
    'django.contrib.staticfiles',  # per gestire i file statici
    ...
]
```

#### Configurazione del Database

Utilizzeremo il database SQLite predefinito per semplicità, ma puoi configurare un altro database se necessario. Assicurati che il file `settings.py` contenga la configurazione del database corretta.

### 2. Modelli e Migrazioni

#### Creazione dei Modelli

Apri `shortener/models.py` e crea i seguenti modelli: `UserProfile`, `URL`, e `User`.

```python
from django.contrib.auth.models import User
from django.db import models
from django.urls import reverse

class UserProfile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    bio = models.TextField(blank=True, null=True)

    def __str__(self):
        return self.user.username

class URL(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    original_url = models.URLField()
    short_url = models.CharField(max_length=10, unique=True)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.short_url

    def get_short_url(self):
        return reverse('redirect_url', kwargs={'short_url': self.short_url})
```

Per creare un utente amministratore (admin) in Django, puoi seguire alcuni passaggi semplici. Gli utenti admin hanno accesso privilegiato all'interfaccia di amministrazione di Django e possono gestire i dati dell'applicazione direttamente tramite il pannello di amministrazione.

### Creazione di un Utente Amministratore in Django

1. **Creazione di un Superuser**:
   - Apri il terminale o il prompt dei comandi.
   - Naviga nella directory del tuo progetto Django dove si trova il file `manage.py`.

2. **Esegui il comando di creazione di un superuser**:
   - Esegui il seguente comando per avviare il processo di creazione di un superuser:

     ```sh
     python manage.py createsuperuser
     ```

   - Premi Invio. Ti verranno chiesti alcuni dettagli per configurare il superuser:
     - **Username**: Inserisci un nome utente per il superuser. Ad esempio, `admin`.
     - **Indirizzo email**: Puoi inserire un indirizzo email (opzionale).
     - **Password**: Inserisci una password sicura. La password non sarà visibile mentre la digiti per motivi di sicurezza.

3. **Completare la creazione**:
   - Dopo aver inserito questi dettagli, conferma la password quando richiesto.

4. **Accesso all'interfaccia di amministrazione**:
   - Una volta creato il superuser con successo, puoi accedere all'interfaccia di amministrazione di Django utilizzando le seguenti URL nel tuo browser:
     - `http://localhost:8000/admin/` (se stai eseguendo il server di sviluppo Django localmente)
     - Inserisci le credenziali del superuser (username e password) che hai appena creato.

5. **Gestione dei dati tramite l'interfaccia di amministrazione**:
   - Una volta effettuato l'accesso, sarai in grado di gestire i dati del tuo progetto tramite l'interfaccia di amministrazione di Django. Puoi aggiungere, modificare o eliminare dati secondo le tue necessità.


#### Migrazioni del Database

Esegui le migrazioni per creare le tabelle nel database.

```sh
python manage.py makemigrations
python manage.py migrate
```

### 3. Creazione dei Form

Creiamo i form per la registrazione e la creazione degli URL. Apri `shortener/forms.py`.

```python
from django import forms
from django.contrib.auth.models import User
from .models import URL

class UserRegistrationForm(forms.ModelForm):
    password = forms.CharField(widget=forms.PasswordInput)
    password2 = forms.CharField(widget=forms.PasswordInput, label='Repeat password')

    class Meta:
        model = User
        fields = ('username', 'email', 'first_name', 'last_name')

    def clean_password2(self):
        cd = self.cleaned_data
        if cd['password'] != cd['password2']:
            raise forms.ValidationError('Passwords don\'t match.')
        return cd['password2']

class URLForm(forms.ModelForm):
    class Meta:
        model = URL
        fields = ['original_url']
```

### 4. Creazione delle Viste

Apri `shortener/views.py` e crea le viste per la registrazione, il login, la gestione degli URL e la pagina del profilo.

```python
from django.shortcuts import render, redirect, get_object_or_404
from django.contrib.auth import authenticate, login, logout
from django.contrib.auth.decorators import login_required
from django.contrib.auth.models import User
from .forms import UserRegistrationForm, URLForm
from .models import URL
import random
import string

def generate_short_url():
    return ''.join(random.choice(string.ascii_letters + string.digits) for _ in range(10))

def user_register(request):
    if request.method == 'POST':
        form = UserRegistrationForm(request.POST)
        if form.is_valid():
            new_user = form.save(commit=False)
            new_user.set_password(form.cleaned_data['password'])
            new_user.save()
            UserProfile.objects.create(user=new_user)
            return redirect('login')
    else:
        form = UserRegistrationForm()
    return render(request, 'shortener/register.html', {'form': form})

def user_login(request):
    if request.method == 'POST':
        username = request.POST['username']
        password = request.POST['password']
        user = authenticate(request, username=username, password=password)
        if user is not None:
            login(request, user)
            return redirect('dashboard')
        else:
            return render(request, 'shortener/login.html', {'error': 'Invalid login credentials'})
    return render(request, 'shortener/login.html')

@login_required
def user_logout(request):
    logout(request)
    return redirect('login')

@login_required
def dashboard(request):
    urls = URL.objects.filter(user=request.user)
    if request.method == 'POST':
        form = URLForm(request.POST)
        if form.is_valid():
            new_url = form.save(commit=False)
            new_url.user = request.user
            new_url.short_url = generate_short_url()
            new_url.save()
            return redirect('dashboard')
    else:
        form = URLForm()
    return render(request, 'shortener/dashboard.html', {'form': form, 'urls': urls})

@login_required
def profile(request):
    return render(request, 'shortener/profile.html')

def redirect_url(request, short_url):
    url = get_object_or_404(URL, short_url=short_url)
    return redirect(url.original_url)
```

### 5. Creazione delle URL

Apri `shortener/urls.py` e configura le rotte per le viste.

```python
from django.urls import path
from . import views

urlpatterns = [
    path('register/', views.user_register, name='register'),
    path('login/', views.user_login, name='login'),
    path('logout/', views.user_logout, name='logout'),
    path('dashboard/', views.dashboard, name='dashboard'),
    path('profile/', views.profile, name='profile'),
    path('<str:short_url>/', views.redirect_url, name='redirect_url'),
]
```

Aggiungi il file `shortener/urls.py` alle URL del progetto principale. Apri `url_shortener/urls.py` e modifica come segue:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('shortener.urls')),
]
```

### 6. Creazione dei Template

Crea una cartella `templates` all'interno della tua applicazione `shortener` e poi crea i seguenti file HTML: `register.html`, `login.html`, `dashboard.html`, `profile.html`.

```sh
mkdir shortener/templates
cd shortener/templates
mkdir shortener
cd shortenermo
touch register.html login.html dashboard.html profile.html
```

#### modificare settings.py

```python
.....
import os
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'shortener', 'templates'),],
        'APP_DIRS': True,
.....
```

#### register.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Register</title>
</head>
<body>
    <h2>Register</h2>
    <form method="post">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit">Register</button>
    </form>
</body>
</html>
```

#### login.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Login</title>
</head>
<body>
    <h2>Login</h2>
    <form method="post">
        {% csrf_token %}
        <p><label for="username">Username:</label> <input type="text" name="username" required></p>
        <p><label for="password">Password:</label> <input type="password" name="password" required></p>
        <button type="submit">Login</button>
    </form>
    {% if error %}
    <p>{{ error }}</p>
    {% endif %}
</body>
</html>
```

#### dashboard.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Dashboard</title>
</head>
<body>
    <h2>Dashboard</h2>
    <form method="post">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit">Shorten URL</button>
    </form>
    <h3>Your URLs</h3>
    <ul>
        {% for url in urls %}
        <li><a href="{{ url.get_short_url }}">{{ url.short_url }}</a></li>
        {% endfor %}
    </ul>
    <p><a href="{% url 'profile' %}">Profile</a></p>
    <p><a href="{% url 'logout' %}">Logout</a></p>
</body>
</html>
```

#### profile.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Profile</title>
</head>
<body>
    <h2>Profile</h2>
    <p>Username: {{ request.user.username }}</p>
    <p>Email: {{ request.user.email }}</p>
    <p>Bio: {{ request.user.userprofile.bio }}</p>
    <p><a href="{% url 'dashboard' %}">Back to Dashboard</a></p>
    <p><a href="{% url 'logout' %}">Logout</a></p>
</body>
</html>


```

### 8. Testing e Debugging

Esegui il server di sviluppo e verifica che tutto funzioni correttamente.

```sh
python manage.py runserver
```

Visita `http://127.0.0.1:8000/register/` per registrare un nuovo utente, poi accedi e inizia a creare URL corti dalla dashboard.

Abbiamo creato un'applicazione Django semplice ma funzionale per creare URL corti con gestione degli utenti. Ogni utente può registrarsi, accedere, gestire i propri URL e visualizzare il proprio profilo. Abbiamo integrato HTMX per migliorare l'esperienza utente, rendendo alcune operazioni più dinamiche.

Scrivere test è fondamentale per garantire che l'applicazione funzioni correttamente e per facilitare la manutenzione e l'estensione del codice. Utilizzeremo il framework di test integrato in Django, che si basa su `unittest`. Creeremo test per le principali funzionalità dell'applicazione, inclusi test per i modelli, le viste e i form.

### 1. Test per i Modelli

Crea un file `tests.py` all'interno della tua applicazione `shortener` se non esiste già. Inizia aggiungendo i test per i modelli `UserProfile` e `URL`.

#### tests.py

```python
from django.test import TestCase
from django.contrib.auth.models import User
from .models import UserProfile, URL

class UserProfileModelTest(TestCase):
    def test_user_profile_creation(self):
        user = User.objects.create_user(username='testuser', password='12345')
        user_profile = UserProfile.objects.create(user=user, bio='This is a bio')
        self.assertEqual(user_profile.user.username, 'testuser')
        self.assertEqual(user_profile.bio, 'This is a bio')

class URLModelTest(TestCase):
    def test_url_creation(self):
        user = User.objects.create_user(username='testuser', password='12345')
        short_url = 'short12345'
        url = URL.objects.create(user=user, original_url='http://example.com', short_url=short_url)
        self.assertEqual(url.user.username, 'testuser')
        self.assertEqual(url.original_url, 'http://example.com')
        self.assertEqual(url.short_url, short_url)
        self.assertIsNotNone(url.created_at)
```

### 2. Test per i Form

Proseguiamo aggiungendo i test per i form di registrazione utente e creazione URL.

#### tests.py (continuazione)

```python
from .forms import UserRegistrationForm, URLForm

class UserRegistrationFormTest(TestCase):
    def test_valid_form(self):
        form_data = {
            'username': 'testuser',
            'email': 'testuser@example.com',
            'first_name': 'Test',
            'last_name': 'User',
            'password': '12345',
            'password2': '12345'
        }
        form = UserRegistrationForm(data=form_data)
        self.assertTrue(form.is_valid())

    def test_invalid_form(self):
        form_data = {
            'username': 'testuser',
            'email': 'testuser@example.com',
            'first_name': 'Test',
            'last_name': 'User',
            'password': '12345',
            'password2': '54321'  # passwords don't match
        }
        form = UserRegistrationForm(data=form_data)
        self.assertFalse(form.is_valid())

class URLFormTest(TestCase):
    def test_valid_form(self):
        form_data = {'original_url': 'http://example.com'}
        form = URLForm(data=form_data)
        self.assertTrue(form.is_valid())

    def test_invalid_form(self):
        form_data = {'original_url': 'not a url'}
        form = URLForm(data=form_data)
        self.assertFalse(form.is_valid())
```

### 3. Test per le Viste

Infine, aggiungiamo i test per le viste, verificando che le risposte HTTP siano corrette e che le operazioni come la registrazione, il login e la creazione degli URL funzionino come previsto.

#### tests.py (continuazione)

```python
from django.urls import reverse
from django.contrib.auth import get_user_model

class UserViewTest(TestCase):
    def setUp(self):
        self.user = get_user_model().objects.create_user(username='testuser', password='12345')

    def test_register_view(self):
        response = self.client.get(reverse('register'))
        self.assertEqual(response.status_code, 200)
        self.assertTemplateUsed(response, 'shortener/register.html')

    def test_valid_user_registration(self):
        form_data = {
            'username': 'newuser',
            'email': 'newuser@example.com',
            'first_name': 'New',
            'last_name': 'User',
            'password': '12345',
            'password2': '12345'
        }
        response = self.client.post(reverse('register'), data=form_data)
        self.assertEqual(response.status_code, 302)  # should redirect after successful registration
        self.assertTrue(User.objects.filter(username='newuser').exists())

    def test_login_view(self):
        response = self.client.get(reverse('login'))
        self.assertEqual(response.status_code, 200)
        self.assertTemplateUsed(response, 'shortener/login.html')

    def test_valid_user_login(self):
        response = self.client.post(reverse('login'), {'username': 'testuser', 'password': '12345'})
        self.assertEqual(response.status_code, 302)  # should redirect after successful login

    def test_dashboard_view(self):
        self.client.login(username='testuser', password='12345')
        response = self.client.get(reverse('dashboard'))
        self.assertEqual(response.status_code, 200)
        self.assertTemplateUsed(response, 'shortener/dashboard.html')

class URLViewTest(TestCase):
    def setUp(self):
        self.user = get_user_model().objects.create_user(username='testuser', password='12345')
        self.client.login(username='testuser', password='12345')

    def test_url_creation(self):
        form_data = {'original_url': 'http://example.com'}
        response = self.client.post(reverse('dashboard'), data=form_data)
        self.assertEqual(response.status_code, 302)  # should redirect back to dashboard after successful creation
        self.assertTrue(URL.objects.filter(original_url='http://example.com').exists())

    def test_redirect_url_view(self):
        short_url = 'short12345'
        url = URL.objects.create(user=self.user, original_url='http://example.com', short_url=short_url)
        response = self.client.get(reverse('redirect_url', args=[short_url]))
        self.assertEqual(response.status_code, 302)
        self.assertEqual(response['Location'], 'http://example.com')
```

### Come Eseguire i Test

Puoi eseguire questi test utilizzando il comando `test` di Django:

```sh
python manage.py test
```

Abbiamo scritto test per i modelli, i form e le viste principali dell'applicazione. Questi test aiutano a garantire che le diverse componenti dell'applicazione funzionino correttamente e consentono di individuare rapidamente eventuali regressioni o errori. I test sono una parte fondamentale di qualsiasi progetto software e contribuiscono a mantenere un codice di alta qualità.

### Migliorie

Login sulla radice, è sufficiente modificare url_shortener/urls.py e aggiungi un reindirizzamento per la root dell'applicazione alla vista di login.

```python

from django.contrib import admin
from django.urls import path, include
from django.shortcuts import redirect

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', lambda request: redirect('login')),  # Reindirizza la root alla vista di login
    path('', include('shortener.urls')),
]
```

Per aggiungere un layout di base basato su Bulma CSS al tuo progetto Django, segui questi passaggi. Bulma è un framework CSS moderno e flessibile che offre una struttura pulita e responsiva per la progettazione delle interfacce utente.

### Installazione di Bulma CSS

1. **Installazione di Bulma tramite CDN**:
   La forma più semplice per utilizzare Bulma è includerlo nel tuo template direttamente da un CDN (Content Delivery Network).

   - Apri il tuo file `base.html` (o qualsiasi altro nome tu abbia scelto per il tuo layout di base) nella directory dei template del tuo progetto Django.

   - Aggiungi il seguente link nel tag `<head>` per importare Bulma CSS:

     ```html
     <!DOCTYPE html>
     <html lang="en">
     <head>
         <meta charset="UTF-8">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>Il tuo titolo</title>
         <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">
         <!-- Altri stili personalizzati, script, etc. -->
     </head>
     <body>
     ```

     Assicurati di sostituire `"https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css"` con la versione più recente di Bulma disponibile al momento dell'integrazione nel tuo progetto.

2. **Utilizzo dei Componenti di Pico CSS**:

   Esempio di struttura di base utilizzando PICO CSS

```html
{% load static %}
<!doctype html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="color-scheme" content="light dark" />
    <!-- Fluid viewport -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@2/css/pico.fluid.classless.min.css" />
    <title>URL Shortener</title>
    </head>
    
    <body>
        <main class="container">
            <h1>URL Shortener</h1>
            <!-- Contenuto principale -->
            {% block content %}
            <!-- Contenuto dinamico specifico della pagina -->
            {% endblock %}
        </main>
    </body>
    
    </html>
```

### Integrazione nei Template Django

- Possiamo ora estendere layout di base (`base.html`) nei template specifici di Django utilizzando il tag `{% extends %}` e il blocco `{% block %}` per il contenuto dinamico.

   Esempio di un template che estende il layout di base:

```html
{% extends 'shortener/base.html' %}

{% block content %}
    <h2>Login</h2>
    <form method="post">
        {% csrf_token %}
        <p><label for="username">Username:</label> <input type="text" name="username" required></p>
        <p><label for="password">Password:</label> <input type="password" name="password" required></p>
        <button type="submit">Login</button>
    </form>
    {% if error %}
    <p>{{ error }}</p>
    {% endif %}
{% endblock %}
```
   
 Non mostrerò il codice HTML di tutte le viste, ma sul repository: https://github.com/micheg/django_shortener troverete il progetto complete.