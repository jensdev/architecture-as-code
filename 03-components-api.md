# 🧩 Niveau 3: Componenten (API Backend)

Hier zijn we ingezoomd op de **API Backend (Node.js)**. Dit diagram is specifiek bedoeld voor het backend-team. 

We zien hier hoe de inkomende netwerkverzoeken worden opgevangen door de controllers, hoe de businesslogica is opgesplitst in specifieke services, en hoe de adapters praten met de buitenwereld.

*(👉 **Tip:** Klik op de Booking Service om door te zoomen naar de broncode in Niveau 4.)*

```mermaid
%%{init: {"flowchart": {"defaultRenderer": "elk"}} }%%
flowchart TB
    %% Styling
    classDef container fill:#438dd5,stroke:#2e6295,color:#fff
    classDef component fill:#85bbf0,stroke:#5b93c9,color:#000
    classDef clickableComponent fill:#85bbf0,stroke:#5b93c9,color:#000,cursor:pointer,stroke-width:2px,stroke-dasharray: 5 5
    classDef external fill:#999999,stroke:#666666,color:#fff
    classDef database fill:#438dd5,stroke:#2e6295,color:#fff,shape:cylinder

    WebApp["Web Applicatie
    [Container]"]:::container
    POS["Kassa Applicatie
    [Container]"]:::container
    
    DB[("Database
    [Container]")]:::database
    Betaal["Betaalprovider
    [Systeem]"]:::external
    Mail["E-mail Service
    [Systeem]"]:::external

    %% Onze specifieke Container die we openbreken
    subgraph API_CONTAINER ["API Backend (Node.js)"]
        direction TB
        
        Controller["Ticket Controller
        [Component: Express Router]
        Ontvangt alle inkomende HTTP requests"]:::component
        MovieSvc["Movie Service
        [Component: TypeScript Class]
        Zoekt films en controleert de planning"]:::component
        BookingSvc["Booking Service
        [Component: TypeScript Class]
        Bevat de kernlogica voor reserveringen
        👉 Klik voor Niveau 4 👈"]:::clickableComponent
        
        PaymentAdapter["Payment Adapter
        [Component: TypeScript Class]
        Vertaalt onze data naar Mollie/Adyen formaat"]:::component
        EmailAdapter["Email Adapter
        [Component: TypeScript Class]
        Genereert de HTML voor e-tickets"]:::component
        Repo["Database Repository
        [Component: TypeORM]
        Voert SQL queries uit"]:::component
    end

    %% Relaties van buiten naar binnen
    WebApp -->|"JSON/HTTPS"| Controller
    POS -->|"JSON/HTTPS"| Controller

    %% Interne relaties (Hoe de code samenwerkt)
    Controller -->|"Vraagt filmlijst op via"| MovieSvc
    Controller -->|"Start boeking via"| BookingSvc

    MovieSvc -->|"Haalt data op via"| Repo
    BookingSvc -->|"Slaat reservering op via"| Repo
    
    BookingSvc -->|"Verwerkt betaling via"| PaymentAdapter
    BookingSvc -->|"Verstuurt ticket via"| EmailAdapter

    %% Relaties van binnen naar buiten
    Repo -->|"Leest/Schrijft (SQL)"| DB
    PaymentAdapter -->|"API Call"| Betaal
    EmailAdapter -->|"API Call"| Mail
    
    %% DE LINK NAAR NIVEAU 4 (Vervang URL door jouw repo voor de demo)
    click BookingSvc "[https://github.com/jensdev/architecture-as-code/blob/main/04-code-booking-service.md](https://github.com/jensdev/architecture-as-code/blob/main/04-code-booking-service.md)" "Bekijk de Code Details" _blank
```

🔙 **[Klik hier om terug te gaan naar Niveau 2: Containers](./02-containers.md)**