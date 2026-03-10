# 🧩 Niveau 3: Componenten (Web Applicatie)

Hier zijn we ingezoomd op de **Web Applicatie (React)**. Dit diagram is bedoeld voor de frontend developers.

We zien hier hoe de Single Page Application (SPA) in de browser van de klant is opgebouwd. Het toont de routing, de belangrijkste weergave-componenten, hoe de data lokaal wordt vastgehouden (Redux), en hoe de applicatie praat met onze API.

```mermaid
%%{init: {"flowchart": {"defaultRenderer": "elk"}} }%%
flowchart TB
    classDef container fill:#438dd5,stroke:#2e6295,color:#fff
    classDef component fill:#85bbf0,stroke:#5b93c9,color:#000
    classDef person fill:#08427b,stroke:#052e56,color:#fff

    Klant[("Filmfan
    [Persoon]")]:::person
    API["API Backend
    [Container: Node.js]"]:::container

    subgraph WEB_CONTAINER ["Web Applicatie (React)"]
        direction TB
        
        Router["App Router
        [Component: React Router]
        Beheert welke pagina wordt getoond"]:::component
        
        MovieList["Movie List View
        [Component: React UI]
        Toont de lijst met actuele films"]:::component
        BookingFlow["Booking Flow View
        [Component: React UI]
        Scherm voor de stoelkeuze en winkelmandje"]:::component
        
        Store["Redux Store
        [Component: Redux]
        Beheert de globale 'state' (het winkelmandje)"]:::component
        ApiClient["API Client
        [Component: Axios Hook]
        Verzorgt alle uitgaande HTTP communicatie"]:::component
    end

    Klant -->|"Bekijkt in de browser"| Router
    
    Router -->|"Routet naar"| MovieList
    Router -->|"Routet naar"| BookingFlow

    MovieList -->|"Leest filmlijst uit"| Store
    BookingFlow -->|"Bewaart geselecteerde stoelen in"| Store

    MovieList -->|"Vraagt lijst op via"| ApiClient
    BookingFlow -->|"Verstuurt definitieve boeking via"| ApiClient

    ApiClient -->|"JSON/HTTPS verzoeken"| API
```

🔙 **[Klik hier om terug te gaan naar Niveau 2: Containers](./02-containers.md)**