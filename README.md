This is a Java project that I developed in my Object-Oriented Programming Class in my University.

# 🎮 Terras Sombrias - RPG Narrativo
## Tarefa 6 - MC322 (Unicamp)

---

## 📋 Sobre o Projeto

RPG narrativo desenvolvido em Java 21 com sistema completo de:
- ✅ **Persistência** (Save/Load com JAXB)
- ✅ **Agregação e Composição** corretamente implementados
- ✅ **Sistema de Batalha** coordenado pela classe Batalha
- ✅ **Sistema de Loot** refatorado com agregação

---

## 🏗️ Arquitetura

### **Composição**
- `Batalha` → `Heroi`: O herói só existe dentro de uma batalha
- A classe `Main` não instancia heróis diretamente

### **Agregação**
- `Monstro` → `List<Class<? extends Arma>>`: Monstros guardam **classes** de armas, não instâncias
- As armas são instanciadas apenas quando dropadas

---

## 🚀 Como Executar

### **Compilar**
```bash
./gradlew clean build
```

### **Executar**
```bash
./gradlew run
```

### **Executar Testes**
```bash
./gradlew test
```

---

## 💾 Sistema de Persistência

### **Salvar Jogo**
- Menu pós-combate → Opção "Salvar jogo"
- Saves armazenados em: `saves/*.xml`

### **Carregar Jogo**
- Menu principal → Opção "Carregar Jogo" (aparece se houver saves)
- Selecione o save desejado

### **Formato**
- Serialização em XML usando **JAXB**
- Toda a classe `Batalha` é salva (herói, fases, progresso)

---

## 📦 Dependências

```gradle
dependencies {
    // JUnit para testes
    testImplementation 'org.junit.jupiter:junit-jupiter:5.10.2'
    
    // JAXB para persistência
    implementation 'jakarta.xml.bind:jakarta.xml.bind-api:4.0.0'
    implementation 'org.glassfish.jaxb:jaxb-runtime:4.0.2'
}
```

---

## 🎯 Funcionalidades Implementadas

### **Tarefa 6**
- [x] Classe `Batalha` coordenando o jogo
- [x] Classe `GerenciadorDePersistencia` com save/load
- [x] Sistema de loot com agregação
- [x] Composição: herói dentro de Batalha
- [x] Anotações JAXB em todas as classes relevantes

### **Tarefas Anteriores**
- [x] Sistema de combate com interfaces
- [x] Sistema de dificuldade
- [x] Menu interativo completo
- [x] Sistema de eventos (Tarefa 3)
- [x] Exceções customizadas
- [x] Testes unitários

---

## 📊 Estrutura de Pacotes

```
src/main/java/
├── app/
│   ├── Main.java
│   ├── Batalha.java
│   └── GerenciadorDePersistencia.java
├── combate/
│   ├── Combatente.java
│   ├── AcaoDeCombate.java
│   └── [classes de ação]
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
│   └── [eventos]
├── itens/
│   ├── Item.java
│   └── armas/
│       ├── Arma.java
│       └── [armas concretas]
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
```

---

## 👥 Autoria

- **Disciplina**: MC322 - Programação Orientada a Objetos
- **Instituição**: Unicamp
- **Semestre**: 2025
- **Autores**: Rafael Rodrigues Pimentel de Melo e Matheus Boazão Silveira

---

## 📝 Notas de Implementação

### **Agregação no Sistema de Loot**
```java
// ANTES (errado - Composição):
this.listaDeArmasParaLargar.add(new MosqueteEnferrujado());

// DEPOIS (correto - Agregação):
this.classesDeArmasParaLargar.add(MosqueteEnferrujado.class);
```

### **Composição na Classe Batalha**
```java
// Main NÃO cria o herói diretamente
// A Batalha é responsável pela existência do herói
public class Batalha {
    private Heroi heroi; // Composição
    // ...
}
```

### **JAXB - Pontos Importantes**
- Todas as classes serializáveis precisam de construtor padrão
- Usar `@XmlTransient` para campos que não devem ser salvos
- Usar `@XmlSeeAlso` para hierarquias de classes
- Ações de combate são recriadas após deserialização

---

## 🐛 Troubleshooting

### **Erro: "No suitable constructor found"**
- Solução: Adicionar construtor padrão sem parâmetros

### **Erro: "ClassCastException"**
- Solução: Adicionar `@XmlSeeAlso` nas classes base

### **Saves não aparecem no menu**
- Verificar se a pasta `saves/` foi criada
- Verificar permissões de escrita

---

## 📚 Referências

- [JAXB Documentation](https://jakarta.ee/specifications/xml-binding/)
- [Gradle User Guide](https://docs.gradle.org/)
- [JUnit 5 Documentation](https://junit.org/junit5/docs/current/user-guide/)

---

**Última atualização**: Tarefa 6 - Sistema de Persistência e Agregação
