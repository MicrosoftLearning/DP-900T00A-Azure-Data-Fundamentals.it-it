---
lab:
  title: Esplorare Spark Streaming in Azure Synapse Analytics
  module: Explore fundamentals of real-time analytics
---

# <a name="explore-spark-streaming-in-azure-synapse-analytics"></a>Esplorare Spark Streaming in Azure Synapse Analytics

In questo esercizio si useranno le funzionalità *Spark Structured Streaming* e le *tabelle delta* in Azure Synapse Analytics per elaborare i dati dei flussi.

Il completamento di questo lab richiederà circa **15** minuti.

## <a name="before-you-start"></a>Prima di iniziare

Sarà necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free) con accesso di livello amministrativo.

## <a name="provision-a-synapse-analytics-workspace"></a>Effettuare il provisioning di un'area di lavoro di Synapse Analytics

Per usare Synapse Analytics, è necessario effettuare il provisioning di una risorsa dell'area di lavoro di Synapse Analytics nella sottoscrizione di Azure.

1. Aprire il portale di Azure all'indirizzo del [portale di Azure](https://portal.azure.com?azure-portal=true) ed eseguire l'accesso usando le credenziali associate alla sottoscrizione di Azure.

    > <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: Ensure you are working in the directory containing your own subscription - indicated at the top right under your user ID. If not, select the user icon and switch directory.

2. Nella **home page** del portale di Azure usare l'icona **&#65291; Crea una risorsa** per creare una nuova risorsa.
3. Cercare *Azure Synapse Analytics* e creare una nuova risorsa **Azure Synapse Analytics** con le impostazioni seguenti:
    - **Sottoscrizione**: *la propria sottoscrizione di Azure*
        - **Gruppo di risorse**: *creare un nuovo gruppo di risorse con un nome appropriato, ad esempio "synapse-rg"*
        - **Gruppo di risorse gestite**: *immettere un nome appropriato, ad esempio "synapse-managed-rg".*
    - **Nome dell'area di lavoro**: *immettere un nome univoco dell'area di lavoro, ad esempio "synapse-ws-<nome_utente>* .
    - **Area**: *selezionare qualsiasi area disponibile*.
    - **Selezionare Data Lake Storage Gen 2**: dalla sottoscrizione 
        - **Nome dell'account**: *creare un nuovo account con un nome univoco, ad esempio "datalake<nome_utente>"* .
        - **Nome file system**: *creare un nuovo file system con un nome univoco, ad esempio "fs<nome_utente>"* .

    > <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: A Synapse Analytics workspace requires two resource groups in your Azure subscription; one for resources you explicitly create, and another for managed resources used by the service. It also requires a Data Lake storage account in which to store data, scripts, and other artifacts.

4. Dopo aver immesso questi dettagli, selezionare **Rivedi e crea**, quindi selezionare **Crea** per creare l'area di lavoro.
5. Attendere che venga creata l'area di lavoro. L'operazione può richiedere circa cinque minuti.
6. Al termine della distribuzione, passare al gruppo di risorse creato e osservare che contiene l'area di lavoro di Synapse Analytics e un account di archiviazione Data Lake.
7. Selezionare l'area di lavoro di Synapse e nella relativa pagina **Panoramica**, nella scheda **Apri Synapse Studio**, selezionare **Apri** per aprire Synapse Studio in una nuova scheda del browser. Synapse Studio è un'interfaccia basata sul Web in cui è possibile usare l'area di lavoro di Synapse Analytics.
8. Sul lato sinistro di Synapse Studio usare l'icona **&rsaquo;&rsaquo;** per espandere il menu. Verranno visualizzate le varie pagine all'interno di Synapse Studio in cui è possibile gestire le risorse ed eseguire attività di analisi dei dati, come illustrato di seguito:

    ![Synapse Studio](images/synapse-studio.png)

## <a name="create-a-spark-pool"></a>Creare un pool di Spark

Per usare Spark per elaborare i dati dei flussi, è necessario aggiungere un pool di Spark all'area di lavoro Azure Synapse.

1. In Synapse Studio selezionare la pagina **Gestisci**.
2. Selezionare la scheda **Pool di Apache Spark** e quindi usare l'icona **&#65291; Nuovo** per creare un nuovo pool di Spark con le impostazioni seguenti:
    - **Nome del pool di Apache Spark**: sparkpool
    - **Famiglia di dimensioni del nodo**: Con ottimizzazione per la memoria
    - **Dimensioni nodo**: Piccolo (4 vCore/32 GB)
    - **Scalabilità automatica**: abilitata
    - **Numero di nodi** 3----3
3. Esaminare e creare il pool di Spark e quindi attendere che venga distribuito. Questa operazione potrebbe richiedere alcuni minuti.

## <a name="explore-stream-processing"></a>Esplorare l'elaborazione dei flussi

Per esplorare l'elaborazione dei flussi con Spark, si userà un notebook che contiene codice Python e note per eseguire alcune operazioni di elaborazione di flusso di base con Spark Structured Streaming e tabelle delta.

1. Scaricare il notebook [Structured Streaming e Delta Tables.ipynb](https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/Spark%20Structured%20Streaming%20and%20Delta%20Tables.ipynb) nel computer locale (se il notebook viene aperto come file di testo nel browser, salvarlo in una cartella locale; prestare attenzione a salvarlo come **Structured Streaming e Delta Tables.ipynb**, non come file .txt).
2. In Synapse Studio selezionare la pagina **Sviluppo**.
3. Nel menu **&#65291;** selezionare **&#8612; Importa** e selezionare il file **Structured Streaming e Delta Tables.ipynb** nel computer locale.
4. Seguire le istruzioni presenti nel notebook per collegarlo al pool di Spark ed eseguire le celle di codice contenute per esplorare vari modi per usare Spark per l'elaborazione dei flussi.

## <a name="delete-azure-resources"></a>Eliminare le risorse di Azure

> <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: If you intend to complete other exercises that use Azure Synapse Analytics, you can skip this section. Otherwise, follow the steps below to avoid unnecessary Azure costs.

1. Chiudere la scheda del browser relativa a Synapse Studio senza salvare le modifiche e tornare al portale di Azure.
1. Nella **home page** del portale di Azure selezionare **Gruppi di risorse**.
1. Selezionare il gruppo di risorse per l'area di lavoro Synapse Analytics (non il gruppo di risorse gestite) e verificare che contenga l'area di lavoro Synapse, l'account di archiviazione e il pool di Esplora dati per l'area di lavoro. Se è stato completato l'esercizio precedente, conterrà anche un pool di Spark.
1. Nel parte superiore della pagina **Panoramica** del gruppo di risorse selezionare **Elimina gruppo di risorse**.
1. Immettere il nome del gruppo di risorse per confermare l'eliminazione e selezionare **Elimina**.

    Dopo alcuni minuti, l'area di lavoro di Azure Synapse e l'area di lavoro gestita associata verranno eliminate.
