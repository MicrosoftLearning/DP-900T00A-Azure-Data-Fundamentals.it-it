---
lab:
  title: Esplorare Archiviazione di Azure
  module: Explore Azure Storage for non-relational data
---

# <a name="explore-azure-storage"></a>Esplorare Archiviazione di Azure

In questo esercizio si effettuerà il provisioning di un account di archiviazione di Azure nella sottoscrizione di Azure e si esploreranno i diversi modi in cui è possibile usarlo per archiviare i dati.

Il completamento di questo lab richiederà circa **15** minuti.

## <a name="before-you-start"></a>Prima di iniziare

Sarà necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free) con accesso di livello amministrativo.

## <a name="provision-an-azure-storage-account"></a>Effettuare il provisioning di un account di archiviazione di Azure

Il primo passaggio per usare Archiviazione di Azure prevede il provisioning di un account di archiviazione di Azure nella sottoscrizione di Azure.

1. Accedere al [portale di Azure](https://portal.azure.com?azure-portal=true) se questa operazione non è già stata eseguita.
1. On the Azure portal home page, select <bpt id="p1">**</bpt>&amp;#65291; Create a resource<ept id="p1">**</ept> from the upper left-hand corner and search for <bpt id="p2">*</bpt>Storage account<ept id="p2">*</ept>. Then in the resulting <bpt id="p1">**</bpt>Storage account<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.
1. Immettere i valori seguenti nella pagina **Crea un account di archiviazione**:
    - **Sottoscrizione** Selezionare la sottoscrizione di Azure.
    - **Gruppo di risorse**: creare un nuovo gruppo di risorse con un nome di propria scelta.
    - **Nome account di archiviazione**: immettere un nome univoco per l'account di archiviazione usando lettere minuscole e numeri.
    - **Area**: selezionare qualsiasi posizione disponibile.
    - **Prestazioni**: *Standard*
    - **Ridondanza**: *archiviazione con ridondanza locale*

1. Select <bpt id="p1">**</bpt>Next: Advanced &gt;<ept id="p1">**</ept> and view the advanced configuration options. In particular, note that this is where you can enable hierarchical namespace to support Azure Data Lake Storage Gen2. Leave this option <bpt id="p1">**</bpt><bpt id="p2">&lt;u&gt;</bpt>unselected<ept id="p2">&lt;/u&gt;</ept><ept id="p1">**</ept> (you'll enable it later), and then select <bpt id="p3">**</bpt>Next: Networking &gt;<ept id="p3">**</ept> to view the networking options for your storage account.
1. Select <bpt id="p1">**</bpt>Next: Data protection &gt;<ept id="p1">**</ept> and then in the <bpt id="p2">**</bpt>Recovery<ept id="p2">**</ept> section, <bpt id="p3">&lt;u&gt;</bpt>de<ept id="p3">&lt;/u&gt;</ept>select all of the <bpt id="p4">**</bpt>Enable soft delete...<ept id="p4">**</ept> options. These options retain deleted files for subsequent recovery, but can cause issues later when you enable hierarchical namespace.
1. Continuare a fare clic su **Avanti >** nelle pagine rimanenti senza modificare nessuna delle impostazioni predefinite e quindi nella pagina **Rivedi e crea** attendere la convalida delle selezioni e selezionare **Crea** per creare l'account di archiviazione di Azure.
1. Wait for deployment to complete. Then go to the resource that was deployed.

## <a name="explore-blob-storage"></a>Esplorare l'archivio BLOB

Dopo aver creato un account di archiviazione di Azure, è possibile creare un contenitore per i dati BLOB.

1. Scaricare il file JSON [product1.json](https://aka.ms/product1.json?azure-portal=true) da `https://aka.ms/product1.json` e salvarlo nel computer. È possibile salvarlo in qualsiasi cartella per caricarlo nell'archivio BLOB in seguito.

    *Se il file JSON viene visualizzato nel browser, salvare la pagina come **product1.json**.*

1. Nella pagina del portale di Azure del contenitore di archiviazione, sulla sinistra, nella sezione **Archiviazione dati** selezionare **Contenitori**.
1. Nella pagina **Contenitori** selezionare **&#65291; Contenitore** e aggiungere un nuovo contenitore denominato **data** con un livello di accesso pubblico **Privato (nessun accesso anonimo)** .
1. Una volta creato il contenitore **data**, verificare che sia elencato nella pagina **Contenitori**.
1. In the pane on the left side, in the top section, select **Storage browser **. This page provides a browser-based interface that you can use to work with the data in your storage account.
1. Nella pagina del browser archiviazione selezionare **Contenitori BLOB** e verificare che il contenitore **data** sia elencato.
1. Selezionare il contenitore **data** e notare che è vuoto.
1. Selezionare **&#65291; Aggiungi directory** e leggere le informazioni sulle cartelle prima di creare una nuova directory denominata **products**.
1. Nel browser archiviazione verificare che la visualizzazione corrente mostri il contenuto della cartella **products** appena creata. Si noti che il percorso di navigazione nella parte superiore della pagina corrisponde al percorso **Contenitori BLOB > data > products**.
1. Nel percorso di navigazione selezionare **data** per passare al contenitore **data** e si noti che <u>non</u> contiene una cartella denominata **products**.

    Folders in blob storage are virtual, and only exist as part of the path of a blob. Since the <bpt id="p1">**</bpt>products<ept id="p1">**</ept> folder contained no blobs, it isn't really there!

1. Usare il pulsante **&#10514; Carica** per aprire il pannello **Carica BLOB**.
1. In the <bpt id="p1">**</bpt>Upload blob<ept id="p1">**</ept> panel, select the <bpt id="p2">**</bpt>product1.json<ept id="p2">**</ept> file you saved on your local computer previously. Then in the <bpt id="p1">**</bpt>Advanced<ept id="p1">**</ept> section, in the <bpt id="p2">**</bpt>Upload to folder<ept id="p2">**</ept> box, enter <bpt id="p3">**</bpt>product_data<ept id="p3">**</ept> and select the <bpt id="p4">**</bpt>Upload<ept id="p4">**</ept> button.
1. Chiudere il pannello **Caricare BLOB** se è ancora aperto e verificare che una cartella virtuale **product_data** sia stata creata nel contenitore **data**.
1. Selezionare la cartella **product_data** e verificare che contenga il BLOB **product1.json** caricato.
1. Sulla sinistra, nella sezione **Archiviazione dati** selezionare **Contenitori**.
1. Aprire il contenitore **data** e verificare che sia elencata la cartella **product_data** creata.
1. Select the <bpt id="p1">**</bpt>&amp;#x2027;&amp;#x2027;&amp;#x2027;<ept id="p1">**</ept> icon at the right-end of the folder, and note that it doesn't display any options. Folders in a flat namespace blob container are virtual, and can't be managed.
1. Usare l'icona **X** in alto a destra nella pagina **data** per chiudere la pagina e tornare alla pagina **Contenitori**.

## <a name="explore-azure-data-lake-storage-gen2"></a>Esplorare Azure Data Lake Storage Gen2

Azure Data Lake Store Gen2 support enables you to use hierarchical folders to organize and manage access to blobs. It also enables you to use Azure blob storage to host distributed file systems for common big data analytics platforms.

1. Scaricare il file JSON [product2.json](https://aka.ms/product2.json?azure-portal=true) da `https://aka.ms/product2.json` e salvarlo sullo stesso computer, nella stessa cartella in cui in precedenza è stato scaricato **product1.json**. Lo si caricherà nell'archivio BLOB in un secondo momento.
1. Nella pagina del portale di Azure dell'account di archiviazione, sulla sinistra scorrere verso il basso fino alla sezione **Impostazioni** e selezionare **Aggiornamento di Data Lake Gen2**.
1. In the ****Data Lake Gen2 upgrade**** page, expand and complete each step to upgrade your storage account to enable hierarchical namespace and support Azure Data Lake Storage Gen 2. This may take some time.
1. Al termine dell'aggiornamento, nel riquadro a sinistra, nella sezione in alto selezionare **Browser archiviazione** e tornare alla radice del contenitore BLOB **data**, che contiene ancora la cartella **product_data**.
1. Selezionare la cartella **product_data** e verificare che contenga ancora il file **product1.json** caricato in precedenza.
1. Usare il pulsante **&#10514; Carica** per aprire il pannello **Carica BLOB**.
1. Nella home page del portale di Azure selezionare **&#65291; Crea una risorsa** nell'angolo in alto a sinistra e cercare *Account di archiviazione*.
1. Chiudere il pannello **Carica BLOB** se è ancora aperto e verificare che una cartella **product_data** contenga ora il file **product2.json**.
1. Sulla sinistra, nella sezione **Archiviazione dati** selezionare **Contenitori**.
1. Aprire il contenitore **data** e verificare che sia elencata la cartella **product_data** creata.
1. Selezionare l'icona **&#x2027;&#x2027;&#x2027;** a destra della cartella e notare che, con lo spazio dei nomi gerarchico abilitato, è possibile eseguire attività di configurazione a livello di cartella, incluse la ridenominazione delle cartelle e l'impostazione delle autorizzazioni.
1. Usare l'icona **X** in alto a destra nella pagina **data** per chiudere la pagina e tornare alla pagina **Contenitori**.

## <a name="explore-azure-files"></a>Esplorare File di Azure

File di Azure consente di creare condivisioni file basate sul cloud.

1. Nella pagina del portale di Azure del contenitore di archiviazione, sulla sinistra, nella sezione **Archiviazione dati** selezionare **Condivisioni file**.
1. Nella pagina Condivisioni file selezionare **&#65291; Condivisione file** e aggiungere una nuova condivisione file denominata **files** usando il livello **Ottimizzato per le transazioni**.
1. In **Condivisioni file** aprire la nuova condivisione **files**.
1. Nella pagina **Account di archiviazione** risultante selezionare **Crea**.
1. Chiudere il riquadro **Connetti** e quindi chiudere la pagina **files** per tornare alla pagina **Condivisioni file** dell'account di archiviazione di Azure.

## <a name="explore-azure-tables"></a>Esplorare Tabelle di Azure

Tabelle di Azure fornisce un archivio di coppie chiave/valore per le applicazioni che, pur dovendo archiviare i valori dei dati, non necessitano della funzionalità completa e della struttura di un database relazionale.

1. Nella pagina del portale di Azure del contenitore di archiviazione, sulla sinistra, nella sezione **Archiviazione dati** selezionare **Tabelle**.
1. Nella pagina **Tabelle** selezionare **&#65291; Tabella** e creare una nuova tabella denominata **products**.
1. Una volta creata la tabella **products**, nel riquadro sulla sinistra, nella sezione in alto selezionare **Browser archiviazione**.
1. Nello strumento di esplorazione dell'archiviazione selezionare **Tabelle** e verificare che la tabella **products** sia elencata.
1. Selezionare la tabella **products**.
1. Nella pagina **product** selezionare **&#65291; Aggiungi entità**.
1. Nel pannello **Aggiungi entità** immettere i valori delle chiavi seguenti:
    - **PartitionKey**: 1
    - **RowKey**: 1
1. Selezionare **Aggiungi proprietà** e creare una nuova proprietà con i valori seguenti:

    |Nome proprietà | Type | valore |
    | ------------ | ---- | ----- |
    | Nome | string | Widget |

1. Aggiungere una seconda proprietà con i valori seguenti:

    |Nome proprietà | Type | valore |
    | ------------ | ---- | ----- |
    | Prezzo | Double | 2,99 |

1. Selezionare **Inserisci** per inserire una riga per la nuova entità nella tabella.
1. Nel browser archiviazione verificare che una riga sia stata aggiunta alla tabella **products** e che sia stata creata una colonna **Timestamp** per indicare quando la riga è stata modificata per l'ultima volta.
1. Aggiungere un'altra entità alla tabella **products** con le proprietà seguenti:

    |Nome proprietà | Type | valore |
    | ------------ | ---- | ----- |
    | PartitionKey | string | 1 |
    | RowKey | string | 2 |
    | Nome | string | Kniknak |
    | Prezzo | Double | 1.99 |
    | Non disponibile | Boolean | true |

1. Dopo aver inserito la nuova entità, verificare che nella tabella sia visualizzata una riga contenente il prodotto fuori produzione.

    You have manually entered data into the table using the storage browser interface. In a real scenario, application developers can use the Azure Storage Table API to build applications that read and write values to tables, making it a cost effective and scalable solution for NoSQL storage.

> **Suggerimento**: se è stata completata l'esplorazione di Archiviazione di Azure, è possibile eliminare il gruppo di risorse creato in questo esercizio.
