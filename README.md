# 🏗️ Proof of Concept: Architecture-as-Code (C4 Model)

Welkom bij de documentatie van ons architectuur-initiatief! Dit project is een Proof of Concept (PoC) om te demonstreren hoe we onze systeemarchitectuur overzichtelijker, interactiever en beter onderhoudbaar kunnen maken in GitHub.

## 🎯 Het Probleem & De Oplossing
Vaak groeien onze architectuurtekeningen uit tot complexe "spaghettidiagrammen" waarin eindgebruikers, netwerkinfrastructuur en specifieke codeblokken door elkaar lopen. Dit maakt het lastig om overzicht te houden, afdelingen op één lijn te krijgen en nieuwe collega's soepel in te werken.

De oplossing is **Architecture-as-Code** met behulp van het **C4-model** en **Mermaid**. 

## 🗺️ De "Google Maps" Aanpak
In plaats van één grote, onleesbare poster, knippen we de architectuur op in logische zoom-niveaus. Je begint met een hoog-over vogelvluchtperspectief en klikt simpelweg op de blokken om in te zoomen op de techniek:

* **Niveau 1: Systeem Context** - De businesswaarde: Wie gebruikt het systeem en met welke externe partijen integreren we?
* **Niveau 2: Containers** - De applicatie-architectuur: Welke apps, API's en databases draaien er onder de motorkap?
* **Niveau 3: Componenten** - De interne structuur: Uit welke microservices of logische modules bestaat een specifieke applicatie?

Omdat we dit met Mermaid-syntax schrijven, leeft de documentatie als platte tekst naast onze broncode. Wijzigt de architectuur? Dan updaten we de documentatie in dezelfde Pull Request.

## 🚀 Bekijk de Demo
Om dit in de praktijk te laten zien, hebben we een herkenbaar voorbeeld uitgewerkt: een **Bioscoop Ticket Systeem**. 

Klik op de link hieronder om de interactieve reis te beginnen. *(Let op: in de diagrammen kun je op de donkerblauwe blokken klikken om een niveau dieper in te zoomen!)*

👉 **[Start de demo: Open het Niveau 1 - Context Diagram](./01-context.md)**