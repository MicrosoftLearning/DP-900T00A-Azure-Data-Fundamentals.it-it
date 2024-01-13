---
lab:
  title: Esplorare Esplora dati di Azure Synapse
  module: Explore fundamentals of real-time analytics
---

# Esplorare Esplora dati di Azure Synapse

> **Nota**: a causa delle modifiche apportate al prodotto, esistono alcuni problemi noti relativi alla sezione **Creare un database e inserire i dati** di questo lab. Stiamo lavorando per risolvere questi problemi.

In questo esercizio si userà Esplora dati di Azure Synapse per analizzare i dati delle serie temporali.

Il completamento di questo lab richiederà circa **25** minuti.

## Prima di iniziare

Sarà necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free) con accesso di livello amministrativo.

## Effettuare il provisioning di un'area di lavoro di Synapse Analytics

> **Suggerimento**: se è già disponibile un'area di lavoro Azure Synapse da un esercizio precedente, ignorare questa sezione e passare direttamente alla sezione **[Creare un pool di Esplora dati](#create-a-data-explorer-pool)**.

1. Aprire il portale di Azure all'indirizzo [https://portal.azure/com](https://portal.azure.com?azure-portal=true) ed eseguire l'accesso usando le credenziali associate alla sottoscrizione di Azure.

    > **Nota**: assicurarsi di essere nella directory relativa alla sottoscrizione personale, indicata in alto a destra sotto l'ID utente. In caso contrario, selezionare l'icona utente e passare alla directory appropriata.

1. Nella **home page** del portale di Azure usare l'icona **&#65291; Crea una risorsa** per creare una nuova risorsa.
1. Cercare *Azure Synapse Analytics* e creare una nuova risorsa **Azure Synapse Analytics** con le impostazioni seguenti:
    - **Sottoscrizione**: *la sottoscrizione di Azure in uso*.
        - **Gruppo di risorse**: *creare un nuovo gruppo di risorse con un nome appropriato, ad esempio "synapse-rg"*
        - **Gruppo di risorse gestite**: *immettere un nome appropriato, ad esempio "synapse-managed-rg".*
    - **Nome dell'area di lavoro**: *immettere un nome univoco dell'area di lavoro, ad esempio "synapse-ws-<nome_utente>*.
    - **Area**: *selezionare qualsiasi area disponibile*.
    - **Selezionare Data Lake Storage Gen 2**: dalla sottoscrizione
        - **Nome dell'account**: *creare un nuovo account con un nome univoco, ad esempio "datalake<nome_utente>"*.
        - **Nome file system**: *creare un nuovo file system con un nome univoco, ad esempio "fs<nome_utente>"*.

    > **Nota**: per un'area di lavoro di Synapse Analytics sono necessari due gruppi di risorse nella sottoscrizione di Azure, uno per le risorse create in modo esplicito e un altro per le risorse gestite usate dal servizio. È inoltre necessario un account di archiviazione Data Lake in cui archiviare dati, script e altri artefatti.

1. Dopo aver immesso questi dettagli, selezionare **Rivedi e crea**, quindi selezionare **Crea** per creare l'area di lavoro.
1. Attendere che venga creata l'area di lavoro. L'operazione può richiedere circa cinque minuti.
1. Al termine della distribuzione, passare al gruppo di risorse creato e osservare che contiene l'area di lavoro di Synapse Analytics e un account di archiviazione Data Lake.
1. Selezionare l'area di lavoro di Synapse e nella relativa pagina **Panoramica**, nella scheda **Apri Synapse Studio**, selezionare **Apri** per aprire Synapse Studio in una nuova scheda del browser. Synapse Studio è un'interfaccia basata sul Web in cui è possibile usare l'area di lavoro di Synapse Analytics.
1. Sul lato a sinistra di Synapse Studio usare l'icona **&rsaquo;&rsaquo;** per espandere il menu. Verranno visualizzate le varie pagine all'interno di Synapse Studio in cui è possibile gestire le risorse ed eseguire attività di analisi dei dati.

## Creare un pool di Esplora dati

1. In Synapse Studio selezionare la pagina **Gestisci**.
1. Selezionare la scheda **Pool di Esplora dati** e quindi usare l'icona **&#65291; Nuovo** per creare un nuovo pool con le impostazioni seguenti:
    - **Nome del pool di Esplora dati**: dxpool
    - **Carico di lavoro**: Con ottimizzazione per il calcolo
    - **Dimensioni**: Extra Small (2 core)
1. Selezionare **Avanti: Impostazioni aggiuntive>** e abilitare l'impostazione **Inserimento streaming** per consentire a Esplora dati di inserire nuovi dati da un'origine di streaming, ad esempio Hub eventi di Azure.
1. Selezionare **Rivedi e crea** per creare il pool di Esplora dati e quindi attendere che venga distribuito. Dopo l'operazione, che potrebbe richiedere 15 minuti o più, lo stato passerà da *Creazione in corso* a *Online*.

## Creare un database e inserire dati

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
1. Assicurarsi che i tipi di dati delle colonne siano stati identificati correttamente come *Ora (datetime)*, *Dispositivo (string)* e *Valore (long)*. Selezionare quindi **Avanti: Avvia inserimento**.
1. Al termine dell'inserimento, selezionare **Chiudi**.
1. In Esplora dati di Azure verificare nella scheda **Query** che il database **iot-data** sia selezionato e quindi nel riquadro della query immettere la query seguente.

    ```kusto
    devices
    ```

1. Sulla barra degli strumenti selezionare **&#9655; Esegui** per eseguire la query ed esaminare i risultati, che dovrebbero essere simili ai seguenti:

    | Time | Dispositivo | valore |
    | --- | --- | --- |
    | 2022-01-01T00:00:00Z | Dev1 | 7 |
    | 2022-01-01T00:00:01Z | Dev2 | 4 |
    | ... | ... | ... |

    Se i risultati corrispondono a questo, la tabella **devices** è stata creata correttamente dai dati presenti nel file.

    > **Suggerimento**: in questo esempio è stata importata una quantità molto ridotta di dati batch da un file e questa operazione è appropriata ai fini di questo esercizio. In realtà, è possibile usare Esplora dati per analizzare volumi di dati di dimensioni maggiori e, poiché è stato abilitato l'inserimento di flussi, è anche possibile configurare Esplora dati in modo da inserire dati nella tabella da un'origine di streaming, ad esempio Hub eventi di Azure.

## Usare il linguaggio di query Kusto per eseguire query sulla tabella in Synapse Studio

1. Chiudere la scheda del browser relativa a Esplora dati di Azure e tornare alla scheda contenente Synapse Studio.
1. Nella pagina **Dati** espandere il database **iot-data** e la relativa cartella **Tabelle**. Nel menu **...** relativo alla tabella **devices** selezionare **Nuovo script KQL** > **Accettare 1.000 righe**.
1. Esaminare la query generata e i relativi risultati. La query dovrebbe contenere il codice seguente:

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

1. Selezionare **&#9655; Esegui** per eseguire la query. Esaminare quindi i risultati, che devono contenere solo le righe relative al dispositivo *Dev1*.

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

## Eliminare le risorse di Azure

Dopo aver completato l'esplorazione di Azure Synapse Analytics, è necessario eliminare le risorse create per evitare costi di Azure non necessari.

1. Chiudere la scheda del browser relativa a Synapse Studio senza salvare le modifiche e tornare al portale di Azure.
1. Nella **home page** del portale di Azure selezionare **Gruppi di risorse**.
1. Selezionare il gruppo di risorse per l'area di lavoro Synapse Analytics (non il gruppo di risorse gestite) e verificare che contenga l'area di lavoro Synapse, l'account di archiviazione e il pool di Esplora dati per l'area di lavoro. Se è stato completato l'esercizio precedente, conterrà anche un pool di Spark.
1. Nel parte superiore della pagina **Panoramica** del gruppo di risorse selezionare **Elimina gruppo di risorse**.
1. Immettere il nome del gruppo di risorse per confermare l'eliminazione e selezionare **Elimina**.

    Dopo alcuni minuti, l'area di lavoro di Azure Synapse e l'area di lavoro gestita associata verranno eliminate.
