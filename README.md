# DM-PyCon 26

Materiali ufficiali di **Data Masters** per **PyCon Italia 2026**.

Il repository raccoglie i materiali dei tre talk/workshop presentati all'evento: un workshop hands-on sugli agenti AI in Python, un caso d'uso reale di un ristorante data-driven con n8n, e una guida pratica al fine-tuning di LLM su hardware limitato.

---

## Contenuto

### [Beginner's Day](./beginners-day/)

Workshop pensato per chi conosce le basi di Python e vuole capire come funzionano gli agenti AI costruendone uno da zero.

Il percorso guida alla creazione di un **Travel Agent** capace di rispondere a domande come *"Preparami una scheda per 3 giorni a Barcellona con 80 euro al giorno"*, usando LangChain, Ollama e API REST gratuite.

**Tecnologie:** Python · LangChain · LangGraph · Ollama · Open-Meteo · REST Countries

---

### [Tigella Data-Driven](./tigella-data-driven/)

Demo di un agente AI reale per un ristorante immaginario: la **Tigelleria Artificiale**.

Il workflow n8n integra RAG sul menù, un agente con memoria e strumenti esterni, e risponde tramite Telegram con consigli sui piatti, generazione di token ordine e QR code.

**Tecnologie:** n8n · LangChain nodes · Ollama · OpenAI / Mistral · Telegram · OpenWeatherMap

---

### [Fine-Tuning di LLM su Budget Limitato](./finr-tuning-llm-budget-limitato/)

Mini-guida pratica al fine-tuning di un LLM con risorse hardware minime: insegna a **Gemma 4 E2B** (5.1B parametri) il canone della *Pizza del Programmatore* tramite **QLoRA** su Google Colab T4 free.

Il notebook copre l'intera pipeline: diagnosi del modello base, tabella decisionale prompting / RAG / fine-tuning, teoria di LoRA e quantizzazione 4-bit, setup QLoRA con `bitsandbytes`, training con `trl` e valutazione del modello fine-tunato.

**Tecnologie:** Python · Hugging Face Transformers · PEFT · TRL · BitsAndBytes · Google Colab

---

## Chi siamo

[Data Masters](https://datamasters.it/) è una community italiana dedicata a data science, machine learning e intelligenza artificiale.

![Data Masters logo](https://s3-eu-west-1.amazonaws.com/tpd/logos/60c784605fd8980001d96a17/0x0.png)
