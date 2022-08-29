---
lab:
  title: Esplorare Analisi di flusso di Azure
  module: Explore data analytics in Azure
---

## <a name="explore-azure-stream-analytics"></a>Esplorare Analisi di flusso di Azure

In questo esercizio si effettuerà il provisioning di un processo di Analisi di flusso di Azure nella sottoscrizione di Azure e lo si userà per elaborare un flusso di dati in tempo reale.

> <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: The exercise is part of a module on Microsoft Learn, and includes an option to use a <bpt id="p2">*</bpt>sandbox<ept id="p2">*</ept> Azure subscription. However, if you are completing this exercise as part of an instructor-led class, you should use the Azure subscription provided as part of the class instead of the sandbox.

Prima di iniziare l'esercizio in Microsoft Learn, sarà necessario preparare un ambiente Cloud Shell per la sottoscrizione di Azure.

1. Accedere alla sottoscrizione di Azure nel [portale di Azure](https://portal.azure.com) all'indirizzo `https://portal.azure.com`, usando le credenziali della sottoscrizione di Azure.
2. Use the <bpt id="p1">**</bpt>[<ph id="ph1">\&gt;</ph>_]<ept id="p1">**</ept> button to the right of the search bar at the top of the page to create a new Cloud Shell in the Azure portal, selecting a <bpt id="p2">***</bpt>Bash<ept id="p2">***</ept> environment and creating storage if prompted. The cloud shell provides a command line interface in a pane at the bottom of the Azure portal, as shown here:

    ![Portale di Azure con un riquadro di Cloud Shell](./images/cloud-shell.png)

3. Note that you can resize the cloud shell by dragging the separator bar at the top of the pane, or by using the <bpt id="p1">**</bpt>&amp;#8212;<ept id="p1">**</ept>, <bpt id="p2">**</bpt>&amp;#9723;<ept id="p2">**</ept>, and <bpt id="p3">**</bpt>X<ept id="p3">**</ept> icons at the top right of the pane to minimize, maximize, and close the pane. For more information about using the Azure Cloud Shell, see the <bpt id="p1">[</bpt>Azure Cloud Shell documentation<ept id="p1">](https://docs.microsoft.com/azure/cloud-shell/overview)</ept>.

4. A questo punto si è pronti per completare l'esercizio in Microsoft Learn: è sufficiente usare Cloud Shell nel portale di Azure invece della shell vuota nel modulo di Learn (disponibile per gli studenti autogestiti che usano una sottoscrizione sandbox).

    Usare il collegamento seguente per aprire l'esercizio in Microsoft Learn.

    **[Vai a Microsoft Learn](https://docs.microsoft.com/learn/modules/explore-fundamentals-stream-processing/5-exercise-stream-analytics#create-azure-resources)**

> **Approfondimenti**: con più a tempo a disposizione, valutare la possibilità di tornare a questo modulo di Microsoft Learn e di provare gli altri esercizi disponibili, tra cui l'esplorazione di Spark Streaming e di Esplora dati di Azure Synapse.
