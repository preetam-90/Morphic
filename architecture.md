# Application Architecture

```mermaid
graph TD
    subgraph "User Interface (Next.js/React)"
        A[Chat Component] --> B{useChat Hook};
        B --> C[ChatMessages];
        B --> D[ChatPanel];
    end

    subgraph "Backend (Next.js API Routes)"
        E[/api/chat] --> F{Model & Search Mode Detection};
        F --> G{Tool Calling Logic};
        G -- Native --> H[createToolCallingStreamResponse];
        G -- Manual --> I[createManualToolStreamResponse];
    end

    subgraph "AI Core"
        H --> J[Researcher Agent];
        I --> K[Manual Researcher Agent];
        J --> L{LLM};
        K --> L;
        L --> M[AI/LLM Providers];
    end

    subgraph "Services"
        M[AI/LLM Providers]
        N[Supabase Auth & DB]
        O[Redis Cache]
        P[Web Search/Video Search Tools]
    end

    A --> E;
    E --> N;
    E --> O;
    J --> P;
    K --> P;
```

This diagram illustrates the flow of information from the user interface to the backend, through the AI core, and out to the various external services.