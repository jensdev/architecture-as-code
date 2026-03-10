# 💻 Niveau 4: Code (Booking Service)

We zijn nu aangekomen op het diepste niveau van ons bioscoop-voorbeeld. Dit diagram is puur bedoeld voor de ontwikkelaar die verantwoordelijk is voor de implementatie van de kern-boekingslogica.

We zoomen hier in op de interne structuur van het **Booking Service** component dat we zagen in het vorige diagram. We behandelen hier niet de gehele code, maar uitsluitend het cruciale traject om een ticket te boeken. 

Dit diagram toont de daadwerkelijke klassen (interfaces) en hun belangrijkste methodes. 

*(👉 **Tip:** Klik op de knop onderaan om terug te gaan naar het Componenten-diagram.)*

```mermaid
%%{init: {"flowchart": {"defaultRenderer": "elk"}} }%%
classDiagram
    %% Styling (Kleuren om het visueel strakker te maken)
    class BookingService {
        <<Service Class>>
        %% Publieke methode (de kern-functionaliteit)
        +bookTicket(userId: String, movieId: String, seatNumber: String): Ticket
        %% Private methodes (interne hulpfuncties)
        -calculateTicketPrice(age: int, basePrice: float): float
        -validateAgeRestriction(userAge: int, movieRating: String): boolean
    }

    class DatabaseRepository {
        <<Interface>>
        +getMovie(id: String): Movie
        +getUser(id: String): User
        +saveTicket(ticket: Ticket): void
        +isSeatAvailable(movieId: String, seatNumber: String): boolean
    }

    class PaymentGatewayAdapter {
        <<Interface>>
        +processPayment(amount: float, userId: String): PaymentResult
    }

    class EmailServiceAdapter {
        <<Interface>>
        +generateETicketMail(ticket: Ticket): MailContent
        +sendMail(mail: MailContent): void
    }

    %% De Data Transfer Objects (DTO's) / Entities
    class Ticket {
        +ticketId: String
        +seatNumber: String
        +price: float
        +isPaid: boolean
    }

    class User {
        +userId: String
        +birthDate: Date
        +getAge(): int
    }

    class Movie {
        +movieId: String
        +rating: String (bijv. '16+')
        +basePrice: float
    }

    %% Hoe de code samenwerkt (interacties)
    BookingService --> DatabaseRepository : "gebruikt voor data"
    BookingService --> PaymentGatewayAdapter : "verwerkt betaling via"
    BookingService --> EmailServiceAdapter : "stuurt bevestiging via"
    
    DatabaseRepository ..> Movie : "haalt op"
    DatabaseRepository ..> User : "haalt op"
    DatabaseRepository ..> Ticket : "slaat op"
    
    BookingService ..> Ticket : "maakt aan"
```

*(Kijk in het diagram hierboven voor de specifieke code-implementatie)*

🔙 **[Klik hier om terug te gaan naar Niveau 3: Componenten](https://github.com/jensdev/architecture-as-code/blob/main/03-components-api.md)**