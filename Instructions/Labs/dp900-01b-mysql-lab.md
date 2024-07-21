---
lab:
  title: Esplorare Database di Azure per MySQL
  module: Explore relational data in Azure
---

# Esplorare Database di Azure per MySQL

In questo esercizio si effettuerà il provisioning di una risorsa di Database di Azure per MySQL nella sottoscrizione personale di Azure.

Il completamento di questo lab richiederà circa **5** minuti.

## Prima di iniziare

Sarà necessaria una [sottoscrizione di Azure](https://azure.microsoft.com/free) con accesso di livello amministrativo.

## Effettuare il provisioning di una risorsa di Database di Azure per MySQL

In questo esercizio si effettuerà il provisioning di una risorsa di Database di Azure per MySQL.

1. Nel portale di Azure selezionare **&#65291; Crea una risorsa** nell'angolo in alto a sinistra e cercare *Database di Azure per MySQL*. Nella pagina **Database di Azure per MySQL** selezionare **Crea**.

1. Esaminare le opzioni di Database di Azure per MySQL disponibili. In **Tipo di risorsa** selezionare quindi **Server flessibile** e infine **Crea**.

    ![Screenshot delle opzioni di distribuzione di Database di Azure per MySQL](images/mysql-options.png)

1. Immettere i valori seguenti nella pagina **Crea database SQL**:
    - **Sottoscrizione**: selezionare una sottoscrizione di Azure.
    - **Gruppo di risorse**: creare un nuovo gruppo di risorse con un nome di propria scelta.
    - **Nome server**: immettere un nome univoco.
    - **Area:** qualsiasi posizione disponibile nelle vicinanze.
    - **Versione di MySQL**: lasciare invariata.
    - **Tipo di carico di lavoro**: per progetti di sviluppo o hobby.
    - **Calcolo e archiviazione**: lasciare invariati.
    - **Zona di disponibilità**: lasciare invariata.
    - **Abilita disponibilità elevata**: lasciare invariata.
    - **Nome utente amministratore**: il proprio nome
    - **Password** e **Conferma password**: una password adeguatamente complessa

1. Selezionare **Avanti: Rete**.

1. In **Regole del firewall** selezionare **&#65291; Aggiungere l'indirizzo IP client corrente**.

1. Selezionare **Rivedi e crea** e quindi selezionare **Crea** per creare il database MySQL di Azure.

1. Attendere il completamento della distribuzione. Passare quindi alla risorsa distribuita, che dovrebbe essere simile alla seguente:

    ![Screenshot del portale di Azure che mostra la pagina Database di Azure per MySQL.](images/mysql-portal.png)

1. Esaminare le opzioni per la gestione della risorsa di Database di Azure per MySQL.

> **Suggerimento**: se è stata completata l'esplorazione di Database di Azure per MySQL, è possibile eliminare il gruppo di risorse creato in questo esercizio.
