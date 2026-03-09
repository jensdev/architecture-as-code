# 🧩 Niveau 3: Componenten (API Backend)

Hier zoomen we in op één specifieke container uit het vorige niveau: de **API Backend**. 

Dit diagram toont de interne structuur van de Node.js applicatie. Ontwikkelaars kunnen hier zien hoe de code logisch is opgedeeld in controllers, services en repositories, en hoe deze onderdelen samenwerken om een ticket te boeken.

```mermaid
---
config:
  flowchart:
    defaultRenderer: "elk"
---
flowchart TB
    %% Styling
    classDef container fill:#438dd5,stroke:#2e6295,color:#fff
    classDef component fill:#85bbf0,stroke:#5b93c9,color:#000
    classDef external fill:#999999,stroke:#666666,color:#fff
    classDef database fill:#438dd5,stroke:#2e6295,color:#fff,shape:cylinder

    %% Context van buitenaf (Grijze/Blauwe blokken om aan te geven waar we zijn)
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
        Bevat de kernlogica voor reserveringen"]:::component
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
```