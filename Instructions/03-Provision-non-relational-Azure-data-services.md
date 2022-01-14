---
lab:
    title: 'Lab 03. Effettuare il provisioning dei servizi dati non relazionali di Azure'
    module: 'Modulo 03. Esplorare i dati non relazionali in Azure'
---

## Istruzioni
Nello scenario di esempio si è deciso di creare gli archivi dati seguenti:

* Un database Cosmos DB per l'archiviazione delle informazioni sul volume degli articoli in magazzino. È necessario archiviare informazioni aggiornate e storiche sui livelli dei volumi, in modo da poter tenere traccia delle variazioni dei livelli nel tempo. I dati vengono registrati giornalmente.
* Un archivio Data Lake per l'archiviazione dei dati su produzione e qualità.
* Un contenitore BLOB per l'archiviazione delle immagini dei prodotti realizzati dall'azienda.
* Archiviazione file per la condivisione di report.

In questo lab verranno eseguiti il provisioning e la configurazione dell'account Cosmos DB, che verrà quindi testato creando un database, un contenitore e un documento di esempio. Verrà inoltre eseguito il provisioning di un account di archiviazione di Azure per fornire archiviazione BLOB, file e Data Lake Storage.

1.	Passare all'esercizio su Microsoft Learn all'indirizzo https://aka.ms/dp900lab03-ita e completare l'unità nel browser: 
