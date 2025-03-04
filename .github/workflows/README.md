# TO DO LIST AZURE

## Diagram Aktorów (Use Case Diagram)

```mermaid
graph TD
    A[Użytkownik] --> B(Zarejestruj się)
    A --> C(Zaloguj się)
    A --> D(Dodaj zadanie)
    A --> E(Edytuj zadanie)
    A --> F(Usuń swoje zadanie)
    A --> G(Wyświetl zadania grupy)
    A --> H(Przydziel zadanie do grupy)
    A --> I(Dołącz do grupy)
```
```mermaid    
    J[Administrator] --> K(Zarządzaj użytkownikami)
    J --> L(Usuń dowolne zadanie)
    J --> M(Wyświetl wszystkich użytkowników)
    J --> N(Blokuj/Odblokuj użytkownika)
    J --> O(Zarządzaj grupami)
```

## Diagram Sekwencji

```mermaid
sequenceDiagram
    participant U as Użytkownik
    participant A as Aplikacja
    participant G as Grupa
    participant C as Chmura
    U->>A: Tworzy zadanie i wybiera grupę
    A-->>U: Potwierdza wprowadzenie
    A->>G: Przydziela zadanie do grupy
    G->>C: Szyfruje i zapisuje zadanie
    C-->>G: Potwierdza zapis
    G-->>A: Aktualizuje listę zadań grupy
    A-->>U: Wyświetla zadania grupy
```

## Diagram Klas

```mermaid
classDiagram
    class User {
        +String id
        +String username
        +String hashedPassword
        +login()
        +register()
        +joinGroup()
    }
    class Task {
        +String id
        +String userId
        +String groupId
        +String content
        +String encryptedContent
        +encrypt()
        +decrypt()
    }
    class Group {
        +String id
        +String name
        +List userIds
        +List taskIds
        +addTask()
        +removeTask()
    }
    User "1" --> "0..*" Task : creates
    User "0..*" --> "0..*" Group : belongs to
    Group "1" --> "0..*" Task : contains
```

## Diagram Przepływu

```mermaid
graph TD
U[Użytkownik] -->|Wprowadza zadanie| A(Aplikacja Frontend)
A -->|Wybiera grupę| B(Backend)
B -->|Szyfrowanie| C(Szyfrowany Task)
B -->|Przypisanie do grupy| G(Grupa)
C -->|Zapis| D(Chmura)
G -->|Powiadomienie członków| B
D -->|Pobieranie| B
B -->|Odszyfrowanie| A
A -->|Wyświetla zadania grupy| U
```

