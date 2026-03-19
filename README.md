This is a Java project that I developed for my Object-Oriented Programming class at the University of Campinas (Unicamp).

🎮 Dark Lands (Terras Sombrias) - Narrative RPG
Task 6 - MC322 (Unicamp)
📋 About the Project
A narrative RPG developed in Java 21 featuring a complete system of:

✅ Persistence (Save/Load functionality using JAXB)

✅ Aggregation and Composition correctly implemented

✅ Battle System coordinated by the Batalha (Battle) class

✅ Loot System refactored using aggregation principles

🏗️ Architecture
Composition
Batalha → Heroi: The hero only exists within the context of a battle.

The Main class does not instantiate heroes directly.

Aggregation
Monstro → List<Class<? extends Arma>>: Monsters store weapon classes, not instances.

Weapons are instantiated only when they are dropped as loot.

🚀 How to Run
Compile
Bash
./gradlew clean build
Run
Bash
./gradlew run
Run Tests
Bash
./gradlew test
💾 Persistence System
Saving the Game
Post-combat menu → "Save Game" option.

Saves are stored in: saves/*.xml.

Loading the Game
Main menu → "Load Game" option (appears only if saves exist).

Select your desired save file.

Format
XML serialization using JAXB.

The entire Batalha class is saved (including the hero, stages, and progress).

📦 Dependencies
Gradle
dependencies {
    // JUnit for testing
    testImplementation 'org.junit.jupiter:junit-jupiter:5.10.2'
    
    // JAXB for persistence
    implementation 'jakarta.xml.bind:jakarta.xml.bind-api:4.0.0'
    implementation 'org.glassfish.jaxb:jaxb-runtime:4.0.2'
}
🎯 Implemented Features
Task 6
[x] Batalha class coordinating the game flow.

[x] GerenciadorDePersistencia (Persistence Manager) class with save/load logic.

[x] Loot system using aggregation.

[x] Composition: Hero scoped within Battle.

[x] JAXB annotations applied to all relevant classes.

Previous Tasks
[x] Combat system with interfaces.

[x] Difficulty system.

[x] Full interactive menu.

[x] Event system (Task 3).

[x] Custom exceptions.

[x] Unit tests.

📊 Package Structure
src/main/java/
├── app/
│   ├── Main.java
│   ├── Batalha.java
│   └── GerenciadorDePersistencia.java
├── combate/
│   ├── Combatente.java
│   ├── AcaoDeCombate.java
│   └── [action classes]
├── config/
│   └── Dificuldade.java
├── exceptions/
│   ├── NivelInsuficienteException.java
│   └── LootIndisponivelException.java
├── fases/
│   ├── Fase.java
│   ├── FaseDeCombate.java
│   ├── GeradorDeFases.java
│   ├── TipoCenario.java
│   └── [events]
├── itens/
│   ├── Item.java
│   └── armas/
│       ├── Arma.java
│       └── [concrete weapons]
├── personagens/
│   ├── Personagem.java
│   ├── Lootavel.java
│   ├── heroi/
│   │   ├── Heroi.java
│   │   ├── CapitaoCabecudo.java
│   │   └── CorsarioSedentario.java
│   └── monstros/
│       ├── Monstro.java
│       ├── Kraken.java
│       ├── HomemPeixe.java
│       └── SereiaEncantadora.java
└── util/
    └── InputManager.java
👥 Authorship
Course: MC322 - Object-Oriented Programming

Institution: Unicamp

Semester: 2025

Authors: Rafael Rodrigues Pimentel de Melo and Matheus Boazão Silveira

📝 Implementation Notes
Aggregation in the Loot System
Java
// BEFORE (Incorrect - Composition):
this.listaDeArmasParaLargar.add(new MosqueteEnferrujado());

// AFTER (Correct - Aggregation):
this.classesDeArmasParaLargar.add(MosqueteEnferrujado.class);
Composition in the Battle Class
Java
// Main DOES NOT create the hero directly
// Battle is responsible for the hero's lifecycle
public class Batalha {
    private Heroi heroi; // Composition
    // ...
}
JAXB - Key Points
All serializable classes require a default (no-arg) constructor.

Use @XmlTransient for fields that should not be persisted.

Use @XmlSeeAlso for class hierarchies.

Combat actions are recreated after deserialization.

🐛 Troubleshooting
Error: "No suitable constructor found"
Solution: Ensure a public default constructor exists for the class.

Error: "ClassCastException"
Solution: Check for missing @XmlSeeAlso annotations in base classes.

Saves not appearing in the menu
Verify if the saves/ folder was created.

Check write permissions for the application folder.

📚 References
JAXB Documentation

Gradle User Guide

JUnit 5 Documentation

Last Update: Task 6 - Persistence and Aggregation System
