---
lab:
  title: Esplorare l'analisi dei dati in Microsoft Fabric
  module: Explore fundamentals of large-scale data analytics
---

# Esplorare l'analisi dei dati in Microsoft Fabric

In questo esercizio saranno esaminati l'inserimento e l'analisi dei dati in un lakehouse di Microsoft Fabric.

Il completamento di questo lab richiederà circa **25** minuti.

> **Nota**: per completare questo esercizio è necessaria una licenza di Microsoft Fabric. Per informazioni dettagliate su come abilitare una licenza di prova gratuita di Fabric, vedere [Introduzione a Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial). Per eseguire questa operazione, è necessario anche un account Microsoft *dell'istituto di istruzione* o *aziendale*. Se non è disponibile, è possibile [iscriversi per ottenere una versione di valutazione di Microsoft Office 365 E3 o versione successiva](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans).

## Creare un'area di lavoro

Prima di usare i dati in Fabric, creare un'area di lavoro con la versione di valutazione di Fabric abilitata.

1. Accedere a [Microsoft Fabric](https://app.fabric.microsoft.com) all'indirizzo `https://app.fabric.microsoft.com`.
2. Nella barra dei menu a sinistra selezionare **Aree di lavoro** (l'icona è simile a &#128455;).
3. Creare una nuova area di lavoro con un nome di propria scelta, selezionando una modalità di licenza nella sezione **Avanzate** che include la capacità di Fabric (*versione di valutazione*, *Premium* o *Fabric*).
4. Quando si apre la nuova area di lavoro, deve essere vuota.

    ![Screenshot di un'area di lavoro vuota Power BI.](./images/new-workspace.png)

## Creare una lakehouse

Ora che si dispone di un'area di lavoro, è possibile passare all'esperienza di *Ingegneria dei dati* nel portale e creare un data lakehouse per i file di dati.

1. Nella parte inferiore sinistra del portale passare all'esperienza di **Ingegneria dei dati**.

    ![Screenshot del menu del selettore dell'esperienza.](./images/fabric-switcher.png)

    La home page di ingegneria dei dati include riquadri per creare asset di ingegneria dei dati di uso comune.

2. Nella home page di **Ingegneria dei dati** creare un nuovo **Lakehouse** con un nome di propria scelta.

    Dopo circa un minuto, verrà creata un nuovo lakehouse:

    ![Screenshot di un nuovo lakehouse.](./images/new-lakehouse.png)

3. Visualizzare il nuovo lakehouse e tenere presente che il riquadro **Lakehouse Explorer** a sinistra consente di esplorare tabelle e file al suo interno:
    - La cartella **Tabelle** contiene tabelle su cui è possibile eseguire query tramite SQL. Le tabelle in un lakehouse di Microsoft Fabric si basano sul formato di file open source *Delta Lake* comunemente usato in Apache Spark.
    - La cartella **File** contiene i file di dati nell'archivio OneLake del lakehouse che non sono associati alle tabelle delta gestite. In questa cartella è anche possibile creare *scelte rapide* per fare riferimento ai dati archiviati esternamente.

    Attualmente non sono presenti tabelle o file nel lakehouse.

## Inserire i dati

Un modo semplice per inserire dati consiste nell'usare un'attività **Copia dati** in una pipeline per estrarre i dati da un'origine e copiarli in un file nel lakehouse.

1. Nella **home page** del lakehouse, dal menu **Recupera dati**, scegliere **Nuova pipeline di dati** e creare una nuova pipeline di dati denominata **Inserimento dati di vendita**.
1. Nella pagina **Scegli un'origine dati** della procedura guidata **Copia dati** selezionare il set di dati di esempio **Retail Data Model from Wide World Importers**.

    ![Screenshot della pagina Scegli origine dati.](./images/choose-data-source.png)

1. Selezionare **Avanti** e visualizzare le tabelle nell'origine dati nella pagina **Connessione all'origine dati**.
1. Selezionare la tabella **dimension_stock_item** che contiene i record dei prodotti. Quindi selezionare **Avanti** per passare alla pagina **Scegli destinazione dati**.
1. Nella pagina **Scegli destinazione dati** selezionare il lakehouse esistente. Quindi seleziona **Avanti**.
1. Impostare le opzioni di destinazione dati seguenti e quindi selezionare **Avanti**:
    - **Cartella radice**: tabelle
    - **Impostazioni di caricamento**: caricare in una nuova tabella
    - **Nome tabella di destinazione**: dimension_stock_item
    - **Mapping delle colonne**: *lasciare invariati i mapping predefiniti*
    - **Abilita partizione**: *deselezionata*
1. Nella pagina **Rivedi e salva** verificare che l'opzione **Avvia trasferimento dati immediatamente** sia selezionata e quindi selezionare **Salva e Esegui**.

    Viene creata una nuova pipeline contenente un'attività **Copia dati**, come illustrato di seguito:

    ![Screenshot di una pipeline con un'attività Copia dati.](./images/copy-data-pipeline.png)

    Quando l'esecuzione della pipeline viene avviata, è possibile monitorarne lo stato nel riquadro **Output** nella finestra di progettazione della pipeline. Utilizzare l'icona **↻** (*Aggiorna*) per aggiornare lo stato e attendere che abbia esito positivo.

1. Nella barra dei menu dell'hub a sinistra selezionare il lakehouse.
1. Nel riquadro **Esplora lakehouse** della **home page** espandere **Tabelle** e verificare che la tabella **dimension_stock_item** sia stata creata.

    > **Nota**: se la nuova tabella è elencata come *non identificata*, usare il pulsante **Aggiorna** nella barra degli strumenti del lakehouse per aggiornare la visualizzazione.

1. Selezionare la tabella **dimension_stock_item** per visualizzarne il contenuto.

    ![Screenshot della tabella dimension_stock_item.](./images/dimProduct.png)

## Eseguire query sui dati nel lakehouse

Ora che i dati sono stati inseriti in una tabella nel lakehouse, è possibile usare SQL per eseguire le query.

1. Nella parte superiore destra della pagina Lakehouse passare all'**endpoint SQL** del lakehouse.

    ![Screenshot del menu endpoint SQL.](./images/endpoint-switcher.png)

1. Selezionare **Nuova query SQL** sulla barra degli strumenti. Nel riquadro dell'editor di query, immettere il seguente codice SQL:

    ```sql
    SELECT Brand, COUNT(StockItemKey) AS Products
    FROM dimension_stock_item
    GROUP BY Brand
    ```

1. Selezionare il pulsante **▷ Esegui** per eseguire la query ed esaminare i risultati, che dovrebbero evidenziare che sono presenti due valori di marchio (*N/A* e *Northwind*) e mostrare il numero di prodotti in ognuno.

    ![Screenshot di una query SQL.](./images/sql-query.png)

## Visualizzare i dati in un lakehouse

I lakehouse di Microsoft Fabric organizzano tutte le tabelle in un modello di dati, che è possibile usare per creare visualizzazioni e report.

1. Nella parte inferiore sinistra della pagina, nel riquadro **Esplora risorse** selezionare la scheda **Modello** per visualizzare il modello di dati per le tabelle nel lakehouse (in questo caso è presente una sola tabella).

    ![Screenshot della pagina del modello in un lakehouse di Fabric.](./images/fabric-model.png)

1. Nella barra degli strumenti selezionare **Nuovo report** per aprire una nuova scheda del browser contenente la finestra di progettazione dei report di Power BI.
1. Nella finestra di progettazione report:
    1. Nel riquadro **Dati** espandere la tabella **dimension_stock_item** e selezionare i campi **marchio** e **StockItemKey**.
    1. Nel riquadro **Visualizzazioni** selezionare la visualizzazione **Grafico a barre in pila** (è la prima dell'elenco). Assicurarsi quindi che l'**asse Y** contenga il campo **Marchio** e modificare l'aggregazione nell'**asse X** in **Conteggio** in modo che contenga il campo **Conteggio di StockItemKey**. Infine, ridimensionare la visualizzazione nell'area di lavoro del report per riempire lo spazio disponibile.

        ![Screenshot di un report di Power BI.](./images/fabric-report.png)

    > **Suggerimento**: è possibile usare le icone **>>** per nascondere i riquadri di Progettazione report per visualizzare il report in modo più chiaro.

1. Scegliere **Salva** dal menu **File** per salvare il report come **Report quantità marchio** nell'area di lavoro di Fabric.

    È ora possibile chiudere la scheda del browser che contiene il report per tornare al lakehouse. Il report è disponibile nella pagina dell'area di lavoro nel portale di Microsoft Fabric.

## Pulire le risorse

Se è stata completata l'esplorazione di Microsoft Fabric, è possibile eliminare l'area di lavoro creata per questo esercizio.

1. Nella barra a sinistra selezionare l'icona dell'area di lavoro per visualizzare tutti gli elementi contenuti.
2. Nel menu **...** sulla barra degli strumenti selezionare **Impostazioni area di lavoro**.
3. Nella sezione **Altro** selezionare **Rimuovi questa area di lavoro**.
