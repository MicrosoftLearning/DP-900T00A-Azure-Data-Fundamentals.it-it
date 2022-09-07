---
lab:
  title: Esplorare Esplora dati di Azure Synapse
  module: Explore fundamentals of real-time analytics
---

# <a name="explore-azure-synapse-data-explorer"></a>Esplorare Esplora dati di Azure Synapse

In questo esercizio si userà Esplora dati di Azure Synapse per analizzare i dati delle serie temporali.

Il completamento di questo lab richiederà circa **25** minuti.

## <a name="before-you-start"></a>Prima di iniziare

Sarà necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free) con accesso di livello amministrativo.

## <a name="provision-a-synapse-analytics-workspace"></a>Effettuare il provisioning di un'area di lavoro di Synapse Analytics

> **Suggerimento**: se è già disponibile un'area di lavoro Azure Synapse da un esercizio precedente, ignorare questa sezione e passare direttamente alla sezione **[Creare un pool di Esplora dati](#create-a-data-explorer-pool)** .

1. Aprire il portale di Azure all'indirizzo [https://portal.azure/com](https://portal.azure.com?azure-portal=true) ed eseguire l'accesso usando le credenziali associate alla sottoscrizione di Azure.

    > <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: Ensure you are working in the directory containing your subscription - indicated at the top right under your user ID. If not, select the user icon and switch directory.

1. Nella **home page** del portale di Azure usare l'icona **&#65291; Crea una risorsa** per creare una nuova risorsa.
1. Cercare *Azure Synapse Analytics* e creare una nuova risorsa **Azure Synapse Analytics** con le impostazioni seguenti:
    - **Sottoscrizione**: *la propria sottoscrizione di Azure*
        - **Gruppo di risorse**: *creare un nuovo gruppo di risorse con un nome appropriato, ad esempio "synapse-rg"*
        - **Gruppo di risorse gestite**: *immettere un nome appropriato, ad esempio "synapse-managed-rg".*
    - **Nome dell'area di lavoro**: *immettere un nome univoco dell'area di lavoro, ad esempio "synapse-ws-<nome_utente>* .
    - **Area**: *selezionare qualsiasi area disponibile*.
    - **Selezionare Data Lake Storage Gen 2**: dalla sottoscrizione 
        - **Nome dell'account**: *creare un nuovo account con un nome univoco, ad esempio "datalake<nome_utente>"* .
        - **Nome file system**: *creare un nuovo file system con un nome univoco, ad esempio "fs<nome_utente>"* .

    > <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: A Synapse Analytics workspace requires two resource groups in your Azure subscription; one for resources you explicitly create, and another for managed resources used by the service. It also requires a Data Lake storage account in which to store data, scripts, and other artifacts.

1. Dopo aver immesso questi dettagli, selezionare **Rivedi e crea**, quindi selezionare **Crea** per creare l'area di lavoro.
1. Attendere che venga creata l'area di lavoro. L'operazione può richiedere circa cinque minuti.
1. Al termine della distribuzione, passare al gruppo di risorse creato e osservare che contiene l'area di lavoro di Synapse Analytics e un account di archiviazione Data Lake.
1. Selezionare l'area di lavoro di Synapse e nella relativa pagina **Panoramica**, nella scheda **Apri Synapse Studio**, selezionare **Apri** per aprire Synapse Studio in una nuova scheda del browser. Synapse Studio è un'interfaccia basata sul Web in cui è possibile usare l'area di lavoro di Synapse Analytics.
1. Sul lato sinistro di Synapse Studio usare l'icona **&rsaquo;&rsaquo;** per espandere il menu. Verranno visualizzate le varie pagine all'interno di Synapse Studio in cui è possibile gestire le risorse ed eseguire attività di analisi dei dati.

## <a name="create-a-data-explorer-pool"></a>Creare un pool di Esplora dati

1. In Synapse Studio selezionare la pagina **Gestisci**.
1. Selezionare la scheda **Pool di Esplora dati** e quindi usare l'icona **&#65291; Nuovo** per creare un nuovo pool con le impostazioni seguenti:
    - **Nome del pool di Esplora dati**: dxpool
    - **Carico di lavoro**: Con ottimizzazione per il calcolo
    - **Dimensioni**: Extra Small (2 core)
1. Selezionare **Avanti: Impostazioni aggiuntive>** e abilitare l'impostazione **Inserimento streaming** per consentire a Esplora dati di inserire nuovi dati da un'origine di streaming, ad esempio Hub eventi di Azure.
1. Selezionare **Rivedi e crea** per creare il pool di Esplora dati e quindi attendere che venga distribuito. Dopo l'operazione, che potrebbe richiedere 15 minuti o più, lo stato passerà da *Creazione in corso* a *Online*.

## <a name="create-a-database-and-ingest-data"></a>Creare un database e inserire dati

1. In Synapse Studio selezionare la pagina **Dati**.
1. Assicurarsi che la scheda **Area di lavoro** sia selezionata e, se necessario, selezionare l'icona **&#8635;** in alto a sinistra della pagina per aggiornare la visualizzazione in modo che l'elenco includa **Database di Esplora dati**.
1. Espandere **Database di Esplora dati** e verificare che **dxpool** sia incluso nell'elenco.
1. Nel riquadro **Dati** usare l'icona **&#65291;** per creare un nuovo **database di Esplora dati** denominato **iot-data** nel pool **dxpool**.
1. Mentre si attende la creazione del database, scaricare il file **devices.csv** da [https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/data/devices.csv](https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/data/devices.csv?azure-portal=true) e salvarlo in qualsiasi cartella nel computer locale.
1. In Synapse Studio attendere che il database venga creato se necessario e quindi nel menu **...** per il nuovo database **iot-data** selezionare **Apri in Esplora dati d Azure**.
1. Nella nuova scheda del browser contenente Esplora dati di Azure selezionare **Inserisci nuovi dati** nella scheda **Dati**.
1. Nella pagina **Destinazione** selezionare le impostazioni seguenti:
    - **Cluster**: *pool di Esplora dati **dxpool** nell'area di lavoro Azure Synapse*
    - **Database**: iot-data
    - **Tabella**: creare una nuova tabella denominata **devices**
1. Selezionare **Avanti: Origine** e nella pagina **Origine** selezionare le opzioni seguenti:
    - **Tipo di origine**: File
    - **File**: caricare il file **devices.csv** dal computer locale.
1. Selezionare **Avanti: Schema** e nella pagina **Schema** assicurarsi che le impostazioni seguenti siano corrette:
    - **Tipo di compressione**: Non compresso
    - **Formato dati**: CSV
    - **Ignora il primo record**: selezionata
    - **Mapping**: devices_mapping
1. Ensure the column data types have been correctly identified as <bpt id="p1">*</bpt>Time (datetime)<ept id="p1">*</ept>, <bpt id="p2">*</bpt>Device (string)<ept id="p2">*</ept>, and <bpt id="p3">*</bpt>Value (long)<ept id="p3">*</ept>). Then select <bpt id="p1">**</bpt>Next: Start Ingestion<ept id="p1">**</ept>.
1. Al termine dell'inserimento, selezionare **Chiudi**.
1. In Esplora dati di Azure verificare nella scheda **Query** che il database **iot-data** sia selezionato e quindi nel riquadro della query immettere la query seguente.

    ```kusto
    devices
    ```

1. Sulla barra degli strumenti selezionare **&#9655; Esegui** per eseguire la query ed esaminare i risultati, che dovrebbero essere simili ai seguenti:

    | Ora | Dispositivo | Valore |
    | --- | --- | --- |
    | 2022-01-01T00:00:00Z | Dev1 | 7 |
    | 2022-01-01T00:00:01Z | Dev2 | 4 |
    | ... | ... | ... |

    Se i risultati corrispondono a questo, la tabella **devices** è stata creata correttamente dai dati presenti nel file.

    > <bpt id="p1">**</bpt>Tip<ept id="p1">**</ept>: In this example, you imported a very small amount of batch data from a file, which is fine for the purposes of this exercise. In reality, you can use Data Explorer to analyze much larger volumes of data; and since you enabled stream ingestion, you could also have configured Data Explorer to ingest data into the table from a streaming source such as Azure Event Hubs.

## <a name="use-kusto-query-language-to-query-the-table-in-synapse-studio"></a>Usare il linguaggio di query Kusto per eseguire query sulla tabella in Synapse Studio

1. Chiudere la scheda del browser relativa a Esplora dati di Azure e tornare alla scheda contenente Synapse Studio.
1. On the <bpt id="p1">**</bpt>Data<ept id="p1">**</ept> page, expand the <bpt id="p2">**</bpt>iot-data<ept id="p2">**</ept> database and its <bpt id="p3">**</bpt>Tables<ept id="p3">**</ept> folder. Then in the <bpt id="p1">**</bpt>...<ept id="p1">**</ept> menu for the <bpt id="p2">**</bpt>devices<ept id="p2">**</ept> table, select <bpt id="p3">**</bpt>New KQL Script<ept id="p3">**</ept><ph id="ph1"> &gt; </ph><bpt id="p4">**</bpt>Take 1000 rows<ept id="p4">**</ept>.
1. Review the generated query and its results. The query should contain the following code:

    ```kusto
    devices
    | take 1000
    ```

    I risultati della query contengono le prime 1.000 righe di dati.

1. Modificare la query come segue:

    ```kusto
    devices
    | where Device == 'Dev1'
    ```

1. Select <bpt id="p1">**</bpt>&amp;#9655; Run<ept id="p1">**</ept> to run the query. Then review the results, which should contain only the rows for the <bpt id="p1">*</bpt>Dev1<ept id="p1">*</ept> device.

1. Modificare la query come segue:

    ```kusto
    devices
    | where Device == 'Dev1'
    | where Time > datetime(2022-01-07)
    ```

1. Eseguire la query ed esaminare i risultati, che devono contenere solo le righe relative al dispositivo *Dev1* successive al 7 gennaio 2022.

1. Modificare la query come segue:

    ```kusto
    devices
    | where Time between (datetime(2022-01-01 00:00:00) .. datetime(2022-07-01 23:59:59))
    | summarize AvgVal = avg(Value) by Device
    | sort by Device asc
    ```

1. Eseguire la query ed esaminare i risultati, che devono contenere il valore medio dei dispositivi registrato tra il 1° gennaio e il 7 gennaio 2022 in ordine crescente di nome di dispositivo.

1. Chiudere la scheda della query KQL e rimuovere le modifiche.

## <a name="delete-azure-resources"></a>Eliminare le risorse di Azure

Dopo aver completato l'esplorazione di Azure Synapse Analytics, è necessario eliminare le risorse create per evitare l'addebito di costi di Azure non necessari.

1. Chiudere la scheda del browser relativa a Synapse Studio senza salvare le modifiche e tornare al portale di Azure.
1. Nella **home page** del portale di Azure selezionare **Gruppi di risorse**.
1. Selezionare il gruppo di risorse per l'area di lavoro Synapse Analytics (non il gruppo di risorse gestite) e verificare che contenga l'area di lavoro Synapse, l'account di archiviazione e il pool di Esplora dati per l'area di lavoro. Se è stato completato l'esercizio precedente, conterrà anche un pool di Spark.
1. Nel parte superiore della pagina **Panoramica** del gruppo di risorse selezionare **Elimina gruppo di risorse**.
1. Immettere il nome del gruppo di risorse per confermare l'eliminazione e selezionare **Elimina**.

    Dopo alcuni minuti, l'area di lavoro di Azure Synapse e l'area di lavoro gestita associata verranno eliminate.
