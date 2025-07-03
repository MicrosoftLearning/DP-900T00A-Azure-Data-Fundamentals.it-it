---
lab:
  title: Esplorare l'analisi dei dati in Microsoft Fabric
  module: Explore fundamentals of large-scale data analytics
---

# Esplorare l'analisi dei dati in Microsoft Fabric

In questo esercizio saranno esaminati l'inserimento e l'analisi dei dati in un lakehouse di Microsoft Fabric.

Il completamento di questo lab richiederà circa **25** minuti.

> **Nota**: per completare questo esercizio è necessaria una licenza di Microsoft Fabric. Per informazioni dettagliate su come abilitare una licenza di prova gratuita di Fabric, vedere [Introduzione a Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial). Per eseguire questa operazione, è necessario anche un account Microsoft *dell'istituto di istruzione* o *aziendale*. Se non è disponibile, è possibile [iscriversi per ottenere una versione di valutazione di Microsoft Office 365 E3 o versione successiva](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans).

*La prima volta che si usano le funzionalità di Microsoft Fabric, potrebbero essere visualizzate richieste con suggerimenti. Ignorare questi elementi.*

## Creare un'area di lavoro

Prima di usare i dati in Fabric, creare un'area di lavoro con la versione di valutazione di Fabric abilitata.

1. Accedere a [Microsoft Fabric](https://app.fabric.microsoft.com) all'indirizzo `https://app.fabric.microsoft.com`.
1. Nella barra dei menu, in basso a sinistra, passare all'esperienza **di Ingegneria dei dati**.

    ![Screenshot del menu del selettore dell'esperienza.](./images/fabric-switcher.png)

1. Nella barra dei menu a sinistra selezionare **Aree di lavoro** (l'icona è simile a &#128455;).
1. Creare una nuova area di lavoro con un nome di propria scelta, selezionando una modalità di licenza nella sezione **Avanzate** che include la capacità di Fabric (*versione di valutazione*, *Premium* o *Fabric*).
1. Quando si apre la nuova area di lavoro, deve essere vuota.

    ![Screenshot di un'area di lavoro vuota Power BI.](./images/new-workspace.png)

## Creare una lakehouse

Ora che si dispone di un'area di lavoro, è possibile creare un data lakehouse per i file di dati.

1. Nella home page dell'area di lavoro creare una nuova **lakehouse** con un nome di propria scelta.

    Dopo circa un minuto, verrà creata un nuovo lakehouse:

    ![Screenshot di un nuovo lakehouse.](./images/new-lakehouse.png)

1. Visualizzare il nuovo lakehouse e tenere presente che il riquadro **Lakehouse Explorer** a sinistra consente di esplorare tabelle e file al suo interno:
    - La cartella **Tabelle** contiene tabelle su cui è possibile eseguire query tramite SQL. Le tabelle in un lakehouse di Microsoft Fabric si basano sul formato di file open source *Delta Lake* comunemente usato in Apache Spark.
    - La cartella **File** contiene i file di dati nell'archivio OneLake del lakehouse che non sono associati alle tabelle delta gestite. In questa cartella è anche possibile creare *scelte rapide* per fare riferimento ai dati archiviati esternamente.

    Attualmente non sono presenti tabelle o file nel lakehouse.

## Inserire i dati

Un modo semplice per inserire dati consiste nell'usare un'attività **Copia dati** in una pipeline per estrarre i dati da un'origine e copiarli in un file nel lakehouse.

1. **Nella home** page del lakehouse, nel **menu Recupera dati** selezionare **Nuova pipeline** di dati e creare una nuova pipeline di dati denominata **Ingest Data**.
1. Nella pagina Scegliere un'origine** dati della ****procedura guidata Copia dati** selezionare Dati** di esempio **e quindi selezionare il **set di dati di esempio NYC Taxi - Green**.

    ![Screenshot della pagina Scegli origine dati.](./images/choose-data-source.png)

1. Nella pagina Connetti all'origine **** dati visualizzare le tabelle nell'origine dati. Dovrebbe essere presente una tabella che contiene i dettagli delle corse in taxi a New York City. Quindi selezionare **Avanti** per passare alla pagina **Scegli destinazione dati**.
1. Nella pagina **Scegli destinazione dati** selezionare il lakehouse esistente. Quindi seleziona **Avanti**.
1. Impostare le opzioni di destinazione dati seguenti e quindi selezionare **Avanti**:
    - **Cartella radice**: tabelle
    - **Impostazioni di caricamento**: caricare in una nuova tabella
    - **Nome tabella di destinazione**: taxi_rides *(potrebbe essere necessario attendere la visualizzazione dell'anteprima dei mapping delle colonne prima di poter modificare questa impostazione)*
    - **Mapping delle colonne**: *lasciare invariati i mapping predefiniti*
    - **Abilita partizione**: *deselezionata*
1. Nella pagina **Rivedi e salva** verificare che l'opzione **Avvia trasferimento dati immediatamente** sia selezionata e quindi selezionare **Salva e Esegui**.

    Viene creata una nuova pipeline contenente un'attività **Copia dati**, come illustrato di seguito:

    ![Screenshot di una pipeline con un'attività Copia dati.](./images/copy-data-pipeline.png)

    Quando l'esecuzione della pipeline viene avviata, è possibile monitorarne lo stato nel riquadro **Output** nella finestra di progettazione della pipeline. Usare l'icona **&#8635;** (*Aggiorna*) per aggiornare lo stato e attendere il completamento (che potrebbe richiedere più di 10 minuti).

1. Nella barra dei menu dell'hub a sinistra selezionare il lakehouse.
1. **Nella home** page, nel **riquadro Lakehouse Explorer**, nel **menu ...** per il **nodo Tabelle** selezionare **Aggiorna** e quindi espandere **Tabelle** per verificare che la **tabella taxi_rides** sia stata creata.

    > **Nota**: se la nuova tabella è elencata come *non identificata*, usare l'opzione **di menu Aggiorna** per aggiornare la visualizzazione.

1. Selezionare la **tabella taxi_rides** per visualizzarne il contenuto.

    ![Screenshot della tabella taxi_rides.](./images/dimProduct.png)

## Eseguire query sui dati nel lakehouse

Ora che i dati sono stati inseriti in una tabella nel lakehouse, è possibile usare SQL per eseguire le query.

1. Nella parte superiore destra della pagina Lakehouse passare dalla **visualizzazione Lakehouse** all'endpoint **** di analisi SQL per il lakehouse.

1. Selezionare **Nuova query SQL** sulla barra degli strumenti. Nel riquadro dell'editor di query, immettere il seguente codice SQL:

    ```sql
    SELECT  DATENAME(dw,lpepPickupDatetime) AS Day,
            AVG(tripDistance) As AvgDistance
    FROM taxi_rides
    GROUP BY DATENAME(dw,lpepPickupDatetime)
    ```

1. Selezionare il **&#9655; Pulsante Esegui** per eseguire la query ed esaminare i risultati, che devono includere la distanza media delle corse per ogni giorno della settimana.

    ![Screenshot di una query SQL.](./images/sql-query.png)

## Visualizzare i dati in un lakehouse

I lakehouse di Microsoft Fabric organizzano tutte le tabelle in un modello di dati semantico, che è possibile usare per creare visualizzazioni e report.

1. Nella parte inferiore sinistra della pagina, nel riquadro Esplora** risorse selezionare la **scheda Modello** per visualizzare il modello di dati per le tabelle nella lakehouse (incluse le tabelle di sistema e la **tabella taxi_rides**).**
1. Sulla barra degli strumenti selezionare **Nuovo report** per creare un nuovo report in base al **taxi_rides**.
1. Nella finestra di progettazione report:
    1. **Nel riquadro Dati** espandere la **tabella taxi_rides** e selezionare i **campi lpepPickupDatetime** e **passengerCount**.
    1. **Nel riquadro Visualizzazioni** selezionare la **visualizzazione Grafico** a linee. Assicurarsi quindi che l'asse **** X contenga il **campo lpepPickupDatetime** e l'asse **Y** contenga **Sum of passengerCount**.

        ![Screenshot di un report di Power BI.](./images/fabric-report.png)

    > **Suggerimento**: è possibile usare le icone **>>** per nascondere i riquadri di Progettazione report per visualizzare il report in modo più chiaro.

1. Scegliere Salva dal **menu **File** per salvare il report come **Report** corse taxi nell'area** di lavoro Infrastruttura.

    Il report è disponibile nella pagina dell'area di lavoro nel portale di Microsoft Fabric.

## Pulire le risorse

Se è stata completata l'esplorazione di Microsoft Fabric, è possibile eliminare l'area di lavoro creata per questo esercizio.

1. Nella barra a sinistra selezionare l'icona dell'area di lavoro per visualizzare tutti gli elementi contenuti.
2. Nel menu **...** sulla barra degli strumenti selezionare **Impostazioni area di lavoro**.
3. Nella sezione **Altro** selezionare **Rimuovi questa area di lavoro**.
