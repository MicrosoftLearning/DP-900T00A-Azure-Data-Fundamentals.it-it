---
lab:
  title: Esplorare Analisi di flusso di Azure
  module: Explore fundamentals of real-time analytics
---

# Esplorare Analisi di flusso di Azure

In questo esercizio si effettuerà il provisioning di un processo di Analisi di flusso di Azure nella sottoscrizione di Azure e lo si userà per elaborare un flusso di dati in tempo reale.

Il completamento di questo lab richiederà circa **15** minuti.

## Prima di iniziare

Sarà necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free) con accesso di livello amministrativo.

## Creare risorse Azure

1. Accedere alla sottoscrizione di Azure nel [portale di Azure](https://portal.azure.com) usando le credenziali della sottoscrizione di Azure.

1. Usare il pulsante **[\>_]** a destra della barra di ricerca, nella parte superiore della pagina, per aprire una nuova sessione di Cloud Shell nel portale di Azure selezionando un ambiente ***Bash*** e creando spazio di archiviazione, se richiesto. Cloud Shell fornisce un'interfaccia della riga di comando in un riquadro nella parte inferiore del portale di Azure, come illustrato di seguito:

    ![Portale di Azure con un riquadro di Cloud Shell](./images/cloud-shell.png)

1. In Azure Cloud Shell immettere il comando seguente per scaricare i file necessari per questo esercizio.

    ```bash
    git clone https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals dp-900
    ```

1. Attendere che l'esecuzione del comando sia completata e immettere quindi il comando seguente per modificare la directory corrente nella cartella contenente i file per questo esercizio.

    ```bash
    cd dp-900/streaming
    ```

1. Immettere il comando seguente per eseguire uno script che crei le risorse di Azure necessarie in questo esercizio.

    ```bash
    bash setup.sh
    ```

    > Ignorare eventuali messaggi di avviso relativi alle modifiche future e alle funzionalità sperimentali.

    Attendere l'esecuzione dello script ed eseguire le azioni seguenti:

    1. Installa le estensioni dell'interfaccia della riga di comando di Azure necessarie per creare risorse (*è possibile ignorare eventuali avvisi sulle estensioni sperimentali*)
    1. Identifica il gruppo di risorse di Azure fornito per questo esercizio.
    1. Crea una risorsa dell'*hub IoT di Azure*, che verrà usata per ricevere un flusso di dati da un dispositivo simulato.
    1. Crea un *account di Archiviazione di Azure*, che verrà usato per archiviare i dati elaborati.
    1. Crea un processo di *Analisi di flusso di Azure*, che elaborerà i dati in ingresso nel dispositivo in tempo reale e scriverà i risultati nell'account di archiviazione.

## Esplorare le risorse di Azure

1. Nella home page del [portale di Azure](https://portal.azure.com?azure-portal=true) selezionare **Gruppi di risorse** per visualizzare i gruppi di risorse presenti nella sottoscrizione. Deve essere incluso anche il gruppo di risorse **learn*xxxxxxxxxxxxxxxxx...*** identificato dallo script di installazione.
2. Selezionare il gruppo di risorse **learn*xxxxxxxxxxxxxxxxx...*** e consultare le risorse contenute, che devono includere:
    - Un *hub IoT* denominato **iothub*xxxxxxxxxxxxx***, che consente di ricevere i dati in ingresso nel dispositivo.
    - Un *account di Archiviazione* denominato **store*xxxxxxxxxxxx***, in cui verranno scritti i risultati del processo di elaborazione dati.
    - Un *processo di Analisi di flusso di Azure* denominato **stream*xxxxxxxxxxxxx***, che consente di elaborare i dati di streaming.

    Se queste tre risorse non sono tutte elencate, fare clic sul pulsante **&#8635; Aggiorna** fino a quando non vengono visualizzate.

3. Selezionare il processo di Analisi di flusso **stream*xxxxxxxxxxxxx*** e visualizzare le informazioni nella relativa pagina **Panoramica**, osservando in particolare i dettagli seguenti:
    - Nel processo è presente sia un *input* denominato **iotinput** sia un *output* denominato **bloboutput**. Questi elementi fanno riferimento all'account di Archiviazione e hub IoT creato dallo script di installazione.
    - Nel processo è presente anche una *query*, che legge i dati dall'input **iotinput** e li aggrega contando il numero di messaggi elaborati ogni 10 secondi; i risultati vengono scritti nell'output **bloboutput**.

## Usare le risorse per analizzare i dati di streaming

1. Nella parte superiore della pagina **Panoramica** del processo di Analisi di flusso, selezionare il pulsante **&#9655; Avvia** e nel riquadro **Avvia processo** selezionare **Avvia** per avviare il processo.
2. Attendere la notifica che il processo di streaming è stato avviato correttamente.
3. Tornare all'istanza di Azure Cloud Shell e immettere il comando seguente per simulare un dispositivo che invia dati alla hub IoT.

    ```
    bash iotdevice.sh
    ```

4. Attendere l'avvio della simulazione, che verrà segnalato da un output simile al seguente:

    ```
    Device simulation in progress: 6%|#    | 7/120 [00:08<02:21, 1.26s/it]
    ```

5. Durante l'esecuzione della simulazione, tornare al portale di Azure, accedere alla pagina del gruppo di risorse **learn*xxxxxxxxxxxxxxxxx...*** e selezionare l'account di archiviazione **store*xxxxxxxxxxxx***.
6. Nel riquadro a sinistra del pannello dell'account di archiviazione selezionare la scheda **Contenitori**.
7. Aprire il contenitore **data**.
8. Nel contenitore **data** passare alla gerarchia di cartelle in cui è contenuta una cartella relativa all'anno corrente, con sottocartelle per il mese, il giorno e l'ora.
9. Nella cartella relativa all'ora notare il file creato, che dovrebbe avere un nome simile a **0_xxxxxxxxxxxxxxxx.json**.
10. Nel menu **...** per il file (a destra dei dettagli del file) selezionare **Visualizza/Modifica** ed esaminare il contenuto del file, che deve essere costituito da un record JSON per ogni periodo di 10 secondi, in cui è indicato il numero di messaggi ricevuti da dispositivi IoT, come illustrato di seguito:

    ```
    {"starttime":"2021-10-23T01:02:13.2221657Z","endtime":"2021-10-23T01:02:23.2221657Z","device":"iotdevice","messages":2}
    {"starttime":"2021-10-23T01:02:14.5366678Z","endtime":"2021-10-23T01:02:24.5366678Z","device":"iotdevice","messages":3}
    {"starttime":"2021-10-23T01:02:15.7413754Z","endtime":"2021-10-23T01:02:25.7413754Z","device":"iotdevice","messages":4}
    ...
    ```

11. Usare il pulsante **&#8635; Aggiorna** per aggiornare il file, osservando come i risultati aggiuntivi vengano scritti nel file mentre il processo di Analisi di flusso elabora i dati del dispositivo in tempo reale, man mano che vengono trasmessi dal dispositivo all'hub IoT.
12. Tornare ad Azure Cloud Shell e attendere il completamento della simulazione del dispositivo (dovrebbe richiedere circa 3 minuti).
13. Tornare al portale di Azure, aggiornare ancora una volta il file per visualizzare il set completo dei risultati generati durante la simulazione.
14. Tornare al gruppo di risorse **learn*xxxxxxxxxxxxxxxxx...*** e riaprire il processo di Analisi di flusso **stream*xxxxxxxxxxxxx***.
15. Nella parte superiore della pagina del processo di Analisi di flusso usare il pulsante **&#11036; Arresta** per interrompere il processo, confermando quando richiesto.

> **Nota**: se è stata completata l'esplorazione della soluzione di streaming, eliminare il gruppo di risorse creato in questo esercizio.
