---
lab:
  title: Esplorare analisi in tempo reale in Microsoft Fabric
  module: Explore fundamentals of large-scale data analytics
---

# Esplorare analisi in tempo reale in Microsoft Fabric

In questo esercizio verrà esaminata l'analisi n tempo reale in Microsoft Fabric.

Il completamento di questo lab richiederà circa **25** minuti.

> **Nota**: per completare questo esercizio è necessaria una licenza di Microsoft Fabric. Per informazioni dettagliate su come abilitare una licenza di prova gratuita di Fabric, vedere [Introduzione a Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial). Per eseguire questa operazione, è necessario anche un account Microsoft *dell'istituto di istruzione* o *aziendale*. Se non è disponibile, è possibile [iscriversi per ottenere una versione di valutazione di Microsoft Office 365 E3 o versione successiva](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans).

## Creare un'area di lavoro

Prima di usare i dati in Fabric, creare un'area di lavoro con la versione di valutazione di Fabric abilitata.

1. Accedere a [Microsoft Fabric](https://app.fabric.microsoft.com) all'indirizzo `https://app.fabric.microsoft.com`.
2. Nella barra dei menu a sinistra selezionare **Aree di lavoro** (l'icona è simile a &#128455;).
3. Creare una nuova area di lavoro con un nome di propria scelta, selezionando una modalità di licenza nella sezione **Avanzate** che include la capacità di Fabric (*versione di valutazione*, *Premium* o *Fabric*).
4. Quando si apre la nuova area di lavoro, deve essere vuota.

    ![Screenshot di un'area di lavoro vuota Power BI.](./images/new-workspace.png)

## Creare un database KQL

Ora che si dispone di un'area di lavoro, è possibile creare un database KQL per archiviare i dati in tempo reale.

1. Nella parte inferiore sinistra del portale, passare all'esperienza di **Intelligence in tempo reale**.

    ![Screenshot del menu del selettore dell'esperienza.](./images/fabric-real-time.png)

    La home page di Intelligence in tempo reale include riquadri per creare asset di uso comune per l'analisi dei dati in tempo reale.

2. Nella home page di Intelligence in tempo reale, creare una nuova **eventhouse** con un nome di propria scelta.

    ![Screenshot dell’editor RTA con Crea KQL DB evidenziato.](./images/create-kql-db.png)

    L’eventhouse viene usata per raggruppare e gestire i database tra i vari progetti. Un database KQL vuoto viene creato automaticamente con il nome dell’eventhouse e i dati verranno aggiunti più avanti nel corso di questo esercizio.

## Creare un eventstream

Gli eventstream offrono un modo scalabile e flessibile per inserire dati in tempo reale da un'origine di streaming.

1. Nella barra dei menu a sinistra, selezionare la pagina **Home** per l'esperienza di Intelligence in tempo reale.
1. Nella home page selezionare il riquadro per creare un nuovo **eventstream** con un nome a piacere.

    Dopo poco, viene visualizzata la finestra di progettazione visiva per eventstream.

    ![Screenshot della finestra di progettazione Eventstream.](./images/eventstream-designer.png)

    Il canvas della finestra di progettazione visiva mostra un'origine che si connette all'eventstream, che a sua volta è connesso a una destinazione.

1. Nel canvas della finestra di progettazione selezionare **Dati di esempio** nell'elenco **Nuova origine** dell'origine. Nel riquadro **Dati di esempio** specificare quindi il nome **taxi** e selezionare i dati di esempio **yellow taxi** (che rappresentano i dati raccolti dai percorsi dei taxi). Selezionare **Aggiungi**.
1. Sotto il canvas della finestra di progettazione selezionare la scheda **Anteprima dati** per visualizzare in anteprima i dati trasmessi in streaming dall'origine:

    ![Screenshot dell'anteprima dati dell'eventstream.](./images/eventstream-preview.png)

1. Nel canvas della finestra di progettazione selezionare **Database KQL** nell'elenco **Nuova destinazione** della destinazione. Nel riquadro del **database KQL** specificare quindi il nome di destinazione **taxi-data** e selezionare l'area di lavoro e il database KQL. Selezionare **Crea nuovo** in Tabella di destinazione e immettere il nome della tabella **taxi-data**. Selezionare **Aggiungi**.
1. Verificare che l'eventstream completato sia simile al seguente:

    ![Screenshot di un eventstream completato.](./images/complete-eventstream.png)

## Eseguire query sui dati in tempo reale in un database KQL

L'eventstream popola continuamente una tabella nel database KQL, consentendo di eseguire query sui dati in tempo reale.

1. Nell'hub del menu a sinistra selezionare il database KQL (oppure selezionare l'area di lavoro e trovare il database KQL in questa posizione).
1. Nel menu **...** della tabella **taxi-data** (creata dall'eventstream) selezionare **Esegui query su tabella > Record inseriti nelle ultime 24 ore**.

    ![Screenshot del menu Esegui query su tabella in un database KQL.](./images/kql-query.png)

1. Visualizzare i risultati della query, che deve essere una query KQL simile alla seguente:

    ```kql
    ['taxi-data']
    | where ingestion_time() between (now(-1d) .. now())
    ```

    I risultati mostrano tutti i record dei taxi inseriti dall'origine di streaming nelle ultime 24 ore.

1. Sostituire tutto il codice di query KQL nella metà superiore dell'editor di query con il codice seguente:

    ```kql
    // This query returns the number of taxi pickups per hour
    ['taxi-data']
    | summarize PickupCount = count() by bin(todatetime(tpep_pickup_datetime), 1h)
    ```

1. Utilizzare il pulsante **▷ Esegui** per eseguire la query ed esaminare i risultati, che mostrano il numero di fermate per i passeggeri dei taxi per ogni ora.

## Pulire le risorse

Se è stata completata l'esplorazione dell'analisi in tempo reale in Microsoft Fabric, è possibile eliminare l'area di lavoro creata per questo esercizio.

1. Nella barra a sinistra selezionare l'icona dell'area di lavoro per visualizzare tutti gli elementi contenuti.
2. Nel menu **...** sulla barra degli strumenti selezionare **Impostazioni area di lavoro**.
3. Nella sezione **Altro** selezionare **Rimuovi questa area di lavoro**.
