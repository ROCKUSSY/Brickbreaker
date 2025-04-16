
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
Initializes the game state:
- Sets up the grid of bricks with positions and active status
- Resets score and lives
- Adjusts game speed based on difficulty level
- Calls `reset_ball()` to center the paddle and ball

### 🔹 `reset_ball()`
Centers the paddle and places the ball just above it with an initial velocity:
```cpp
bx = 0;
by = -12.8;
dirx = 0.7f;
diry = 0.7f;
px = 0;
```
This ensures predictable start for each round.

### 🔹 `draw_paddle()`, `draw_ball()`, `draw_bricks()`
These rendering functions use OpenGL primitives:
- `draw_paddle()` draws a rectangle based on `paddle_size`
- `draw_ball()` uses `glutSolidSphere()` and lighting for 3D look
- `draw_bricks()` iterates over active bricks and draws each one

### 🔹 `check_collisions()`
The heart of the physics engine:
- Detects and responds to wall, paddle, and brick collisions
- Adjusts `dirx`, `diry` to simulate bounce
- On paddle hit: uses relative hit position to vary angle
- On brick hit: disables brick, increases score, checks win condition

### 🔹 `update(int value)`
Moves the ball based on its direction and speed multiplier. Called repeatedly using `glutTimerFunc()` for smooth animation:
```cpp
bx += dirx * speed_multiplier / game_speed;
by += diry * speed_multiplier / game_speed;
```

Also reduces `game_speed` gradually to simulate acceleration over time.

### 🔹 `keyboard()` and `special_keys()`
Handles player input:
- `A/D` and Arrow Keys to move paddle
- `Q` to quit
- `S` to start or restart

Includes boundary clamping to keep paddle within visible area.

### 🔹 `add_menu()`
Builds a context menu (on right-click) using GLUT's `glutCreateMenu()`:
- Submenus for colors, paddle size, speed, and difficulty
- Each choice sets a global variable used in rendering or logic

### 🔹 `display()`
This is the main draw loop:
- Clears the screen
- Draws the current game state (menu, playing screen, game over, win)
- Uses `glTranslatef()` to simulate camera movement and position the game

### 🔹 `main()`
Sets up the OpenGL environment:
- Initializes GLUT window
- Registers callback functions for rendering, input, and timer
- Starts main event loop with `glutMainLoop()`

---

## 🎨 Customization Options

Accessed via **Right-Click Menu**:
- Brick, Ball, Paddle, and Text color
- Paddle size: Small / Medium / Large
- Game speed: Normal / Fast / Very Fast
- Difficulty: Easy / Medium / Hard

Each option changes real-time appearance and behavior using global state variables.

---

## 🧠 Game Logic & Concepts

### Paddle Collision Logic

```cpp
float hit_pos = (bx - px) / paddle_size;
dirx = hit_pos * 2.5f;
```

This creates a skill-based deflection system where hitting the edge of the paddle sends the ball at sharper angles.

---

### Brick Hit Detection

Each brick is checked with bounding box collision:

```cpp
if (bx >= brick_left && bx <= brick_right &&
    by >= brick_bottom && by <= brick_top)
```

- On collision, direction is reversed
- Brick is marked inactive
- Score increments
- Checks if all bricks are gone → triggers win

---

## 🧪 Testing Strategy

- Manual testing of all paddle sizes, speeds, and colors
- Verified all collision zones
- Ensured score updates correctly
- Restart mechanics tested across all states
- Tried rapid key inputs and mouse control

---

## ❓ Frequently Asked Questions (FAQ)

### Q1: **How do I start or restart the game?**

**A:** Press `S` to start from the menu. After losing or winning, pressing `S` restarts with full lives, new bricks, and a score of 0.

---

### Q2: **How is the difficulty managed in the game?**

**A:** Difficulty affects the `game_speed`, where lower values mean faster ball movement. This is set through the right-click menu and impacts how much time the player has to react.

---

### Q3: **What happens when the ball touches different parts of the screen?**

**A:** 
- Left/Right wall: ball bounces horizontally
- Top wall: vertical bounce
- Paddle: directional change based on hit location
- Bottom: life lost or game over if no lives remain

---

### Q4: **What does the context menu do?**

**A:** Right-clicking opens a GLUT menu that allows you to change visual settings (colors), paddle size, difficulty level, and ball speed—real-time without restarting.

---

### Q5: **Can I use both keyboard and mouse to control the paddle?**

**A:** Yes. You can use `A/D` or `←/→` keys. Alternatively, you can use your mouse (horizontal movement) for fluid control during gameplay.

---

### Q6: **How does paddle size affect gameplay?**

**A:** A larger paddle makes hitting the ball easier but lowers the challenge. Smaller paddles demand better timing and control, especially at higher speeds.

---

### Q7: **How does the game determine when you’ve won?**

**A:** The game checks whether all bricks in the 2D array are marked inactive. If so, it switches to the `STATE_WIN` screen and shows your final score.

---

### Q8: **What makes this version “Fast Mode”?**

**A:** The ball starts at a higher speed than traditional games and accelerates slightly every frame. You can also set higher speed multipliers from the right-click menu.

---

### Q9: **Are lighting and shadows important for gameplay?**

**A:** Not mechanically, but they make the visuals more dynamic. OpenGL lights add shading, highlights, and a 3D look to the ball and paddle, enhancing realism.

---

### Q10: **Is the game scalable or extendable?**

**A:** Yes. The modular code design makes it easy to add:
- New brick types (e.g., unbreakable)
- Power-ups (multi-ball, paddle extension)
- Sound effects
- Level progression
- High score tracking

---

## 📌 Final Thoughts

This project is both a fun arcade game and a solid OpenGL learning platform. It combines essential game development skills—rendering, physics, input handling, and user customization—in a clean, understandable codebase.

Great for beginners or as a foundation for more advanced features!


---

## 🧱 Key Data Structures Explained

### 🧮 1. `brick_coords` Struct

```cpp
struct brick_coords {
    GLfloat x;
    GLfloat y;
    int active;
};
```

- Stores the position (`x`, `y`) of a brick and whether it's **active (1)** or **destroyed (0)**.
- Used in a 2D array: `brick_array[50][50]` to simulate a grid layout.
- Each brick is checked in `draw_bricks()` and `check_collisions()`.

---

### 🪄 2. Game State Variables

```cpp
int game_state, score, lives;
```

- `game_state` controls what is rendered (menu, game, win, loss).
- `score` is incremented when bricks are destroyed.
- `lives` decrement when the ball falls below the paddle.

---

### 🎯 3. Ball and Paddle Positions

```cpp
GLfloat px, bx, by;
GLfloat dirx, diry;
```

- `px`: Paddle's X-position
- `bx`, `by`: Ball’s current position
- `dirx`, `diry`: Ball’s current direction vector (normalized)

Used across `draw_ball()`, `update()`, and `check_collisions()` to simulate motion and interactions.

---

## 🧭 Visual Flow Diagram (Conceptual)

```text
        +-------------------------+
        |      STATE_MENU         |
        |  [Press S to Start]     |
        +-----------+-------------+
                    |
                    v
        +-------------------------+
        |     STATE_PLAYING       |
        |  Paddle, Ball, Bricks   |
        |   ↓       ↑             |
        | Lose   Destroy All      |
        +----+--------+-----------+
             |        |
             v        v
     +---------------+ +----------------+
     | STATE_GAME_OVER| |  STATE_WIN     |
     |[Press S to Retry]|[Press S to Play Again]
     +----------------+ +----------------+
```

This is how the game transitions between states based on gameplay events like loss of life or destroying all bricks.

---

## 🔧 OpenGL Setup Walkthrough

### Step-by-Step Breakdown from `main()`

1. **Initialize GLUT and Window**
```cpp
glutInit(&argc, argv);
glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH | GLUT_RGB);
glutInitWindowSize(900, 900);
```

2. **Create Window**
```cpp
glutCreateWindow("Brick Breaker (Fast Mode)");
```

3. **Register Callback Functions**
```cpp
glutDisplayFunc(display);      // Render loop
glutReshapeFunc(reshape);      // Window resize
glutKeyboardFunc(keyboard);   // Key press
glutSpecialFunc(special_keys); // Arrow keys
glutPassiveMotionFunc(mouse_motion); // Mouse movement
glutTimerFunc(0, update, 0);   // Animation loop
```

4. **Initialize Rendering Parameters**
```cpp
init_gl();  // Enables lighting, depth, materials
add_menu(); // Builds right-click context menu
```

5. **Start Main Loop**
```cpp
glutMainLoop();
```

### Rendering Features

- `glEnable(GL_LIGHTING)`: Enables scene lighting
- `glLightfv(...)`: Sets properties like diffuse/specular light
- `glMaterialfv(...)`: Sets object-specific material effects
- `glutSolidSphere()`: 3D sphere for ball

These simulate real lighting and shadow interactions to give the game a polished 3D appearance.

---

## 📷 Recommended Enhancements

To visualize the game better in the README:

- Add **screenshots** of:
  - Menu Screen
  - In-Game (bricks + paddle + ball)
  - Game Over / Win screen

Example Markdown (once images are available):

```markdown
### 📸 In-Game Screenshot
![Gameplay](images/brickbreaker_gameplay.png)

### 🏆 Victory Screen
![You Win](images/brickbreaker_win.png)
```

Let me know if you'd like help generating sample screenshots or creating ASCII art diagrams of gameplay layout.

