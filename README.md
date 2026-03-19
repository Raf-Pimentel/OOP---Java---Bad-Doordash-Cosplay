🎮 Dark Lands (Terras Sombrias)
A Narrative RPG Engine built with Java 21 > Final Project for MC322 - Object-Oriented Programming (Unicamp)

📖 Overview
Dark Lands is a text-based narrative RPG where players face mythical creatures in strategic turn-based combat. Developed as a university assignment, the project focuses on demonstrating mastery of Object-Oriented Programming (OOP) design patterns, specifically regarding object lifecycles, data persistence, and clean architecture.

🛠️ Key Technical Features
🧩 OOP Design: Composition vs. Aggregation
The project strictly follows architectural requirements to demonstrate different object relationships:

Composition (Strict Lifecycle): The Hero is composed within the Battle (Batalha). A Hero does not exist independently of a game session; if the Battle is destroyed, the Hero is too.

Aggregation (Weak Coupling): The Monster (Monstro) uses aggregation for its loot. It stores a list of weapon classes (List<Class<? extends Arma>>) rather than active instances. This ensures that items are only created when "dropped," optimizing memory and decoupling state.

💾 Persistence System (JAXB)
The game features a robust Save/Load system using JAXB (Jakarta XML Binding).

The entire state of the Batalha class is serialized into XML.

Saves are automatically handled in the saves/ directory.

Complex Hierarchy: Handles polymorphic classes (Heroes/Monsters) using @XmlSeeAlso annotations.

⚔️ Combat & Loot Mechanics
Dynamic Events: Random encounters and scenario-based modifiers (e.g., rising water levels affecting stats).

Polymorphic Actions: Combat moves are implemented as distinct classes, allowing for easy expansion of the move pool.

🚀 Getting Started
Prerequisites
JDK 21 or higher

Gradle (Wrapper included)

Installation & Execution
Clone the repository:

Bash
git clone https://github.com/your-user/dark-lands-rpg.git
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
├── app/          # Game loop, Main entry point, and Persistence Logic
├── combate/      # Combat engine and Action interfaces
├── config/       # Difficulty and game settings
├── exceptions/   # Custom domain exceptions (e.g., LevelInsuficiente)
├── fases/        # Level generation and environmental events
├── itens/        # Weapons and inventory system
├── personagens/  # Hero and Monster hierarchies
└── util/         # Input handling and CLI helpers
📝 Implementation Insights
Aggregation Refactoring
To meet the "Task 6" requirements, the loot system was refactored. Instead of a monster "carrying" a physical object (Composition), it now "knows" what it can drop (Aggregation):

Java
// Modern Aggregation Approach
this.lootTable.add(RustyMusket.class); 
// Item is only instantiated upon monster's defeat
Persistence Logic
The PersistenceManager ensures that even after a crash, your hero's progress (XP, Items, Stages) is safely stored in saves/session.xml.

👥 Authors
Rafael Rodrigues Pimentel de Melo

Matheus Boazão Silveira

University of Campinas (Unicamp) - 2025
