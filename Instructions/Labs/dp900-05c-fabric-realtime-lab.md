---
lab:
  title: Esplorare l'analisi in tempo reale in Microsoft Fabric
  module: Explore fundamentals of large-scale data analytics
---

# Esplorare l'analisi in tempo reale in Microsoft Fabric

In questo esercizio si esaminerà l'analisi in tempo reale in Microsoft Fabric.

Il completamento di questo lab richiederà circa **25** minuti.

> **Nota**: è necessaria una licenza di Microsoft Fabric per completare questo esercizio. Per informazioni dettagliate su come abilitare una licenza di valutazione gratuita di Fabric, vedere [Introduzione a Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial) . Per eseguire questa operazione sarà necessario *un account* *aziendale o dell'istituto di istruzione* Microsoft. Se non ne hai uno, puoi [iscriverti per una versione di valutazione di Microsoft Office 365 E3 o successiva](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans).

## Creare un'area di lavoro

Prima di usare i dati in Fabric, creare un'area di lavoro con la versione di valutazione di Fabric abilitata.

1. Accedere a [Microsoft Fabric](https://app.fabric.microsoft.com) all'indirizzo `https://app.fabric.microsoft.com`.
2. Nella barra dei menu a sinistra selezionare **Aree** di lavoro (l'icona è simile a &#128455;).
3. Creare una nuova area di lavoro con un nome scelto, selezionando una modalità di licenza nella sezione **Avanzate** che include capacità infrastruttura (*Versione di valutazione*, *Premium* o *Fabric*).
4. Quando si apre la nuova area di lavoro, deve essere vuota.

    ![Screenshot di un'area di lavoro vuota in Power BI.](./Images/new-workspace.png)

## Creare un database KQL

Dopo aver creato un'area di lavoro, è possibile creare un database KQL per archiviare i dati in tempo reale.

1. Nella parte inferiore sinistra del portale passare all'esperienza **di Analisi in tempo reale**.

    ![Screenshot del menu del commutatore di esperienza.](./images/fabric-real-time.png)

    La home page dell'analisi in tempo reale include riquadri per creare asset comunemente usati per gli analyi di dati in tempo reale

2. Nella home page dell'analisi in tempo reale creare un nuovo **database KQL** con un nome scelto.

    Dopo un minuto o così via, verrà creato un nuovo database KQL:

    ![Screenshot di un nuovo database KQL.](./Images/kql-database.png)

    Attualmente non sono presenti tabelle nel database.

## Creare un eventstream

Gli eventistream offrono un modo scalabile e flessibile per inserire dati in tempo reale da un'origine di streaming.

1. Nella barra dei menu a sinistra selezionare la **home** page per l'esperienza di analisi in tempo reale.
1. Nella home page selezionare il riquadro per creare un nuovo **eventstream** con un nome scelto.

    Dopo un breve periodo di tempo, viene visualizzata la finestra di progettazione visiva per il flusso di eventi.

    ![Screenshot della finestra di progettazione Eventstream.](./Images/eventstream-designer.png)

    L'area di disegno della finestra di disegno della finestra di progettazione visiva mostra un'origine che si connette al flusso di eventi, che a sua volta è connesso a una destinazione.

1. Nell'area di disegno della finestra di progettazione selezionare **Dati di esempio** nell'elenco **Nuova origine** per l'origine. Nel riquadro **Dati di esempio** specificare quindi i **taxi** dei nomi e selezionare i dati di esempio **giallo** taxi (che rappresenta i dati raccolti dai percorsi dei taxi). Quindi selezionare **Aggiungi**.
1. Sotto l'area di disegno della finestra di progettazione selezionare la scheda **Anteprima dati** per visualizzare in anteprima i dati trasmessi dall'origine:

    ![Screenshot dell'anteprima dei dati Eventstream.](./Images/eventstream-preview.png)

1. Nell'area di disegno della finestra di progettazione selezionare **database KQL** nell'elenco **Nuova destinazione** per la destinazione. Nel riquadro **del database KQL** specificare quindi i dati dei **taxi** di destinazione e selezionare l'area di lavoro e il database KQL. Selezionare **quindi Crea e configura**.
1. Nella procedura guidata **Inserimento dati** nella pagina **Destinazione** selezionare **Nuova tabella** e immettere il nome della tabella **taxi-data**. Selezionare **Avanti: Origine**.
1. Nella pagina **Origine** esaminare il nome di connessione dati predefinito e quindi selezionare **Avanti: Schema**.
1. Nella pagina **Schema** modificare il **formato dati** da **TXT a JSON** e visualizzare l'anteprima per verificare che questo formato restituisca più colonne di dati. Selezionare **Avanti: Riepilogo**.
1. Nella pagina **Riepilogo** attendere che venga stabilita l'inserimento continuo e quindi selezionare **Chiudi**.
1. Verificare che il flusso di eventi completato sia simile al seguente:

    ![Screenshot di un eventstream completato.](./Images/complete-eventstream.png)

## Eseguire query sui dati in tempo reale in un database KQL

Il flusso di eventi popola continuamente una tabella nel database KQL, consentendo di eseguire query sui dati in tempo reale.

1. Nell'hub dei menu a sinistra selezionare il database KQL (o selezionare l'area di lavoro e trovare il database KQL).
1. Nel menu **...** per la tabella **dei dati dei taxi** (creata dall'eventostream), selezionare **Tabella query > Record inseriti negli ultimi 24 ore**.

    ![Screenshot del menu Tabella query in un database KQL.](./Images/kql-query.png)

1. Visualizzare i risultati della query, che deve essere una query KQL simile alla seguente:

    ```kql
    ['taxi-data']
    | where ingestion_time() between (now(-1d) .. now())
    ```

    I risultati mostrano tutti i record di taxi inseriti dall'origine di streaming negli ultimi 24 ore.

1. Sostituire tutto il codice di query KQL nella metà superiore dell'editor di query con il codice seguente:

    ```kql
    // This query returns the number of taxi pickups per hour
    ['taxi-data']
    | summarize PickupCount = count() by bin(tpep_pickup_datetime, 1h)
    ```

1. Usare il pulsante **&#9655; Esegui** per eseguire la query e esaminare i risultati, che mostrano il numero di ritiri taxi per ogni ora.
 
## Pulire le risorse

Se è stata completata l'esplorazione dell'analisi in tempo reale in Microsoft Fabric, è possibile eliminare l'area di lavoro creata per questo esercizio.

1. Nella barra a sinistra selezionare l'icona per l'area di lavoro per visualizzare tutti gli elementi contenuti.
2. Nel menu **...** sulla barra degli strumenti selezionare **Impostazioni area di lavoro**.
3. Nella sezione **Altre** selezionare **Rimuovi questa area di lavoro**.
