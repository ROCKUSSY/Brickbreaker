
# Brick Breaker (Fast Mode)

---

## 🔷 Introduction

Brick Breaker (Fast Mode) is a fast-paced arcade game implemented in C++ using **OpenGL** and **GLUT** libraries. The player uses a paddle to bounce a ball and break all bricks on the screen. It includes colorful visuals, custom settings, and increasing challenge levels.

---

## 🧠 Project Objective

To create a functional, dynamic, and customizable brick-breaking game with:

- Real-time rendering using OpenGL
- Collision detection and response
- Customizable game settings (colors, sizes, difficulty)
- Smooth gameplay loop

---

## 💻 Technologies Used

- **C++**
- **OpenGL (GLUT)**
- **GLUT Keyboard, Mouse, and Timer Functions**

---

## 🕹️ Gameplay Controls

| Action | Key |
|--------|-----|
| Move Paddle Left | `A` / `←` Arrow |
| Move Paddle Right | `D` / `→` Arrow |
| Start/Restart Game | `S` |
| Quit Game | `Q` |
| Open Options Menu | Right Click |

---

## 📑 Game Flow

- **STATE_MENU (0):** Default startup screen
- **STATE_PLAYING (1):** Active gameplay
- **STATE_GAME_OVER (2):** When all lives are lost
- **STATE_WIN (3):** When all bricks are broken

---

## 🧩 Main Functional Components

### 🔹 `init_game()`
Initializes bricks, score, lives, and resets the ball. Called at the start and after restart.

### 🔹 `reset_ball()`
Resets ball and paddle to the center. Used at game start or after losing a life.

### 🔹 `draw_paddle()`, `draw_ball()`, `draw_bricks()`
Render the paddle, ball, and brick grid. Uses `glBegin()` and OpenGL lighting/material functions.

### 🔹 `check_collisions()`
Core physics logic. Handles ball collisions with walls, paddle, and bricks.

### 🔹 `update(int value)`
Called every ~16ms (60 FPS). Moves the ball based on current direction and speed.

### 🔹 `keyboard()` and `special_keys()`
Handle player input from standard keys and arrow keys.

### 🔹 `add_menu()`
Creates a right-click menu for customization of game elements.

### 🔹 `display()`
Main rendering logic based on current game state.

### 🔹 `main()`
Sets up OpenGL context and starts GLUT main loop.

---

## 🎨 Customization Options

Accessible via right-click:

- Brick, Ball, Paddle, Text Color
- Difficulty: Easy / Medium / Hard
- Paddle Size: Small / Medium / Large
- Game Speed: Normal / Fast / Very Fast

---

## 🧠 Game Logic & Concepts

### Paddle Collision Logic
Direction of the ball after paddle collision is calculated based on hit location.

### Brick Hit Detection
Each brick has a bounding box. Collision disables the brick, updates score, and checks for game win.

---

## 🧪 Testing Strategy

- Manual testing across difficulties and speeds
- Verifying collision behavior and game transitions

---

## ❓ Frequently Asked Questions

### Q1: How do I start/restart the game?
**A:** Press `S` from the menu, win screen, or game over screen.

### Q2: What’s the difference between difficulty and game speed?
**A:** Difficulty changes ball speed logic, while game speed alters movement multiplier.

### Q3: How does collision detection work?
**A:** Ball checks bounding areas for bricks, paddle, and walls to reverse direction or trigger state changes.

### Q4: What are the graphics features used?
**A:** Lighting, materials, and shading via OpenGL functions.

### Q5: Can I use the mouse to control the paddle?
**A:** Yes, horizontal movement adjusts paddle's position live.

### Q6: How does the game determine a win or loss?
**A:** All bricks cleared = win. All lives lost = game over.

### Q7: Is this game extensible?
**A:** Yes! Add more levels, effects, and even new mechanics.

---

## 📌 Final Thoughts

This project is a solid foundation for learning OpenGL and game design, and it’s fun to expand with creative ideas.
