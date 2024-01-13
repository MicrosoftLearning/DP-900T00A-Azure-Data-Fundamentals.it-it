---
lab:
  title: Esplorare Azure Cosmos DB
  module: Explore fundamentals of Azure Cosmos DB
---
# Esplorare Azure Cosmos DB

In questo esercizio si effettuerà il provisioning di un database di Azure Cosmos DB nella sottoscrizione di Azure e si esploreranno i diversi modi in cui è possibile usarlo per archiviare i dati non relazionali.

Il completamento di questo lab richiederà circa **15** minuti.

## Prima di iniziare

Sarà necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free) con accesso di livello amministrativo.

## Creare un account Cosmos DB

Per usare Cosmos DB, è necessario effettuare il provisioning di un account Cosmos DB in una sottoscrizione di Azure. In questo esercizio si effettuerà il provisioning di un account Cosmos DB che usa Azure Cosmos DB for NoSQL.

1. Nel portale di Azure selezionare **Crea una risorsa** in alto a sinistra e cercare *Azure Cosmos DB*.  Nei risultati selezionare **Azure Cosmos DB** e quindi **Crea**.
1. Nel riquadro **Azure Cosmos DB for NoSQL** selezionare **Crea**.
1. Immettere i dettagli seguenti e quindi selezionare **Rivedi e crea**:
    - **Sottoscrizione**: se si sta usando una sandbox, selezionare *Concierge Subscription* (Sottoscrizione Concierge). In caso contrario, selezionare la sottoscrizione di Azure personale.
    - **Gruppo di risorse**: se si sta usando una sandbox, selezionare il gruppo di risorse esistente (che avrà un nome simile a *learn-xxxx...*). In caso contrario, creare un nuovo gruppo di risorse con il nome desiderato.
    - **Nome account**: immettere un nome univoco
    - **Località**: scegliere una località consigliata
    - **Modalità di capacità**: velocità effettiva con provisioning
    - **Applica sconto livello gratuito**: selezionare Applica, se disponibile
    - **È possibile limitare la velocità effettiva totale dell'account**: opzione deselezionata
1. Una volta convalidata la configurazione, selezionare **Crea**.
1. Attendere il completamento della distribuzione. Passare quindi alla risorsa distribuita.

## Creare un database di esempio

*Per tutta la durata di questa procedura, chiudere eventuali suggerimenti visualizzati nel portale*.

1. Nella pagina del nuovo account Cosmos DB, nel riquadro a sinistra selezionare **Esplora dati**.
1. Nella pagina **Esplora dati** selezionare **Avviare l'avvio rapido**.
1. Nella scheda **Nuovo contenitore** esaminare le impostazioni pre-popolate per il database di esempio e quindi selezionare **OK**.
1. Osservare lo stato nel pannello disponibile nella parte inferiore della schermata fino a quando non saranno stati creati il database **SampleDB** e il contenitore **SampleContainer** (questa operazione può richiedere alcuni minuti).

## Visualizzare e creare elementi

1. Nella pagina Esplora dati espandere il database **SampleDB** e il contenitore **SampleContainer** e selezionare **Elementi** per visualizzare l'elenco degli elementi disponibili nel contenitore. Gli elementi rappresentano dati di prodotto, ognuno con un ID univoco e altre proprietà.
1. Selezionare uno degli elementi nell'elenco per visualizzare una rappresentazione JSON dei rispettivi dati.
1. Nella parte superiore della pagina selezionare **Nuovo elemento** per creare un nuovo elemento vuoto.
1. Modificare il file JSON relativo al nuovo elemento come indicato di seguito e quindi selezionare **Salva**.

    ```json
    {
        "name": "Road Helmet,45",
        "id": "123456789",
        "categoryID": "123456789",
        "SKU": "AB-1234-56",
        "description": "The product called \"Road Helmet,45\" ",
        "price": 48.74
    }
    ```

1. Dopo aver salvato il nuovo elemento, osservare come siano state automaticamente aggiunte altre proprietà dei metadati.

## Eseguire query sul database

1. Nella pagina **Esplora dati** selezionare l'icona **Nuova query SQL**.
1. Nell'editor di query SQL controllare la query predefinita (`SELECT * FROM c`) e usare il pulsante **Esegui query** per eseguirla.
1. Esaminare i risultati, in cui è inclusa anche la rappresentazione JSON completa di tutti gli elementi.
1. Modificare la query come segue:

    ```sql
    SELECT *
    FROM c
    WHERE CONTAINS(c.name,"Helmet")
    ```

1. Usare il pulsante **Esegui query** per eseguire la query aggiornata ed esaminare i risultati, che includono le entità JSON per tutti gli elementi con un campo **name** contenente il testo "Helmet".
1. Chiudere l'editor di query SQL ignorando le modifiche.

    È stata illustrata la procedura per creare ed eseguire query su entità JSON in un database Cosmos DB usando l'interfaccia Esplora dati nel portale di Azure. In uno scenario reale, uno sviluppatore di applicazioni userebbe uno dei molti SDK (Software Development Kit) specifici dei linguaggi di programmazione per chiamare l'API NoSQL ed eseguire operazioni sui dati nel database.

> **Suggerimento**: se è stata completata l'esplorazione di Azure Cosmos DB, è possibile eliminare il gruppo di risorse creato in questo esercizio.
