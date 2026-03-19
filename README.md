# ⚓ Terras Sombrias — RPG Narrativo

Um jogo de RPG por turnos ambientado nos mares, onde você enfrenta criaturas marinhas em batalhas estratégicas ao longo de três fases.

---

## 🎮 Sobre o Jogo

Você é um herói pirata que deve enfrentar as criaturas das profundezas para conquistar o tesouro da Ilha Perdida. Cada fase apresenta um novo cenário e um inimigo diferente, com eventos aleatórios que podem te ajudar ou te prejudicar.

---

## 🗺️ Fases

| Fase | Cenário | Inimigo |
|------|---------|---------|
| 1 | Praia Assombrada | Sereia Encantadora |
| 2 | Gruta Submersa | Homem-Peixe |
| 3 | Covil do Kraken | Kraken |

Cada cenário pode disparar **eventos aleatórios** antes do combate:

- **Praia Assombrada** → Emboscada de Carangueijos (causa dano)
- **Gruta Submersa** → Cardume de Peixes Descontrolados (dano ou cura)
- **Covil do Kraken** → Elevação do Nível da Água (dano e redução de força)

---

## 🦸 Heróis

### Capitão Cabeçudo
> Pirata veterano com ataques físicos poderosos

- **HP:** 330 | **Força:** 6 | **Sorte:** 25%
- **Ataque do Capitão** — golpe físico com multiplicador aleatório
- **Tiro Caolho** *(crítico)* — dano massivo ativado pela sorte (Força × 6)
- Acumula raiva com o Ataque de Tridente

### Corsário Sedentário
> Estrategista que estuda inimigos para golpes devastadores

- **HP:** 120 | **Força:** 2 | **Sorte:** 30%
- **Analisar Inimigo** — acumula Pontos de Estudo (1 ou 2 por turno)
- **Golpe de Mestre** — ativado com 3+ Pontos de Estudo; bônus de +15 dano por ponto acumulado

---

## 👾 Monstros

### Sereia Encantadora
- HP: 75 | Força: 7 | XP: 25
- **Golpe de Cauda** — ataque físico padrão
- **Canto Divino** *(30% de chance)* — dano mágico amplificado
- Dropa: **Cutelo**

### Homem-Peixe
- HP: 50 | Força: 5 | XP: 40
- **Ataque de Tridente** — ataque físico que acumula raiva
- **Jato de Amônia** *(após 3 ataques de raiva)* — dano especial devastador
- Dropa: **Mosquete Enferrujado**

### Kraken
- HP: 130 | Força: 10 | XP: 100
- **Golpe de Tentáculo** — ataque físico com 20% de chance de agarrar
- **Afogamento** *(quando herói estiver agarrado)* — dano massivo
- Dropa: **Pistola do Kraken**

---

## ⚔️ Sistema de Combate

O combate é por turnos: herói age primeiro, depois o monstro. O ciclo continua até um dos dois morrer.

**Mecânicas especiais:**
- A cada vitória o herói ganha **XP** e pode **subir de nível** (aumentando HP máximo, força e sorte)
- Armas droppadas pelos monstros podem ser **equipadas** no menu pós-turno
- Equipar armas requer **nível mínimo**

---

## 🗡️ Armas

| Arma | Dano | Nível Mínimo |
|------|------|--------------|
| Cutelo | +10 | 1 |
| Mosquete Enferrujado | +14 | 2 |
| Pistola do Kraken | +22 | 3 |

---

## 🎚️ Dificuldades

| Dificuldade | Força dos Monstros | XP Ganho |
|-------------|-------------------|----------|
| Fácil | ×0.75 | ×1.25 |
| Normal | ×1.0 | ×1.0 |
| Difícil | ×1.5 | ×0.8 |

---

## 💾 Sistema de Saves

O jogo permite **salvar e carregar** partidas em qualquer momento do menu pós-turno. Os saves são armazenados em arquivos XML na pasta `saves/` usando serialização JAXB.

---

## 🛠️ Tecnologias

- **Java 21**
- **Gradle** (gerenciamento de build)
- **JAXB** (serialização XML para saves)
- **JUnit 5** (testes automatizados)

---

## 🚀 Como Executar

### Pré-requisitos
- Java 21+
- Gradle

### Rodando o jogo

```bash
./gradlew run
```

### Rodando os testes

```bash
./gradlew test
```

---

## 📁 Estrutura do Projeto

```
src/main/java/
├── app/              # Ponto de entrada e gerenciamento da batalha
├── combate/          # Interfaces e ações de combate
├── config/           # Enum de dificuldade
├── exceptions/       # Exceções customizadas
├── fases/            # Fases, cenários e eventos
├── itens/armas/      # Armas disponíveis no jogo
├── personagens/      # Base para heróis e monstros
│   ├── heroi/        # Classes dos heróis jogáveis
│   └── monstros/     # Classes dos monstros inimigos
└── util/             # Utilitários (InputManager)
```

---

## 🏗️ Design Patterns Utilizados

- **Strategy** — ações de combate (`AcaoDeCombate`) são intercambiáveis
- **Template Method** — herói e monstros herdam de `Personagem` com comportamentos customizáveis
- **Builder** — `ConstrutorDeCenarioFixo` implementa `GeradorDeFases`
- **Composição** — `Batalha` contém o herói (herói não existe fora de uma batalha)
- **Agregação** — monstros guardam classes de armas, não instâncias
