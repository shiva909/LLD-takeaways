# 🎲 Snake & Ladder – Low Level Design (LLD)

This project explores the **Low-Level Design (LLD)** of the classic Snake & Ladder game.  
The focus is on **class responsibilities, trade-offs, and extensibility** while keeping the design modular and OOP-driven.

---

## 📌 Problem Statement

Design a **Snake & Ladder** game system where:
- Players roll dice and move across the board.
- Landing on a ladder moves the player up.
- Landing on a snake moves the player down.
- The first player to reach the final cell wins.

The system should be **modular, extensible, and designed using OOP principles**.

---

## 🎯 High-Level Requirements

- Support multiple players.  
- Support different board sizes (default 10x10, but configurable).  
- Allow adding snakes and ladders dynamically.  
- Dice rules should be flexible (e.g., multiple dice, custom rolls).  
- Game flow should be manageable for both local and future online modes.  

---

## 🏗️ Class Responsibilities (Why divided like that?)

- **Game** → Controls overall game flow and player turns.  
- **Board** → Manages cells and stores snakes/ladders.  
- **Cell** → Represents each square on the board.  
- **Jump (Snake/Ladder)** → Defines start and end of snakes/ladders.  
- **Player** → Tracks player details and current position.  
- **Dice** → Handles rolling logic (single/multiple/custom).  

👉 By splitting responsibilities, we:
- Keep code clean and modular.  
- Avoid tightly coupling logic in one class.  
- Make the design easier to extend for new rules.  

---

## 🧩 Design Patterns Considered

- **Strategy Pattern** → For flexible dice logic (single dice, multiple dice, custom rules).  
- **Factory Pattern** → Could be used for creating custom boards or jumps dynamically.  
- **Observer/Event-Driven** → Useful in online/multiplayer scenarios where events update all clients in real time.  

---

## 📊 UML Class Diagram

*(Attach your UML diagram here)*  

---

## 🔄 Key Flows

### Game Flow
1. Players join and are placed at starting position (cell 0).  
2. On each turn, a player rolls the dice.  
3. Player’s token moves forward by the dice value.  
4. If the player lands on:  
   - **Snake head** → Move down to the tail.  
   - **Ladder base** → Move up to the top.  
5. Check if the player reached the final cell → Declare winner.  
6. Continue turns until a player wins.  

---

## ⚖️ Trade-offs Considered

### 1. Array vs Map for Board Representation  
- **Array**: Simple, fast for fixed 10x10 boards.  
- **Map**: Flexible for irregular/custom boards.  

👉 Example: Custom board with only `{1, 2, 3, 7, 15, 22, 50, 100}` →  
- Using an **array** wastes memory.  
- Using a **map** stores only active cells.  

---

### 2. Single Dice vs Strategy Pattern  
- **Single Dice**: Works for the classic game.  
- **Strategy Pattern**: Easier to extend for custom rules.  

👉 Example:  
- **Fast-play mode** → Dice returns values between 2–12.  
- **Teaching mode** → Dice returns only even numbers.  

---

### 3. Centralized Game Flow vs Event-Driven Flow  
- **Centralized**: Easier for local, offline play.  
- **Event-Driven**: Better for multiplayer/online scaling.  

👉 Example:  
In an online mode, when **Player A** rolls, an event instantly updates **Player B’s UI**.  

---

## ⚡ Extensibility Points

- Add bonus rules (e.g., extra turn on rolling a 6, exact roll to win).  
- Support AI/bot players.  
- Extend to online multiplayer using event-driven design.  
- Allow different board themes or rules (e.g., Power-ups, Teleports).  

---

## 📚 Learnings & Takeaways

- Separating class responsibilities keeps the design **modular and testable**.  
- Thinking about future rules early helps avoid redesign.  
- Trade-offs like **Array vs Map** and **Centralized vs Event-Driven** are critical for scalability.  
- Even a simple game can reveal **core LLD principles** applicable in real-world systems.  

---

## 💡 Feedback

I’d love to hear how you would extend **Snake & Ladder** into an online multiplayer game 🚀  
Feel free to share your ideas or suggest improvements!  

## 🔗 Go Back
[⬅️ Back to LLD Takeaways](../../README.md)
