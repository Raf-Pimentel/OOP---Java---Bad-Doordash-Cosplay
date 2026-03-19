# 🎮 Dark Lands (Terras Sombrias)
> **Narrative RPG Engine built with Java 21**
> *Final Project for MC322 - Object-Oriented Programming (Unicamp)*

---

## 📖 Overview

**Dark Lands** is a text-based narrative RPG where players face mythical creatures in strategic turn-based combat. Developed as a university assignment, the project focuses on demonstrating mastery of **Object-Oriented Programming (OOP) design patterns**, specifically regarding object lifecycles, data persistence, and clean architecture.

---

## 🛠️ Key Technical Features (Task 6)

The project strictly follows architectural requirements to demonstrate different object relationships and persistence techniques.

### 🧩 Architecture: Composition vs. Aggregation
We implemented a clear distinction between how objects are owned and referenced:

* **Composition (Strict Lifecycle):** The `Hero` (`Heroi`) exists only within a `Battle` (`Batalha`). If the battle session is destroyed, the hero instance is also cleared.
* **Aggregation (Weak Coupling):** The `Monster` (`Monstro`) doesn't carry physical weapon instances. Instead, it stores a list of weapon **classes** (`List<Class<? extends Arma>>`). Items are only instantiated ("dropped") when a monster is defeated.

#### Relationship Diagram

```mermaid
classDiagram
    class Batalha {
        -Heroi heroi
        -List~Fase~ fases
        +iniciar()
        +salvarProgresso()
    }
    class Heroi {
        <<Composition>>
        -String nome
        -int nivel
    }
    class Monstro {
        <<Aggregation>>
        -List~Class~ lootTable
    }
    class Arma {
        <<Abstract>>
    }
    Batalha *-- Heroi : Owned_by
    Monstro o-- Arma : References_Classes
    
💾 Persistence System (JAXB)
The game features a robust Save/Load system using JAXB (Jakarta XML Binding):

Serialization: The entire state of the Batalha class is converted to XML.

Hierarchical Support: Handles polymorphic structures (different types of monsters and actions) using @XmlSeeAlso annotations.

Storage: Saves are managed by the GerenciadorDePersistencia and stored in the saves/ directory.

🚀 Getting Started
Prerequisites
JDK 21 or higher

Gradle 8.x (Wrapper included)

Installation & Execution
Clone the repository:

Bash
git clone [https://github.com/your-username/dark-lands-rpg.git](https://github.com/your-username/dark-lands-rpg.git)
cd dark-lands-rpg
Build the project:

Bash
./gradlew build
Run the game:

Bash
./gradlew run
Running Tests
We use JUnit 5 to ensure the stability of combat logic and persistence:

Bash
./gradlew test
📁 Project Structure
Plaintext
src/main/java/
├── app/          # Main entry, Battle coordination, and Persistence logic
├── combate/      # Combat engine, Combatant interfaces, and Actions
├── config/       # Difficulty and game settings
├── exceptions/   # Custom domain exceptions (e.g., LevelInsuficiente)
├── fases/        # Level generation, scenarios, and environment events
├── itens/        # Items and Weapon hierarchy
├── personagens/  # Hero and Monster specializations
└── util/         # Input handling and CLI helpers
👥 Authors
Rafael Rodrigues Pimentel de Melo

Matheus Boazão Silveira

University of Campinas (Unicamp) - 2025
