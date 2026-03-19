# ⚓ Dark Lands — Narrative RPG

A turn-based RPG set on the high seas, where you face marine creatures in strategic battles across three stages.

---

## 🎮 About the Game

You are a pirate hero who must confront the creatures of the deep to claim the treasure of the Lost Island. Each stage introduces a new scenario and a different enemy, with random events that can help or hinder your progress.

---

## 🗺️ Stages

| Stage | Scenario | Enemy |
|-------|----------|-------|
| 1 | Haunted Beach | Enchanting Mermaid |
| 2 | Submerged Grotto | Fish-Man |
| 3 | Kraken's Lair | Kraken |

Each scenario can trigger **random events** before combat:

- **Haunted Beach** → Crab Ambush (deals damage)
- **Submerged Grotto** → Rampant Fish Swarm (damage or healing)
- **Kraken's Lair** → Rising Water Level (damage and strength reduction)

---

## 🦸 Heroes

### Captain Hardhead
> Veteran pirate with powerful physical attacks

- **HP:** 330 | **Strength:** 6 | **Luck:** 25%
- **Captain's Strike** — physical blow with a random multiplier
- **One-Eyed Shot** *(critical)* — massive damage triggered by luck (Strength × 6)
- Builds rage with the Trident Attack

### Sedentary Corsair
> Tactician who studies enemies to deliver devastating blows

- **HP:** 120 | **Strength:** 2 | **Luck:** 30%
- **Analyze Enemy** — accumulates Study Points (1 or 2 per turn)
- **Master Strike** — activated with 3+ Study Points; deals +15 bonus damage per accumulated point

---

## 👾 Monsters

### Enchanting Mermaid
- HP: 75 | Strength: 7 | XP: 25
- **Tail Whip** — standard physical attack
- **Divine Song** *(30% chance)* — amplified magical damage
- Drops: **Cleaver**

### Fish-Man
- HP: 50 | Strength: 5 | XP: 40
- **Trident Attack** — physical attack that builds rage
- **Ammonia Blast** *(after 3 rage attacks)* — devastating special damage
- Drops: **Rusty Musket**

### Kraken
- HP: 130 | Strength: 10 | XP: 100
- **Tentacle Whip** — physical attack with 20% chance to grab
- **Drowning** *(when hero is grabbed)* — massive damage
- Drops: **Kraken's Pistol**

---

## ⚔️ Combat System

Combat is turn-based: the hero acts first, then the monster. The cycle continues until one of them dies.

**Special mechanics:**
- Each victory grants the hero **XP** and may trigger a **level up** (increasing max HP, strength, and luck)
- Weapons dropped by monsters can be **equipped** in the post-turn menu
- Equipping weapons requires a **minimum level**

---

## 🗡️ Weapons

| Weapon | Damage | Min Level |
|--------|--------|-----------|
| Cleaver | +10 | 1 |
| Rusty Musket | +14 | 2 |
| Kraken's Pistol | +22 | 3 |

---

## 🎚️ Difficulty Levels

| Difficulty | Monster Strength | XP Gained |
|------------|-----------------|-----------|
| Easy | ×0.75 | ×1.25 |
| Normal | ×1.0 | ×1.0 |
| Hard | ×1.5 | ×0.8 |

---

## 💾 Save System

The game allows you to **save and load** runs at any point from the post-turn menu. Saves are stored as XML files in the `saves/` folder using JAXB serialization.

---

## 🛠️ Technologies

- **Java 21**
- **Gradle** (build management)
- **JAXB** (XML serialization for saves)
- **JUnit 5** (automated testing)

---

## 🚀 How to Run

### Prerequisites
- Java 21+
- Gradle

### Running the game

```bash
./gradlew run
```

### Running tests

```bash
./gradlew test
```

---

## 📁 Project Structure

```
src/main/java/
├── app/              # Entry point and battle management
├── combate/          # Combat interfaces and actions
├── config/           # Difficulty enum
├── exceptions/       # Custom exceptions
├── fases/            # Stages, scenarios, and events
├── itens/armas/      # Available weapons
├── personagens/      # Base classes for heroes and monsters
│   ├── heroi/        # Playable hero classes
│   └── monstros/     # Enemy monster classes
└── util/             # Utilities (InputManager)
```

---

## 🏗️ Design Patterns Used

- **Strategy** — combat actions (`AcaoDeCombate`) are interchangeable
- **Template Method** — heroes and monsters inherit from `Personagem` with customizable behaviors
- **Builder** — `ConstrutorDeCenarioFixo` implements `GeradorDeFases`
- **Composition** — `Batalha` owns the hero (the hero does not exist outside a battle)
- **Aggregation** — monsters store weapon classes, not instances
