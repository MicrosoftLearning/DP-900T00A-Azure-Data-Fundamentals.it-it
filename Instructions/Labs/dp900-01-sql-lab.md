---
lab:
  title: Esplorare il database SQL di Azure
  module: Explore relational data in Azure
---

# Esplorare il database SQL di Azure

In questo lab si apprenderà come effettuare il provisioning di un database SQL di Azure e interagire con esso usando query SQL. Si userà il database di esempio Microsoft AdventureWorks, che fornisce tabelle e dati precompilato, in modo da potersi concentrare sull'esplorazione e l'esecuzione di query sui dati relazionali senza dover creare uno schema personalizzato o inserire record di esempio. Questo approccio mantiene le cose semplici e consente di concentrarsi sulla comprensione dei concetti di base del database e della sintassi SQL.

Il completamento di questo lab richiederà circa **15** minuti.

## Prima di iniziare

Sarà necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free) con accesso di livello amministrativo.

## Effettuare il provisioning di una risorsa del database SQL di Azure

1. [Nella portale di Azure](https://portal.azure.com?azure-portal=true) selezionare **&#65291; Creare una risorsa** dall'angolo superiore sinistro e cercare `Azure SQL`. Nella pagina **Azure SQL** risultante selezionare **Crea**.

    ![Screenshot del portale di Azure che mostra Azure SQL nel marketplace](images/azure-sql-marketplace.png)

1. Esaminare le opzioni di Azure SQL disponibili e quindi nel riquadro **SQL database** verificare che sia selezionato **Database singolo** e selezionare **Crea**.

    ![Screenshot del portale di Azure che mostra la pagina Azure SQL.](images/azure-sql-portal.png)

    > _**Suggerimento**: il database singolo è il più semplice e veloce da configurare per questo lab. Le altre opzioni aggiungono impostazioni non necessarie._

1. Immettere i valori seguenti nella pagina **Crea database SQL** e lasciare tutte le altre proprietà con l'impostazione predefinita:
    - **Sottoscrizione**: selezionare una sottoscrizione di Azure.
    - **Gruppo di risorse**: creare un nuovo gruppo di risorse con un nome di propria scelta.
    - **Nome del database**: `AdventureWorks`
    - **Server**: selezionare **Crea nuovo** e creare un nuovo server con un nome univoco in qualsiasi posizione disponibile. Usare **Autenticazione SQL** e specificare il proprio nome come account di accesso amministratore server e una password adeguatamente complessa (da ricordare perché sarà necessaria più avanti).
    - **Usare il pool elastico SQL?**: *No*
    - **Ambiente del carico di lavoro**: Sviluppo
    - **Calcolo e archiviazione**: lasciare invariati
    - **Ridondanza dell'archivio di backup**: selezionare *Archivio di backup con ridondanza locale*

    > _**Suggerimento**: l'autenticazione SQL è rapida da configurare per l'ultima (nessun passaggio aggiuntivo per Microsoft Entra ID). Le impostazioni predefinite di sviluppo sono più economiche e veloci. Il backup locale è la scelta a basso costo e va bene per un database di procedure temporanee._

1. Nella pagina **Crea database SQL** selezionare **Avanti: Rete >** e quindi nella pagina **Rete**, nella sezione **Connettività di rete**, selezionare **Endpoint pubblico**. Selezionare quindi **Sì** per entrambe le opzioni nella sezione **Regole del firewall** per consentire l'accesso al server di database dai servizi di Azure e dall'indirizzo IP client corrente.

    ![Screenshot del portale di Azure che mostra le impostazioni di rete per il database SQL](images/sql-database-network.png)

    > _**Suggerimento**: endpoint pubblico e consentire l'indirizzo IP consente di connettersi subito. Buono per un breve laboratorio. Nei progetti reali si blocca in genere l'accesso in modo più basso._

1. Selezionare **Avanti: Sicurezza >** e impostare l'opzione **Abilita Microsoft Defender for SQL** su **Non ora**.

    > _**Suggerimento**: Defender è un componente aggiuntivo per la sicurezza a pagamento. Lo saltiamo qui per mantenere le cose semplici ed evitare costi in un breve esercizio._

1. Selezionare **Avanti: Impostazioni aggiuntive>** e nella scheda **Impostazioni aggiuntive** impostare l'opzione **Usa dati esistenti** su **Esempio** per creare un database di esempio che sarà possibile esplorare in un secondo momento.

    > _**Suggerimento**: i dati di esempio offrono tabelle e righe pronte per iniziare subito a eseguire query._

1. Selezionare **Rivedi e crea** e quindi selezionare **Crea** per creare il database SQL di Azure.

1. Attendere il completamento della distribuzione. Passare quindi alla risorsa distribuita, che dovrebbe essere simile alla seguente:

    ![Screenshot del portale di Azure che mostra la pagina Database SQL.](images/sql-database-portal.png)

1. Nel riquadro a sinistra della pagina selezionare **Editor di query (anteprima)** e accedere usando l'account di accesso amministratore e la password specificati per il server.
    
    >**Nota**: se viene visualizzato un messaggio di errore che informa che l'indirizzo IP del client non è consentito, selezionare il **collegamento Allowlist IP ...** alla fine del messaggio per consentire l'accesso e tentare di accedere di nuovo (in precedenza è stato aggiunto l'indirizzo IP client del proprio computer alle regole del firewall, ma l'editor di query può connettersi da un indirizzo diverso a seconda della configurazione di rete).
    
    L'editor di query ha un aspetto simile al seguente:
    
    ![Screenshot del portale di Azure che mostra l'editor di query.](images/query-editor.png)

1. Espandere la cartella **Tabelle** per visualizzare le tabelle nel database.

1. Nel riquadro **Query 1** immettere il codice SQL seguente:

    ```sql
   SELECT * FROM SalesLT.Product;
    ```

    > _**Suggerimento**: SELECT * mostra rapidamente ogni colonna e alcuni valori. Nelle app reali in genere si evita e si selezionano solo le colonne necessarie._

1. Selezionare **&#9655; Esegui** sopra la query per eseguirla e visualizzare i risultati, che dovrebbero includere tutte le colonne per tutte le righe nella tabella **SalesLT.Product**, come mostrato qui:

    ![Screenshot del portale di Azure che mostra l'editor di query con i risultati della query.](images/sql-query-results.png)

1. Sostituire l'istruzione SELECT con il codice seguente e quindi selezionare **&#9655; Esegui** per eseguire la nuova query ed esaminare i risultati (che includono solo le colonne **ProductID**, **Name**, **ListPrice** e **ProductCategoryID**):

    ```sql
   SELECT ProductID, Name, ListPrice, ProductCategoryID
   FROM SalesLT.Product;
    ```

    > _**Suggerimento**: elencare solo le colonne necessarie mantiene i risultati più piccoli e può essere eseguito più velocemente._

1. Ora provare la query seguente, che usa un JOIN per ottenere il nome della categoria dalla tabella **SalesLT.ProductCategory**:

    ```sql
    SELECT 
        p.ProductID, 
        p.Name AS ProductName,
        c.Name AS Category, 
        p.ListPrice
    FROM SalesLT.Product AS p
    INNER JOIN SalesLT.ProductCategory AS c 
        ON p.ProductCategoryID = c.ProductCategoryID;
    ```

    > _**Suggerimento**: join mostra come eseguire il pull dei dati correlati (il nome della categoria) da un'altra tabella usando un ID corrispondente._

1. Chiudere il riquadro dell'editor di query, rimuovendo le modifiche.

> _**Suggerimento**: se è stata completata l'esplorazione database SQL di Azure, è possibile eliminare il gruppo di risorse creato in questo esercizio. L'eliminazione del gruppo di risorse rimuove tutte le risorse in un unico passaggio. Riduce anche i costi._
