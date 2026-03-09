# 🌍 Niveau 1: Systeem Context (Bioscoop Ticket Systeem)

Dit is de "wereldkaart" van onze architectuur. Dit diagram is ontworpen om door iedereen binnen het bedrijf begrepen te worden, van de directie tot aan de ontwikkelaars.

We behandelen ons systeem hier als een gesloten doos (*black box*). Het diagram toont uitsluitend het grote plaatje: **wie** gebruikt ons systeem (de actoren) en met welke **externe partijen** communiceren we, zonder dat je wordt afgeleid door technische details.

```mermaid
---
config:
  flowchart:
    defaultRenderer: "elk"
---
flowchart TB
    %% Styling
    classDef person fill:#08427b,stroke:#052e56,color:#fff
    classDef system fill:#1168bd,stroke:#0b4884,color:#fff,cursor:pointer,stroke-width:2px
    classDef external fill:#999999,stroke:#666666,color:#fff

    %% Actoren
    Klant[("Filmfan
    [Persoon]")]:::person
    Kassa[("Bioscoopmedewerker
    [Persoon]")]:::person

    %% Het Hoofdsysteem (Klikbaar)
    TicketSysteem["Bioscoop Ticket Systeem
    [Systeem]
    👉 Klik hier om in te zoomen"]:::system

    %% Externe Systemen
    Betaal["Betaalprovider
    [Systeem]
    (bijv. Mollie / Adyen)"]:::external
    Mail["E-mail Service
    [Systeem]
    (bijv. SendGrid)"]:::external

    %% Relaties
    Klant -->|"Zoekt films & bestelt tickets"| TicketSysteem
    Kassa -->|"Verkoopt tickets aan de balie"| TicketSysteem
    
    TicketSysteem -->|"Verwerkt betalingen via"| Betaal
    TicketSysteem -->|"Stuurt e-tickets via"| Mail

    %% De doorklik-link
    click TicketSysteem "https://github.com/jensdev/architecture-as-code/blob/main/02-containers.md" "Open het Container Diagram" _blank
```