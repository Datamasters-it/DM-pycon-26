<a target="_blank" rel="noopener noreferrer" href="https://colab.research.google.com/github/Datamasters-it/DM-pycon-26/blob/main/beginners-day/Student_Pycon_2026_Beginners_Day.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

# Creiamo un Agente AI da zero con Python

Benvenuti al repository del **Beginner's Day**, l'evento di apertura di **PyCon Italia 2026** 
*by Data Masters*   <img src="https://s3-eu-west-1.amazonaws.com/tpd/logos/60c784605fd8980001d96a17/0x0.png" width=20 >

Questo workshop guida passo passo nella costruzione di un piccolo **Travel Agent AI**: un assistente capace di usare funzioni Python, chiamare API REST gratuite, recuperare dati reali su città, meteo e paesi, calcolare budget di viaggio e produrre consigli pratici per la valigia.

Il percorso è pensato per chi ha basi di Python e vuole capire, in modo pratico, come passare da una semplice funzione a un agente AI costruito con **LangChain** e `create_agent()`.

## Obiettivo del Workshop

L'obiettivo principale è fornire una comprensione pratica di:

* Come configurare un modello LLM locale in ambiente notebook con **Ollama**.  
* Come collegare LangChain a un modello tramite `init_chat_model()`.  
* Come trasformare normali funzioni Python in strumenti utilizzabili da un agente con `@tool`.  
* Come funziona il ciclo **ReAct**: Reason → Act → Observe.  
* Come chiamare API REST gratuite con `requests`.  
* Come costruire tool riusabili per:  
  * geocoding di una città;  
  * meteo corrente;  
  * informazioni su paesi, capitali, lingue e valute;  
  * calcolo del budget di viaggio;  
  * suggerimenti deterministici per la valigia.  
* Come assemblare più tool in un unico agente con `create_agent()`.  
* Come osservare l'esecuzione dell'agente con `invoke()` e `stream()`.  
* Come rendere l'agente più affidabile nella gestione di errori e input ambigui.  
* Come aggiungere memoria conversazionale con `InMemorySaver` e `thread_id`.

Il focus è sull'apprendimento pratico: ogni concetto viene introdotto con una breve spiegazione e poi applicato direttamente nel notebook.

## Cosa Costruiremo

Durante il workshop costruiremo un **Travel Agent** che può rispondere a domande come:

```
Preparami una scheda per 3 giorni a Barcellona con 80 euro al giorno.
```

L'agente sarà in grado di:

1. riconoscere la destinazione citata dall'utente;  
2. trovare latitudine, longitudine e timezone della città;  
3. recuperare il meteo corrente;  
4. ottenere informazioni sul paese, come capitale, valuta e lingue;  
5. calcolare il budget totale del viaggio;  
6. suggerire cosa mettere in valigia in base alle condizioni meteo;  
7. restituire una risposta finale organizzata in italiano.

## Contenuto del Notebook

Il notebook è strutturato in passaggi progressivi.

### 1\. LLM in locale con Ollama

* Installazione e configurazione di Ollama in ambiente Colab.  
* Avvio di `ollama serve` in background.  
* Download del modello locale usato nel workshop.  
* Collegamento tra LangChain e il modello locale.

### 2\. Primo tool Python: budget di viaggio

* Introduzione al concetto di **tool**.  
* Uso di `@tool` per trasformare una funzione Python in uno strumento per l'agente.  
* Creazione del tool `calculate_trip_budget`.  
* Primo agente con un solo tool.

### 3\. API REST in Python: geocoding

* Anatomia di una richiesta HTTP con `requests.get()`.  
* Uso dell'API gratuita di geocoding di Open-Meteo.  
* Creazione di una funzione wrapper `get_json`.  
* Creazione del tool `search_city_tool`.

### 4\. API meteo: Open-Meteo Forecast

* Recupero del meteo corrente a partire da latitudine e longitudine.  
* Interpretazione dei codici meteo.  
* Creazione del tool `get_current_weather_tool`.

### 5\. API paesi: REST Countries

* Recupero di capitale, valuta, lingue, popolazione e timezone.  
* Creazione del tool `get_country_info_tool`.  
* Gestione di nomi paese in italiano o inglese.

### 6\. Tool deterministici: cosa mettere in valigia

* Quando conviene usare codice Python invece del modello.  
* Regole `if/else` per suggerire vestiti e accessori.  
* Creazione del tool `suggest_packing_items`.

### 7\. Travel Agent con `create_agent()`

* Assemblaggio di tutti i tool in un unico agente.  
* Scrittura del system prompt.  
* Uso del modello per decidere quali tool chiamare e in quale ordine.  
* Demo di una scheda viaggio completa.

### 8\. Streaming e debug

* Differenza tra `invoke()` e `stream()`.  
* Visualizzazione dei passaggi intermedi dell'agente.  
* Osservazione di tool call, risultati e risposta finale.

### 9\. Affidabilità e gestione degli errori

* Test con città inesistenti, input numerici non validi e richieste ambigue.  
* Uso di risposte `ok=False` nei tool.  
* Strategie per evitare che l'agente inventi dati.

### 10\. Output strutturato

* Creazione di un formato fisso per la scheda viaggio.  
* Prompting per ottenere risposte più leggibili e consistenti.

### 11\. Memoria conversazionale

* Introduzione a `InMemorySaver`.  
* Uso di `thread_id` per separare conversazioni diverse.  
* Differenza tra memoria in RAM e memoria persistente.  
* Limiti legati alla context window del modello.

## Come Utilizzare il Notebook

### 1\. Ambiente consigliato

Il workshop è pensato per essere eseguito in **Google Colab**, così tutti possono partire dallo stesso ambiente senza configurazioni locali complesse.

È comunque possibile eseguirlo anche in locale, a patto di avere:

* Python 3.10 o successivo;  
* Jupyter Notebook o JupyterLab;  
* Ollama installato;  
* accesso a Internet per scaricare il modello e chiamare le API REST.

### 2\. Installazione delle librerie

Nel notebook sono già presenti le celle di installazione necessarie. Le librerie principali sono:

```shell
pip install langchain_ollama langchain_community
```

In base alla versione dell'ambiente, potrebbe essere utile installare anche:

```shell
pip install langchain langgraph requests
```

### 3\. Avvio di Ollama

Nel notebook viene configurato Ollama direttamente da Colab. Il flusso generale è:

```shell
curl -fsSL https://ollama.com/install.sh | sh
ollama serve
ollama pull <nome-modello>
```

Nel notebook l'avvio del server Ollama viene gestito in background tramite Python, così è possibile continuare a eseguire le celle successive.

### 4\. API utilizzate

Il workshop utilizza API gratuite e senza API key:

| API | Utilizzo | Richiede account? |
| :---- | :---- | :---- |
| Open-Meteo Geocoding | Ricerca coordinate da nome città | No |
| Open-Meteo Forecast | Meteo corrente da coordinate | No |
| REST Countries | Informazioni su paesi, capitali, lingue e valute | No |

Questo rende il workshop adatto a un ambiente didattico: non servono credenziali personali e non ci sono file esterni da caricare.

## Ordine Consigliato di Esecuzione

1. Apri il notebook in Google Colab o Jupyter.  
2. Esegui le celle di configurazione di Ollama.  
3. Installa le librerie Python richieste.  
4. Inizializza il modello con LangChain.  
5. Crea ed esegui il primo tool locale.  
6. Costruisci il primo agente con `create_agent()`.  
7. Aggiungi progressivamente i tool basati su API.  
8. Assembla il Travel Agent completo.  
9. Prova le demo guidate.  
10. Sperimenta con nuove domande, nuove città e nuovi tool.

## Idee per Estendere il Progetto

Una volta completato il workshop, puoi estendere il Travel Agent in molti modi:

* Aggiungere un tool per stimare il costo dei voli.  
* Integrare informazioni sui trasporti pubblici.  
* Aggiungere un calendario di viaggio giorno per giorno.  
* Salvare le schede viaggio generate in file Markdown o PDF.  
* Sostituire `InMemorySaver` con una memoria persistente.  
* Creare una piccola interfaccia web con Streamlit o Gradio.  
* Cambiare dominio: food agent, study agent, logistics agent, coding assistant.

## Troubleshooting

### Ollama non risponde

Verifica che il server sia partito correttamente e che `ollama serve` sia in esecuzione.

### Il modello non viene trovato

Controlla il nome del modello scaricato con:

```shell
ollama list
```

Poi verifica che lo stesso nome venga usato nella configurazione di LangChain.

### Le API non restituiscono risultati

Controlla:

* che il nome della città o del paese sia scritto correttamente;  
* che ci sia connessione Internet;  
* che il tool gestisca il caso in cui la lista dei risultati sia vuota.

### L'agente inventa informazioni

Rafforza il system prompt con regole esplicite, ad esempio:

```
Non inventare meteo, capitali, valute o numeri. Se non hai dati dai tool, dillo chiaramente.
```

## Takeaway Finali

Alla fine del workshop avrai visto cinque pattern fondamentali:

* `@tool`: nome, docstring e type hints rendono una funzione usabile da un agente.  
* **ReAct**: l'agente alterna ragionamento, azione e osservazione.  
* `requests.get()`: poche righe di Python permettono di parlare con API reali.  
* `create_agent()`: assembla modello, tool e prompt in un agente operativo.  
* `thread_id`: separa conversazioni diverse e abilita una memoria di breve periodo.

## Risorse Utili

* [LangChain Documentation](https://python.langchain.com/)  
* [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)  
* [Ollama](https://ollama.com/)  
* [Open-Meteo](https://open-meteo.com/)  
* [REST Countries](https://restcountries.com/)  
* [PyCon Italia](https://pycon.it/)  
* [Datamasters](https://datamasters.it/)

## A chi è rivolto

Questo workshop è pensato per partecipanti beginner/intermediate che:

* conoscono le basi di Python;  
* hanno usato almeno una volta un notebook;  
* vogliono capire come funzionano gli agenti AI senza partire da framework complessi;  
* preferiscono imparare costruendo un progetto concreto.

Non è necessario avere esperienza precedente con LangChain, Ollama o sviluppo di agenti AI.

## Licenza

Materiale didattico creato per il Beginner's Day di PyCon Italia 2026\. Verifica la licenza della repository prima di riutilizzare o distribuire il materiale.  
