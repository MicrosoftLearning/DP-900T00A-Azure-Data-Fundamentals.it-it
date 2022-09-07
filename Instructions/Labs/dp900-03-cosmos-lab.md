---
lab:
  title: Esplora Azure Cosmos DB
  module: Explore fundamentals of Azure Cosmos DB
---
# <a name="explore-azure-cosmos-db"></a>Esplora Azure Cosmos DB

In questo esercizio si effettuerà il provisioning di un database di Azure Cosmos DB nella sottoscrizione di Azure e si esploreranno i diversi modi in cui è possibile usarlo per archiviare i dati non relazionali.

Il completamento di questo lab richiederà circa **15** minuti.

## <a name="before-you-start"></a>Prima di iniziare

Sarà necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free) con accesso di livello amministrativo.

## <a name="create-a-cosmos-db-account"></a>Creare un account Cosmos DB

To use Cosmos DB, you must provision a Cosmos DB account in your Azure subscription. In this exercise, you'll provision a Cosmos DB account that uses the core (SQL) API.

1. In the Azure portal, select <bpt id="p1">**</bpt>+ Create a resource<ept id="p1">**</ept> at the top left, and search for <bpt id="p2">*</bpt>Azure Cosmos DB<ept id="p2">*</ept>.  In the results, select <bpt id="p1">**</bpt>Azure Cosmos DB<ept id="p1">**</ept> and select  <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.
1. Nel riquadro **Core (SQL) - Consigliato** selezionare **Crea**.
1. Immettere i dettagli seguenti e quindi selezionare **Rivedi e crea**: 
    - <bpt id="p1">**</bpt>Subscription<ept id="p1">**</ept>: If you're using a sandbox, select <bpt id="p2">*</bpt>Concierge Subscription<ept id="p2">*</ept>. Otherwise, select your Azure subscription.
    - **Gruppo di risorse**: se si sta usando una sandbox, selezionare il gruppo di risorse esistente (che avrà un nome simile a *learn-xxxx...* ). In caso contrario, creare un nuovo gruppo di risorse con il nome desiderato.
    - **Nome account**: immettere un nome univoco
    - **Località**: scegliere una località consigliata
    - **Modalità di capacità**: velocità effettiva con provisioning
    - **Applica sconto livello gratuito**: selezionare Applica, se disponibile
    - **È possibile limitare la velocità effettiva totale dell'account**: opzione deselezionata
1. Una volta convalidata la configurazione, selezionare **Crea**.
1. Wait for deployment to complete. Then go to the deployed resource.

## <a name="create-a-sample-database"></a>Creare un database di esempio

*Per tutta la durata di questa procedura, chiudere eventuali suggerimenti visualizzati nel portale*.

1. Nella pagina del nuovo account Cosmos DB, nel riquadro a sinistra selezionare **Esplora dati**.
1. Nella pagina **Esplora dati** selezionare **Avviare l'avvio rapido**.
1. Nella scheda **Nuovo contenitore** esaminare le impostazioni pre-popolate per il database di esempio e quindi selezionare **OK**.
1. Osservare lo stato nel pannello disponibile nella parte inferiore della schermata fino a quando non saranno stati creati il database **SampleDB** e il contenitore **SampleContainer** (questa operazione può richiedere alcuni minuti).

## <a name="view-and-create-items"></a>Visualizzare e creare elementi

1. In the Data Explorer page, expand the <bpt id="p1">**</bpt>SampleDB<ept id="p1">**</ept> database and the <bpt id="p2">**</bpt>SampleContainer<ept id="p2">**</ept> container, and select <bpt id="p3">**</bpt>Items<ept id="p3">**</ept> to see a list of items in the container. The items represent addresses, each with a unique id and other properties.
1. Selezionare uno degli elementi nell'elenco per visualizzare una rappresentazione JSON dei rispettivi dati.
1. Nella parte superiore della pagina selezionare **Nuovo elemento** per creare un nuovo elemento vuoto.
1. Modificare il file JSON relativo al nuovo elemento come indicato di seguito e quindi selezionare **Salva**.

    ```json
    {
        "address": "1 Any St.",
        "id": "123456789"
    }
    ```

1. Dopo aver salvato il nuovo elemento, osservare come siano state automaticamente aggiunte altre proprietà dei metadati.

## <a name="query-the-database"></a>Eseguire query sul database

1. Nella pagina **Esplora dati** selezionare l'icona **Nuova query SQL**.
1. Nell'editor di query SQL controllare la query predefinita (`SELECT * FROM c`) e usare il pulsante **Esegui query** per eseguirla.
1. Esaminare i risultati, in cui è inclusa anche la rappresentazione JSON completa di tutti gli elementi.
1. Modificare la query come segue:

    ```sql
    SELECT c.id, c.address
    FROM c
    WHERE CONTAINS(c.address, "Any St.")
    ```

1. Usare il pulsante **Esegui query** per eseguire la query aggiornata ed esaminare i risultati, che includono le entità JSON per tutti gli elementi con un campo **address** contenente il testo "Any St."
1. Chiudere l'editor di query SQL ignorando le modifiche.

    You've seen how to create and query JSON entities in a Cosmos DB database by using the data explorer interface in the Azure portal. In a real scenario, an application developer would use one of the many programming language specific software development kits (SDKs) to call the core (SQL) API and work with data in the database.

> **Suggerimento**: se è stata completata l'esplorazione di Azure Cosmos DB, è possibile eliminare il gruppo di risorse creato in questo esercizio.
