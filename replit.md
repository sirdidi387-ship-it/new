# Overview

Questo è un bot AI costruito con Mastra, un framework TypeScript per creare e orchestrare agenti AI. Il progetto fornisce un setup fondamentale per costruire agenti AI conversazionali con supporto per più provider LLM, gestione della memoria e orchestrazione dei workflow tramite Inngest.

L'applicazione include un playground di sviluppo per testare gli agenti ed è configurata per funzionare su Node.js 20.9.0 o superiore con supporto per moduli ES.

# Recent Changes

**06 Ottobre 2025** - Bot riparato e configurato completamente:
- Creata struttura del progetto con file di configurazione
- Implementato script di build (`scripts/build.sh`) per deployment su Render
- Creato agente AI base con modello gpt-4o-mini
- Configurato workflow di sviluppo Mastra
- Aggiunta chiave API OpenAI per funzionamento del bot
- Build di produzione testato con successo

# User Preferences

Lingua preferita: Italiano
Stile di comunicazione: Linguaggio semplice e quotidiano

# Project Architecture

## Struttura File
```
src/
  mastra/
    index.ts         - Configurazione principale Mastra
    agents/
      basic-agent.ts - Agente AI base
scripts/
  build.sh           - Script di build per produzione
```

## Framework Principale
- **Mastra Core**: Framework centrale per gestione agenti, strumenti e integrazioni
- **Sistema Agenti**: Basato sulla classe Agent da @mastra/core/agent
- **Sistema Moduli**: Moduli ES2022 con risoluzione bundler

## Integrazione AI/LLM
- **Provider Principale**: Integrazione OpenAI via @ai-sdk/openai (usando gpt-4o-mini come modello predefinito)
- **Provider Alternativo**: Supporto OpenRouter via @openrouter/ai-sdk-provider
- **AI SDK**: Vercel AI SDK per interazioni LLM standardizzate

## Memoria & Storage
- **Sistema Memoria**: @mastra/memory per cronologia conversazioni
- **Opzioni Database**: PostgreSQL via @mastra/pg, LibSQL via @mastra/libsql
- **Validazione Dati**: Zod per validazione schema runtime

## Orchestrazione Workflow
- **Sistema Eventi**: Inngest per esecuzione workflow affidabile
- **Funzionalità Real-time**: @inngest/realtime per aggiornamenti streaming
- **Integrazione**: @mastra/inngest collega agenti Mastra con workflow Inngest

## Sviluppo & Tooling
- **Sistema Build**: Mastra CLI per sviluppo, build e deployment
- **TypeScript**: Modalità strict abilitata con target ES2022
- **Runtime**: tsx per esecuzione TypeScript veloce durante sviluppo

## Logging & Observability
- **Logging Strutturato**: Logger Pino via @mastra/loggers
- **Telemetria**: Instrumentazione OpenTelemetry in build di produzione

## Architettura Server
- **Server HTTP**: Server basato su Express in esecuzione su porta 5000
- **Playground UI**: Playground di sviluppo integrato con hot-reload via SSE
- **Modalità Produzione**: Output compilato in directory .mastra/output con package.json separato

## Deployment
- **Piattaforma**: Configurato per Render tramite render.yaml
- **Build Command**: `bash scripts/build.sh`
- **Start Command**: `npm start` (esegue node su .mastra/output/index.mjs)
- **Variabili d'Ambiente**: OPENAI_API_KEY (richiesta), NODE_ENV, PORT
