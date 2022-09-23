---
lab:
  title: Esplorare il database SQL di Azure
  module: Explore relational data in Azure
---

# <a name="explore-azure-sql-database"></a>Esplorare il database SQL di Azure

In questo esercizio si effettuerà il provisioning di una risorsa del database SQL di Azure nella sottoscrizione di Azure e si userà quindi SQL per eseguire una query delle tabelle nel database relazionale.

Il completamento di questo lab richiederà circa **15** minuti.

## <a name="before-you-start"></a>Prima di iniziare

Sarà necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free) con accesso di livello amministrativo.

## <a name="provision-an-azure-sql-database-resource"></a>Effettuare il provisioning di una risorsa del database SQL di Azure

1. In the <bpt id="p1">[</bpt>Azure portal<ept id="p1">](https://portal.azure.com?azure-portal=true)</ept>, select <bpt id="p2">**</bpt>&amp;#65291; Create a resource<ept id="p2">**</ept> from the upper left-hand corner and search for <bpt id="p3">*</bpt>Azure SQL<ept id="p3">*</ept>. Then in the resulting <bpt id="p1">**</bpt>Azure SQL<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.

1. Esaminare le opzioni di Azure SQL disponibili e quindi nel riquadro **SQL database** verificare che sia selezionato **Database singolo** e selezionare **Crea**.

    ![Screenshot del portale di Azure che mostra la pagina Azure SQL.](images//azure-sql-portal.png)

1. Immettere i valori seguenti nella pagina **Crea database SQL**:
    - **Sottoscrizione** Selezionare la sottoscrizione di Azure.
    - **Gruppo di risorse**: creare un nuovo gruppo di risorse con un nome di propria scelta.
    - **Nome database**: *AdventureWorks*
    - <bpt id="p1">**</bpt>Server<ept id="p1">**</ept>:  Select <bpt id="p2">**</bpt>Create new<ept id="p2">**</ept> and create a new server with a unique name in any available location. Use <bpt id="p1">**</bpt>SQL authentication<ept id="p1">**</ept> and specify your name as the server admin login and a suitably complex password (remember the password - you'll need it later!)
    - **Usare il pool elastico SQL?**: *No*
    - **Calcolo e archiviazione**: lasciare invariati
    - **Ridondanza dell'archivio di backup**: selezionare *Archivio di backup con ridondanza locale*

1. On the <bpt id="p1">**</bpt>Create SQL Database<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Next :Networking &gt;<ept id="p2">**</ept>, and on the <bpt id="p3">**</bpt>Networking<ept id="p3">**</ept> page, in the <bpt id="p4">**</bpt>Network connectivity<ept id="p4">**</ept> section, select <bpt id="p5">**</bpt>Public endpoint<ept id="p5">**</ept>. Then select <bpt id="p1">**</bpt>Yes<ept id="p1">**</ept> for both options in the <bpt id="p2">**</bpt>Firewall rules<ept id="p2">**</ept> section to allow access to your database server from Azure services and your current client IP address.

1. Selezionare **Avanti: Sicurezza >** e impostare l'opzione **Abilita Microsoft Defender for SQL** su **Non ora**.

1. Selezionare **Avanti: Impostazioni aggiuntive>** e nella scheda **Impostazioni aggiuntive** impostare l'opzione **Usa dati esistenti** su **Esempio** per creare un database di esempio che sarà possibile esplorare in un secondo momento.

1. Selezionare **Rivedi e crea** e quindi selezionare **Crea** per creare il database SQL di Azure.

1. Wait for deployment to complete. Then go to the resource that was deployed, which should look like this:

    ![Screenshot del portale di Azure che mostra la pagina Database SQL.](images//sql-database-portal.png)

1. Nel riquadro a sinistra della pagina selezionare **Editor di query (anteprima)** e accedere usando l'account di accesso amministratore e la password specificati per il server.
    
    *Se viene visualizzato un messaggio di errore che informa che l'indirizzo IP client non è consentito, selezionare il collegamento **IP elenco elementi consentiti…** alla fine del messaggio per consentire l'accesso e provare nuovamente ad accedere (in precedenza è stato aggiunto l'indirizzo IP client del computer alle regole del firewall, ma l'editor di query può connettersi da un indirizzo diverso a seconda della configurazione di rete).*
    
    L'editor di query ha un aspetto simile al seguente:
    
    ![Screenshot del portale di Azure che mostra l'editor di query.](images//query-editor.png)

1. Espandere la cartella **Tabelle** per visualizzare le tabelle nel database.

1. Nel riquadro **Query 1** immettere il codice SQL seguente:

    ```sql
    SELECT * FROM SalesLT.Product;
    ```

1. Selezionare **&#9655; Esegui** sopra la query per eseguirla e visualizzare i risultati, che dovrebbero includere tutte le colonne per tutte le righe nella tabella **SalesLT.Product**, come mostrato qui:

    ![Screenshot del portale di Azure che mostra l'editor di query con i risultati della query.](images//sql-query-results.png)

1. Sostituire l'istruzione SELECT con il codice seguente e quindi selezionare **&#9655; Esegui** per eseguire la nuova query ed esaminare i risultati (che includono solo le colonne **ProductID**, **Name**, **ListPrice** e **ProductCategoryID**):

    ```sql
    SELECT ProductID, Name, ListPrice, ProductCategoryID
    FROM SalesLT.Product;
    ```

1. Ora provare la query seguente, che usa un JOIN per ottenere il nome della categoria dalla tabella **SalesLT.ProductCategory**:

    ```sql
    SELECT p.ProductID, p.Name AS ProductName,
            c.Name AS Category, p.ListPrice
    FROM SalesLT.Product AS p
    JOIN [SalesLT].[ProductCategory] AS c
        ON p.ProductCategoryID = c.ProductCategoryID;
    ```

1. Chiudere il riquadro dell'editor di query, rimuovendo le modifiche.

> **Suggerimento**: se è stata completata l'esplorazione di Database SQL di Azure, è possibile eliminare il gruppo di risorse creato in questo esercizio.
