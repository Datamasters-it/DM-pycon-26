# TigellAI

Agente AI per la **Tigelleria Artificiale**: un caso d'uso reale e completo di ristorante data-driven, presentato al **Beginner's Day di PyCon Italia 2026** by Data Masters.

Il progetto mostra come costruire un assistente intelligente per un ristorante usando **n8n**, RAG sul menù, memoria conversazionale e integrazioni esterne — senza scrivere un'applicazione da zero.

---

## Contenuto della cartella

| File | Descrizione |
|------|-------------|
| `TigellAI.json` | Workflow n8n importabile — l'intera logica dell'agente |
| `slides.pptx` | Slide della presentazione |
| `tigelleria_artificiale_menu.pdf` | Menù del ristorante usato come knowledge base RAG |

---

## Come funziona

### 1. Caricamento del menù (RAG)

Un form trigger riceve il PDF del menù, ne estrae il testo e lo indicizza in un **vector store in-memory** usando embedding Ollama (`nomic-embed-text`). Da questo momento l'agente può rispondere a domande sui piatti con dati reali, non inventati.

### 2. Agente AI

Il cuore del workflow è un **AI Agent** (LangChain in n8n) con:

- **Memoria conversazionale** — buffer window per ricordare il contesto della sessione
- **RAG sul menù** — recupera i piatti rilevanti prima di rispondere
- **Meteo in tempo reale** — integrazione OpenWeatherMap per suggerire piatti caldi o freschi in base alla temperatura
- **Tool Think** — ragionamento intermedio prima di dare la risposta finale
- **Contesto emotivo** — analisi del tono del messaggio per adattare lo stile di risposta

Il modello LLM usato è configurabile: nel workflow sono presenti sia **OpenAI** che **Mistral Cloud**.

### 3. Human-in-the-Loop

Il nodo HIL permette di intercettare la risposta dell'agente prima che venga inviata, utile per moderazione o demo live.

### 4. Risposta via Telegram

L'agente risponde al cliente su **Telegram** con:
- testo della risposta, firmato *"Powered by TigellAI ✨"*
- **token ordine** generato via codice
- **QR code** dell'ordine, inviato come immagine

---

## Come importare il workflow

1. Apri la tua istanza n8n.
2. Vai su **Workflows → Import from file**.
3. Carica `TigellAI.json`.
4. Configura le credenziali richieste:
   - Telegram Bot API
   - Ollama (URL dell'istanza locale)
   - OpenAI o Mistral Cloud API key
   - OpenWeatherMap API key
5. Avvia il workflow e invia un messaggio al bot Telegram.

---

## Risorse

- [n8n Documentation](https://docs.n8n.io/)
- [Ollama](https://ollama.com/)
- [OpenWeatherMap API](https://openweathermap.org/api)
- [PyCon Italia](https://pycon.it/)
- [Datamasters](https://datamasters.it/)
