# 📦 Niveau 2: Containers (Bioscoop Ticket Systeem)

Hier zoomen we één stap dieper in en openen we de "zwarte doos" van ons hoofdsysteem. Dit overzicht is vooral waardevol voor software architecten, systeembeheerders en ontwikkelaars.

In dit diagram zie je de zogenaamde *deployable units*: de grote, onafhankelijk draaiende onderdelen (containers) waaruit ons systeem bestaat. Het toont de interactie tussen onze frontends, backend API's en databases, en geeft de belangrijkste technologische keuzes (zoals React en Node.js) weer.

```mermaid
%%{init: {"flowchart": {"defaultRenderer": "elk"}} }%%
flowchart TB
    %% Styling
    classDef person fill:#08427b,stroke:#052e56,color:#fff
    classDef container fill:#438dd5,stroke:#2e6295,color:#fff
    classDef external fill:#999999,stroke:#666666,color:#fff
    classDef database fill:#438dd5,stroke:#2e6295,color:#fff,shape:cylinder

    %% Actoren & Externe systemen van Niveau 1 (als context)
    Klant[("Filmfan
    [Persoon]")]:::person
    Kassa[("Bioscoopmedewerker
    [Persoon]")]:::person
    Betaal["Betaalprovider
    [Systeem]"]:::external
    Mail["E-mail Service
    [Systeem]"]:::external

    %% De binnenkant van ons systeem
    subgraph TICKETS ["Bioscoop Ticket Systeem"]
        direction TB
        
        WebApp["Web Applicatie
        [Container: React]
        De website voor de klanten thuis"]:::container
        POS["Kassa Applicatie
        [Container: iPad App]
        Voor de medewerker aan de balie"]:::container
        
        API["API Backend
        [Container: Node.js]
        Het brein dat alle regels beheert"]:::container
        
        DB[("Database
        [Container: PostgreSQL]
        Bewaart films, zalen en stoelen")]:::database
    end

    %% Relaties
    Klant -->|"Bezoekt"| WebApp
    Kassa -->|"Gebruikt"| POS

    WebApp -->|"Haalt films op & boekt via"| API
    POS -->|"Haalt films op & boekt via"| API

    API -->|"Leest/Schrijft data"| DB
    API -->|"Start online betaling"| Betaal
    API -->|"Geeft opdracht voor ticketmail"| Mail

    DB ~~~ Betaal
    DB ~~~ Mail

    %% Maak zowel de WebApp als de API klikbaar (vervang URL met jouw repo)
    click WebApp "https://github.com/jensdev/architecture-as-code/blob/main/03-components-webapp.md" "Bekijk de React Componenten" _blank
    click API "https://github.com/jensdev/architecture-as-code/blob/main/03-components-api.md" "Bekijk de API Componenten" _blank
```