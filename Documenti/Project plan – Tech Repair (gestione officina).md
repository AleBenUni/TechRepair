# Project plan – Tech Repair (gestione officina)



Tech Repair è il sistema che il nostro team di quattro persone sviluppa per il corso di Ingegneria del software (AA 2026/27); questo project plan ne fissa processo, ruoli, rischi e calendario.



## Versioni

|Versione|Data|Modifiche|
|-|-|-|
|1.0.0|12/10/2026|Versione iniziale|
|1.0.1|13/10/2026|Aggiunti i work package; ore settimanali, sprint e date ricalcolati (progetto quasi pronto il 13 dicembre, consegna entro l'8 gennaio); interfaccia solo console; repository creato da AleBenUni; regole su pull request e review, board GitHub, codice generato e scenari di eccezione|

## 

## 1.Introduction

Tech Repair gestisce il percorso di un dispositivo in riparazione, dall'accettazione in officina alla consegna e al pagamento.



**Scopo del documento**

Pianificare come sviluppiamo il sistema: processo, organizzazione, rischi, risorse e calendario. Il piano è condiviso con il professore e l'esercitatrice tramite issue GitHub per l'approvazione.

**Attori.** Il sistema ha tre attori: il Cliente, il Tecnico Riparatore e il Responsabile Magazzino.



**Funzionalità principali**

* Accettazione del dispositivo, creazione della scheda di riparazione e generazione della ricevuta di ingresso
* Diagnosi del guasto, invio del preventivo e approvazione da parte del cliente
* Ordine del pezzo di ricambio quando non è presente in magazzino
* Consegna del dispositivo riparato e registrazione del pagamento



**Flussi di eccezione**

Se il cliente rifiuta il preventivo, la scheda passa ad "Annullato" e si addebita solo il costo di diagnosi. Se il pezzo di ricambio è fuori produzione, il sistema notifica l'impossibilità di riparare.



**Perimetro**

Rientra tutto il flusso sopra, con dati persistiti in un database embedded e interfaccia solo a riga di comando (console), senza interfaccia grafica. Restano fuori pagamenti reali, invio reale di email o SMS (le notifiche sono simulate) e contabilità.

**Riferimenti.** Requisiti per il progetto di ingegneria del software AA 2026/27 (Gargantini, Bonfanti); materiale del corso, incluso il capitolo 2 del libro.

## 

## 2.Process model

Seguiamo un processo iterativo e incrementale a sprint di due settimane (lo sprint 0 dura una settimana), in cui requisiti e modelli vengono raffinati a ogni iterazione; il progetto è quasi completo il 13 dicembre 2026.



**Perché questo processo**

Il team è piccolo e ha poche ore a testa, quindi servono iterazioni brevi e verificabili. Il corso chiede di spendere almeno il 70% del tempo su requisiti, modellazione e progettazione, quindi i modelli UML precedono il codice. Lavorare a sprint ci permette di ricevere feedback dal professore tramite issue prima di consolidare le scelte.



**Ciclo di ogni sprint**

1. Pianificazione: scegliamo le issue dello sprint e le assegniamo sulla board GitHub
2. Lavoro su branch dedicati, con pull request e code review
3. Chiusura: verifica dei criteri di accettazione e retrospettiva breve



**Obiettivi per sprint** (date e ore nella sezione 12).

* Sprint 0 (12-18 ott, 16 ore di team): setup del repository, project plan, avvio dei requisiti
* Sprint 1 (19 ott-1 nov, 32 ore): specifica dei requisiti, use case diagram, class diagram
* Sprint 2 (2-15 nov, 32 ore): state machine, sequence, communication o timing e activity diagram, prima generazione del codice da StarUML, prime viste architetturali
* Sprint 3 (16-29 nov, 32 ore): architettura (component e package diagram), design pattern, implementazione del nucleo
* Sprint 4 (30 nov-13 dic, 32 ore): implementazione completa, test JUnit, copertura e metriche, refactoring e documenti finali; il progetto è quasi pronto il 13 dicembre
* Sprint 5 (14 dic-8 gen, nessuna ora pianificata): margine per correzioni, revisione incrociata, prova su clone pulito e consegna entro l'8 gennaio

Le differenze tra questo piano e il processo realmente seguito saranno riportate nel documento di gestione del progetto.

## 

## 3.Organization of the project

Il team è composto da quattro persone, ciascuna con un'area di responsabilità specifica, operando in una struttura collaborativa senza una gerarchia rigida



**Struttura interna**

Tutte le decisioni operative e architetturali vengono prese per consenso all'interno del team. Nel caso in cui non si raggiunga un accordo entro la riunione settimanale, la decisione finale spetta al Project Manager. Quest'ultimo ha l'obbligo di motivare formalmente la scelta intrapresa tramite un commento dedicato all'interno dell'issue di riferimento



**Interfacce esterne**

* Docenti di riferimento: Il Prof. Gargantini e la Prof.ssa Bonfanti dispongono dell'accesso completo al repository GitHub del progetto. Le richieste di approvazione formale e i feedback vengono gestiti tramite GitHub
* Project Plan: Il project plan deve essere formalmente approvato dal professore almeno un mese prima della data d'esame prevista





**Comunicazione**

* GitHub: Canale ufficiale ed esclusivo per il tracciamento delle decisioni, l'inoltro delle richieste di modifica al codice o ai modelli, e lo svolgimento delle attività di code review
* Riunione settimanale: Incontro periodico del team finalizzato all'allineamento sullo stato di avanzamento delle attività (stato dei task sulla lavagna Kanban) e alla pianificazione degli obiettivi futuri
* Chat di gruppo: Utilizzata unicamente per comunicazioni rapide, urgenze operative o scambi informativi interni. Questo canale non ha alcuna validità decisionale ai fini dello sviluppo del progetto

## 

## 4.Standards, guidelines, procedures

Tutto il lavoro passa da GitHub e segue regole comuni su repository, codice, modelli e documenti, per rendere chiaro chi ha fatto cosa.



**Repository e cartelle**

* Proprietà del Repository: Creato dall'account AleBenUni e condiviso con i professori Gargantini e Bonfanti. La root del repository prende il nome del software (Tech Repair) e non deve contenere file di configurazione dell'IDE (es. .project)
* Struttura delle cartelle:

  * documenti/: Contiene la documentazione ufficiale e il file di progetto StarUML
  * codice/: Contiene i progetti Eclipse
* Nomenclatura progetti Eclipse: Devono tassativamente iniziare con la sigla TR\_ (es. TR\_core, TR\_console, TR\_database). Sono vietati nomi generici
* Gestione Gitignore: Il file .gitignore deve escludere i file .class e la cartella target/. I file .project, .classpath e pom.xml devono essere sempre committati per garantire l'allineamento dell'ambiente di sviluppo



**Procedura git e Kanban**

* Branch 'main' stabile: Il ramo main rappresenta il codice di produzione stabile. Nessuna modifica viene effettuata direttamente su di esso
* Apertura dei Branch: Ogni attività parte da un Issue. Il branch associato deve essere creato direttamente dall'interfaccia web dell'issue su GitHub, accettando la nomenclatura automatica predefinita
* Commit piccoli e frequenti: Ogni commit deve avere un titolo esplicativo ed eventuale descrizione dettagliata. Sono vietati messaggi generici
* Una pull request per ogni branch: Ogni branch richiede l'apertura di una Pull Request (PR), che risulterà nativamente collegata all'issue di origine grazie alla creazione guidata del ramo
* #### Gestione file StarUML (.mdj): Essendo un file unico e non integrabile via merge testuale, è tassativo lavorarci una sola persona alla volta

  * #### Chi inizia a lavorarci deve "prenotarlo" con un commento nell'issue dedicato
  * #### Nessun altro può modificare il modello finché l'issue associato non passa nello stato di In Review
  * #### È obbligatorio eseguire un git pull immediatamente prima di aprire StarUML



**Pull request e review**

* Nessun push diretto su 'main': Ogni modifica passa da una pull request
* Approvazione mirata: Per poter effettuare il merge, serve l'approvazione del Project Manager. In caso di sua indisponibilità, l'approvazione può essere concessa da un membro del team diverso dall'autore, scelto in base alla competenza specifica del task
* Strategia di Merge: Il merge viene eseguito solo dopo aver ottenuto l'approvazione. Si utilizza il merge normale (Create a merge commit) e non lo squash, per mantenere intatta la cronologia dei singoli commit nella storia del progetto
* Statistiche finali: A fine progetto, il documento di gestione riporterà i dati analitici su commit, PR aperte e review effettuate per ciascun componente del team



**Codice**

* Tecnologie: Linguaggio Java (adottando le convenzioni standard) e progetti gestiti tramite Maven con la suite di test posizionata in 'src/test/java'
* Portabilità: Divieto assoluto di inserire percorsi (path) assoluti. Il database deve essere di tipo embedded e l'applicazione non deve dipendere da servizi esterni da installare localmente
* Architettura del codice: Package coesi e privi di cicli di dipendenza. Rispetto del principio dell'information hiding tramite l'uso appropriato dei modificatori 'private' e 'public'. Uso sistematico di interfacce, classi astratte e dell'annotazione @Override dove necessario
* Tracciamento: Logging dell'applicazione gestito tramite Log4j, con la relativa dipendenza configurata nel 'pom.xml' di Maven



**Modelli e documenti**

* Modellazione UML: Gestita tramite StarUML 5. Il file di progetto contenente tutti i diagrammi deve essere salvato nel repository
* Documentazione finale: Tutta la documentazione ufficiale viene organizzata e consegnata in un unico file PDF strutturato a capitoli, contenente le immagini dei diagrammi UML esportate direttamente nel testo

## 

## 5\. Management activities

La strategia di gestione pone come priorità assoluta un'analisi e una progettazione solide, seguite da un'implementazione funzionante dei flussi principali del sistema. Il progetto deve essere in stato di quasi completo completamento entro il 13 dicembre 2026, con consegna definitiva fissata entro l'8 gennaio 2027



**Obiettivi in ordine di priorità**

1. Requisiti e modelli UML: Sviluppo di modelli completi, coerenti e non banali (assorbono circa il 70% del monte ore totale)
2. Implementazione software: Sviluppo funzionante dei flussi principali dell'applicazione Tech Repair
3. Utilizzo effettivo di GitHub: Applicazione rigorosa del flusso di lavoro tramite milestone, issue, branch, pull request e attività di code review
4. Qualità del codice: Scrittura di test JUnit, misurazione della code coverage e monitoraggio delle metriche del codice



**Assunzioni**

* Impegno orario: Ogni membro del team dedica circa 4 ore a settimana per 9 settimane (dal 12 ottobre al 13 dicembre 2026), per un totale stimato di 36 ore pro capite, rispettando la forchetta di 30-40 ore indicata dal corso
* Standardizzazione: Tutti i componenti del team utilizzano i medesimi strumenti di sviluppo e la stessa struttura concordata per il repository
* Fattori esterni (Dipendenze): La pianificazione temporale è strettamente subordinata alla data di approvazione del Project Plan, alla calendarizzazione della presentazione orale e alle sessioni d'esame degli altri insegnamenti universitari



**Monitoraggio e reporting (GitHub Projects)**

* Bacheca Kanban:

  * ToDo board: Vista operativa principale organizzata che mappa visivamente i task dall'ideazione fino alla chiusura

    * Backlog: Raccolta iniziale di tutti gli issue e delle idee
    * Ready: Task rifiniti e pronti per essere presi in carico dal team
    * In Progress: Attività attualmente in fase di sviluppo
    * In Review: Codice o modelli sotto revisione tramite Pull Request
    * Done: Task completati e validati
  * Team items: Panoramica globale che mostra tutti gli issue del progetto, i rispettivi assegnatari e la suddivisione del lavoro organizzata per ciascuna milestone
  * My items: Vista personalizzata filtrata esclusivamente sugli issue assegnati al singolo utente, raggruppati in base alla milestone di riferimento
  * Roadmap: Visualizzazione cronologica che ordina e traccia nel tempo la pianificazione di tutti gli issue lungo una linea temporale
* Registro ore: Registro contenente le ore di lavoro suddiviso in milestone e assegnatari

  * Ore stimate: Ore stimate per il completamento dell'issue
  * Ore effettive: Ore impiegate per il completamento dell'issue



**Rituali di controllo**

* Allineamento settimanale: Riunione periodica volta a verificare lo stato di avanzamento dei task e a ridistribuire le attività in caso di colli di bottiglia

## 

## 6\. Risks

I rischi più pesanti sono la sottostima del tempo di modellazione e la distribuzione non uniforme del carico; il registro viene rivisto a ogni fine sprint.

|Rischio|Probabilità|Impatto|Mitigazione|Responsabile|
|-|-|-|-|-|
|Sottostima del tempo di modellazione|Alta|Alto|Buffer nello sprint 2, review dei diagrammi a metà sprint|Architetto|
|Diagrammi UML troppo semplici|Media|Alto|Checklist degli elementi visti a lezione per state machine, sequence e activity; review incrociata|Analista dei requisiti|
|Carico di lavoro non uniforme tra i membri|Media|Alto|Issue assegnate esplicitamente, registro ore, controllo settimanale|Project manager|
|Implementazione frammentaria|Media|Alto|Perimetro ridotto, priorità ai flussi principali, test sui flussi|Responsabile sviluppo|
|Sovrapposizione con gli esami di altri corsi|Alta|Medio|Calendario condiviso, sprint più leggeri nelle settimane d'esame, margine dello sprint 5 (14 dicembre-8 gennaio)|Project manager|
|Uso scorretto di git, conflitti di merge|Media|Medio|Branch per issue, pull request obbligatorie, breve formazione iniziale|Project manager|
|Cicli tra package nel codice|Media|Medio|Controllo con JDepend o Structure101 a fine sprint|Architetto|
|File StarUML o .project non committati|Bassa|Alto|Commit regolari, prova di clone pulito prima della consegna|Project manager|

## 

## 7\. Staffing

Quattro persone con ruoli di responsabilità distinti, ma tutte coinvolte in modellazione, codice e test, per circa 36 ore ciascuna (4 ore a settimana per 9 settimane).

|Ruolo|Responsabilità principali|Membro|
|-|-|-|
|Project manager e configuration manager|Pianificazione, board, issue, release, ordine del repository, registro ore|Matteo Testa|
|Analista dei requisiti|Specifica dei requisiti, use case, scenari ed eccezioni|Alice Rota|
|Architetto|Architettura, class, component e package diagram, design pattern|Mattia Maggioni|
|Responsabile sviluppo e test|Implementazione, test JUnit, copertura, metriche|Alessandro Benigni|

I ruoli indicano chi risponde di un'area, non chi la svolge da solo: ogni diagramma e ogni classe passano per la review di almeno un'altra persona.

Ogni membro deve dare un contributo significativo. A fine progetto ciascuno valuta in privato il proprio impegno e quello dei compagni, come previsto dal corso.

## 

## 8\. Methods and techniques

Usiamo i metodi visti a lezione per ogni attività, con UML come linguaggio comune tra requisiti, design e codice.

* **Requisiti:** Analisi del dominio dell'officina attraverso scenari d'uso dei tre attori, specifica secondo IEEE 830, use case con scenario principale ed eccezioni; ogni flusso di eccezione (per esempio preventivo rifiutato, pezzo fuori produzione) diventa un flusso alternativo di uno use case, una transizione della state machine, un frammento alt del sequence diagram e almeno un test JUnit, con tracciabilità tra i documenti Requisiti e Testing
* **Modellazione:** UML con StarUML 5: use case, class, state machine, sequence, communication o timing, activity, component e package diagram
* **Generazione del codice:** Prima versione delle classi Java generata una sola volta dal class diagram con StarUML, a modello stabile (fine sprint 2), per non sovrascrivere codice scritto a mano; poi completata a mano, compresi tutti i corpi dei metodi. La generazione ha un commit dedicato e il Documento 4 (design) riporta l'elenco delle classi generate, con package e modifiche manuali successive
* **Design:** Almeno due design pattern visti a lezione; candidati: State per la scheda di riparazione, Observer per le notifiche al cliente, Strategy per il calcolo dei costi
* **Implementazione:** Java moderno, Maven, log4j, database embedded, interfaccia solo a riga di comando (console)
* #### **Test.** JUnit per i test di unità, con misura di copertura; un test per ogni flusso alternativo degli use case, con l'elenco di test, scenario ed esito atteso nel documento di testing
* #### **Qualità del codice.** Metriche con gli strumenti visti a lezione (JDepend, Structure101, SonarLint, PMD)
* **Refactoring:** Attività svolte e documentate durante lo sprint 4, con eventuali correzioni nello sprint 5
* **Configuration management:** GitHub con issue, branch, pull request e code review

## 

## 9\. Quality assurance

La qualità si controlla con revisioni sistematiche, test automatici e metriche, verificati a ogni fine sprint

* **Revisioni:**

  * Ogni pull request è rivista da almeno un altro membro prima del merge
  * Ogni diagramma UML è controllato con una checklist degli elementi visti a lezione
  * Coerenza tra modelli, codice e documenti verificata a fine sprint
* **Test:**

  * Test JUnit per le classi e per i flussi principali
* ##### **Metriche:** Nessun ciclo tra package, complessità sotto controllo e avvisi di SonarLint e PMD esaminati e risolti o motivati.
* ##### **Criteri di accettazione di uno sprint:**

  * ##### La build Maven passa da zero su un clone pulito del repository
  * ##### Le issue dello sprint sono chiuse o riassegnate con motivazione
  * ##### I documenti dello sprint sono aggiornati e committati

## 

## 10\. Work packages

Il lavoro è diviso in sette work package, ciascuno con ore, sprint e responsabile; la somma delle ore coincide con il budget di 144 ore

* **WP1 – Gestione e setup** (14 ore, sprint 0 e riepiloghi in ogni sprint; Project manager). Configurazione del repository, board, project plan, registro ore. Deliverable: project plan 1.0.0 e repository configurato
* **WP2 – Requisiti** (22 ore, sprint 0 e 1; Analista dei requisiti). Elicitazione, specifica secondo IEEE 830, use case con scenari ed eccezioni. Deliverable: documento dei requisiti e use case diagram
* **WP3 – Modellazione UML** (35 ore, sprint 1 e 2; Architetto). Class diagram, state machine, sequence, communication o timing e activity diagram, prima generazione del codice da StarUML Deliverable: progetto StarUML con i diagrammi e prime classi Java generate
* **WP4 – Architettura e design** (30 ore, sprint 2 e 3; Architetto). Viste architetturali, component e package diagram, stile architetturale, design pattern, libreria esterna Maven Deliverable: documento di architettura e design
* **WP5 – Implementazione** (24 ore, sprint 3 e 4; Responsabile sviluppo e test). Progetti Eclipse Maven, completamento del codice generato, database embedded, logging, interfaccia a riga di comando. Deliverable: codice funzionante dei flussi principali
* **WP6 – Testing** (10 ore, sprint 4; Responsabile sviluppo e test). Test JUnit, misura di copertura, metriche sul codice. Deliverable: suite di test e documento di testing
* **WP7 – Rifinitura e presentazione** (9 ore, sprint 4; Project manager). Refactoring documentato, documenti finali, README, prova su clone pulito, presentazione. Deliverable: repository pronto per la consegna e slide

Ogni work package parte dai deliverable del precedente (requisiti, modelli, design, codice, test); gestione e rifinitura accompagnano l'intero progetto

## 

## 11\. Resources

Le risorse sono quattro persone per circa 36 ore ciascuna e strumenti tutti gratuiti, quindi il budget si misura solo in ore

* **Persone:** Quattro membri, 144 ore in totale (sezione 12)
* **Sviluppo:** JDK, Eclipse, Maven, JUnit, log4j come dipendenza Maven, database embedded, interfaccia solo a riga di comando
* **Modellazione:** StarUML 5, versione gratuita
* **Collaborazione:** GitHub per repository, issue, project board, pull request e code review
* **Analisi del codice:** Strumenti di metriche e copertura
* **Hardware:** I computer personali dei membri e un PC dedicato per la demo all'esame orale

## 

## 12\. Budget and schedule

Il budget è di 144 ore (36 a testa: 4 ore a settimana per 9 settimane, dal 12 ottobre al 13 dicembre) e almeno il 70% va a gestione, requisiti, modellazione e design

* Le ore sono una stima iniziale: Le aggiorniamo a fine sprint con il registro ore. La forchetta di 30-40 ore del corso equivale a 3/4 ore a settimana
* Il calendario proposto copre sei sprint: I primi cinque (dal 12 ottobre al 13 dicembre 2026) portano il progetto quasi a compimento; lo sprint 5 (14 dicembre/8 gennaio) copre le vacanze natalizie ed è un margine per correzioni, revisione e consegna
* La consegna interna è fissata all'8 gennaio 2027. Il progetto completo va consegnato almeno cinque giorni prima della presentazione, quindi la presentazione non può cadere prima del 13 gennaio 2027

## 

## 13\. Changes

Ogni modifica a requisiti, piano o documenti nasce come issue GitHub e passa da una pull request, così resta tracciata

**Richieste di modifica:**

1. Chi propone apre un'issue con motivo, impatto su requisiti, modelli, codice e ore
2. Il project manager, sentito il team, valuta la richiesta 
3. La modifica approvata viene implementata tramite un branch e rivista con pull request

**Versioning dei documenti:** Il project plan ha una tabella delle versioni in testa: Ogni revisione aggiunge una riga con data e modifiche. I documenti nel repository sono versionati con git, quindi la cronologia dei commit fa da storico.

## 

## 14\. Delivery

Consegniamo un repository GitHub completo e funzionante, con tutta la documentazione, almeno cinque giorni prima della presentazione.

**Cosa consegniamo:**

* Project plan, approvato dal professore almeno un mese prima dell'esame
* Relazione finale in un unico PDF diviso in capitoli: project plan, gestione del progetto, requisiti, design, testing, maintenance
* Progetti Eclipse Maven con codice, test JUnit e istruzioni per eseguirli
* File StarUML con tutti i diagrammi

**Come:**

* Tutto committato nel repository condiviso con Gargantini e Bonfanti
* Prima della consegna, prova su un clone pulito: build Maven e test devono passare da zero ................
* Dopo la consegna si possono correggere eventuali errori, senza creare nuovi documenti né nuovi progetti Java

**Presentazione:** Il tempo a disposizione per quattro persone è di 35 minuti, più circa 10 per le domande. Portiamo un PC con il progetto in esecuzione per demo ed esecuzione dei test.

