---
lab:
  title: Esplorare i principi fondamentali della visualizzazione dei dati con Power BI
  module: Explore fundamentals of data visualization
---

# Esplorare i principi fondamentali della visualizzazione dei dati con Power BI

In questo esercizio si userà Microsoft Power BI Desktop per creare un modello di dati e un report contenente le visualizzazioni interattive dei dati.

Il completamento di questo lab richiederà circa **20** minuti.

## Installare Power BI Desktop

Se Microsoft Power BI Desktop non è già installato nel computer Windows, è possibile scaricarlo e installarlo gratuitamente.

1. Scaricare il programma di installazione di Power BI Desktop da [https://aka.ms/power-bi-desktop](https://aka.ms/power-bi-desktop?azure-portal=true).
1. Quando il file è stato scaricato, aprirlo e usare la procedura guidata di installazione per installare Power BI Desktop nel computer. Questa installazione potrebbe richiedere alcuni minuti.

## Importare dati

1. Apri Power BI Desktop. L'interfaccia dell'applicazione ha un aspetto simile al seguente:

    ![Screenshot che mostra la schermata iniziale di Power BI Desktop.](images/power-bi-start.png)

    A questo punto, è possibile importare i dati per il report.

1. Nella schermata iniziale di Power BI Desktop selezionare **Recupera dati** e quindi nell'elenco delle origini dati selezionare **Web** e quindi **Connetti**.

    ![Screenshot che mostra come selezionare l'origine dati Web in Power BI.](images/web-source.png)

1. Nella finestra di dialogo **Da Web** immettere l'URL seguente e quindi selezionare **OK**:

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/customers.csv
    ```

1. Nella finestra di dialogo Accedere a contenuto Web selezionare **Connetti**.

1. Verificare che l'URL apra un set di dati contenente i dati dei clienti, come illustrato di seguito. Selezionare quindi **Carica** per caricare i dati nel modello di dati per il report.

    ![Screenshot che mostra un set di dati dei clienti visualizzato in Power BI.](images/customers.png)

1. Nella finestra principale di Power BI Desktop nel menu Dati selezionare **Recupera dati** e quindi selezionare **Web**:

    ![Screenshot che mostra il menu Recupera dati in Power BI.](images/get-data.png)

1. Nella finestra di dialogo **Da Web** immettere l'URL seguente e quindi selezionare **OK**:

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/products.csv
    ```

1. Nella finestra di dialogo selezionare **Carica** per caricare i dati dei prodotti in questo file nel modello di dati.

1. Ripetere i tre passaggi precedenti per importare un terzo set di dati contenente i dati dell'ordine dall'URL seguente:

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/orders.csv
    ```

## Esplorare un modello di dati

Le tre tabelle di dati importate sono state caricate in un modello di dati, che verrà ora esaminato e affinato.

1. In Power BI Desktop, nel bordo sinistro, selezionare la scheda **Modello** e quindi disporre le tabelle nel modello in modo che siano visibili. È possibile nascondere i riquadri a destra usando le icone **>>**:

    ![Screenshot che mostra la scheda Modello in Power BI.](images/model-tab.png)

1. Nella tabella **ordini** selezionare il campo **Ricavi** e quindi nel riquadro **Proprietà** impostare la relativa proprietà **Formato** su **Valuta**:

    ![Screenshot che mostra come impostare il formato di Revenue su Valuta in Power BI.](images/revenue-currency.png)

    Questo passaggio garantisce che i valori dei ricavi vengano visualizzati come valuta nelle visualizzazioni del report.

1. Nella tabella dei prodotti fare clic con il pulsante destro del mouse sul campo **Category** (o aprire il relativo menu **&vellip;**) e selezionare **Crea gerarchia**. Questo passaggio crea una gerarchia denominata **Gerarchia di Category**. Per visualizzarla, potrebbe essere necessario espandere o scorrere la tabella **products**. È possibile visualizzarla anche nel riquadro **Campi**:

    ![Screenshot che mostra come aggiungere la gerarchia di categorie in Power BI.](images/category-hierarchy.png)

1. Nella tabella dei prodotti fare clic con il pulsante destro del mouse sul campo **ProductName** (o aprire il relativo menu **&vellip;**) e scegliere **Aggiungi alla gerarchia** > **Gerarchia di Category**. In questo modo, il campo **NomeProdotto** viene aggiunto alla gerarchia creata in precedenza.
1. Nel riquadro **Campi** fare clic con il pulsante destro del mouse su **Gerarchia di categorie** (o aprire il relativo menu **...** ) e selezionare **Rinomina**. Rinominare quindi la gerarchia in **Prodotto classificato**.

    ![Screenshot che mostra come rinominare la gerarchia in Power BI.](images/rename-hierarchy.png)

1. Sul bordo sinistro selezionare la **scheda Visualizzazione** tabella e quindi nel **riquadro Dati** selezionare la **tabella customers** .
1. Selezionare l'intestazione di colonna **Città** e quindi impostare la proprietà **Categoria di dati** su **Città**:

    ![Screenshot che mostra come impostare una categoria di dati in Power BI.](images/data-category.png)

    Questo passaggio garantirà che i valori di questa colonna vengano interpretati come nomi di città, utili se si intende includere visualizzazioni di mappa.

## Creazione di un report

A questo punto, è possibile creare un report. È innanzitutto necessario controllare alcune impostazioni per assicurarsi che tutte le visualizzazioni siano abilitate.

1. Nel menu **File** selezionare **Opzioni e Impostazioni**. Selezionare quindi **Opzioni** e nella sezione **Sicurezza** assicurarsi che **Utilizza oggetti visivi della mappa e della mappa colorata** siano abilitati e selezionare **OK**.

    ![Screenshot che mostra come impostare la proprietà Utilizza oggetti visivi della mappa e della mappa colorata in PowerBI.](images/set-options.png)

    Questa impostazione garantisce che sia possibile includere visualizzazioni mappa nei report.

1. Nel bordo a sinistra selezionare la scheda **Vista report** e visualizzare l'interfaccia di progettazione del report.

    ![Screenshot che mostra la scheda Report in Power BI.](images/report-tab.png)

1. Nella barra multifunzione, sopra l'area di progettazione del report, selezionare **Casella di testo** e aggiungere al report una casella di testo contenente il testo **Report vendite**. Formattare il testo in grassetto con una dimensione del carattere pari a 32.

    ![Screenshot che mostra come aggiungere una casella di testo in Power BI.](images/text-box.png)

1. Selezionare qualsiasi area vuota nel report per deselezionare la casella di testo. Nel riquadro **Dati** espandere **Prodotti** e selezionare il campo **Prodotti classificati**. Questo passaggio aggiunge una tabella al report.

    ![Screenshot che mostra come aggiungere una tabella di prodotti classificati a un report in Power BI.](images/categorized-products-table.png)

1. Con la tabella ancora selezionata, nel riquadro **Dati** espandere **Ordini** e selezionare **Ricavi**. Alla tabella viene aggiunta una colonna Revenue. Potrebbe essere necessario espandere le dimensioni della tabella per visualizzarla.

    I ricavi vengono formattati come valuta, come specificato nel modello. Non è, tuttavia, stato specificato il numero di posizioni decimali, quindi i valori includono quantità frazionarie. Non è importante per le visualizzazioni che si intende creare, ma se lo si desidera è possibile tornare alla scheda **Modello** o **Dati** e modificare le posizioni decimali.

    ![Screenshot che mostra una tabella di prodotti classificati con Revenue in un report.](images/revenue-column.png)

1. Con la tabella ancora selezionata, nel riquadro **Visualizzazioni** selezionare la visualizzazione **Istogramma a colonne in pila**. La tabella viene modificata in un grafico a colonne che mostra i ricavi per categoria.

    ![Screenshot che mostra un grafico a istogramma in pila di prodotti classificati con Revenue in un report.](images/stacked-column-chart.png)

1. Sopra il grafico a colonne selezionato, selezionare l'icona **&#8595;** per attivare il drill-down. Nel grafico selezionare quindi la seconda colonna per eseguire il drill-down e visualizzare i ricavi per i singoli prodotti in questa categoria. Questa funzionalità è possibile perché è stata definita una gerarchia di categorie e prodotti.

    ![Screenshot che mostra un istogramma con drill-down per visualizzare i prodotti all'interno di una categoria.](images/drill-down.png)

1. Usare l'icona **&#x2191;** per eseguire il drill-up fino al livello di categoria. Selezionare quindi l'icona **(**&#8595;**)** per disattivare la funzionalità di drill-down.
1. Selezionare un'area vuota del report e quindi nel riquadro **Dati** selezionare il campo **Quantità** nella tabella **ordini** e il campo **Categoria** nella tabella **prodotti**. Questo passaggio consente di ottenere un altro grafico a colonne che mostra la quantità di vendite in base alla categoria di prodotti.
1. Con il nuovo grafico a colonne selezionato, nel riquadro **Visualizzazioni** selezionare **Grafico a torta** e quindi ridimensionare il grafico e posizionarlo accanto al grafico ricavi per colonna categoria.

    ![Screenshot che mostra un grafico a torta che mostra la quantità di vendite per categoria.](images/category-pie-chart.png)

1. Selezionare un'area vuota del rapporto e quindi nel riquadro **Dati** selezionare il campo **Città** nella tabella **clienti** e il campo **Ricavi** nella tabella **ordini**. Il risultato è una mappa che mostra i ricavi di vendita per città. Ridisporre e ridimensionare le visualizzazioni come necessario:

    ![Screenshot che mostra una mappa che mostra i ricavi per città.](images/revenue-map.png)

1. Tenere presente che nella mappa è possibile trascinare, fare doppio clic, usare una rotellina del mouse o pizzicare e trascinare su un touch screen per interagire. Selezionare quindi una città specifica e notare che le altre visualizzazioni nel report vengono modificate per evidenziare i dati per la città selezionata.

    ![Screenshot che mostra una mappa che mostra i ricavi per città evidenziando i dati per la città selezionata.](images/selected-data.png)

1. Scegliere **Save** (Salva) dal menu **File**. Salvare quindi il file con un nome file con estensione pbix appropriato. È possibile aprire il file ed esplorare ulteriormente la modellazione e la visualizzazione dei dati, in base alle proprie esigenze.

Se è disponibile una sottoscrizione del [servizio Power BI](https://www.powerbi.com/?azure-portal=true), è possibile accedere all'account e pubblicare il report in un'area di lavoro di Power BI. 
