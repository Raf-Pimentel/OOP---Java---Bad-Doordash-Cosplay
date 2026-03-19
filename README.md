# 🎮 Dark Lands (Terras Sombrias)
> **Narrative RPG Engine built with Java 21**
> *Final Project for MC322 - Object-Oriented Programming (Unicamp)*

---

## 📖 Overview

**Dark Lands** is a text-based narrative RPG where players face mythical creatures in strategic turn-based combat. Developed as a university assignment, the project demonstrates core **Object-Oriented Programming (OOP)** principles, focusing on object lifecycles, data persistence, and clean architecture.

---

## 🛠️ Technical Highlights (Task 6)

This version (Task 6) specifically implements advanced architectural requirements regarding object relationships and data handling.

### 🧩 OOP Design: Composition vs. Aggregation
The project strictly follows architectural requirements to demonstrate different object relationships:

* **Composition (Strict Lifecycle):** The `Hero` (`Heroi`) is created and managed exclusively within the `Battle` (`Batalha`). If the battle ends or is destroyed, the hero instance follows the same lifecycle.
* **Aggregation (Weak Coupling):** The loot system was refactored. `Monster` (`Monstro`) now stores a list of weapon **classes** (`List<Class<? extends Arma>>`) instead of active instances. Weapons are only instantiated when "dropped," demonstrating memory efficiency and decoupling.

### 💾 Persistence System (JAXB)
Full game state management using **JAXB (Jakarta XML Binding)**:
* **Save/Load:** Players can save progress after combat sessions.
* **XML Serialization:** Converts the entire `Batalha` object tree into readable XML.
* **Polymorphism:** Handles complex class hierarchies (different types of monsters/heroes) using `@XmlSeeAlso`.

---

## 🚀 Getting Started

### Prerequisites
* **JDK 21**
* **Gradle 8.x** (Included wrapper)

### Installation & Execution
1. **Clone the repository:**
   ```bash
   git clone [https://github.com/your-username/dark-lands-rpg.git](https://github.com/your-username/dark-lands-rpg.git)
   cd dark-lands-rpg
