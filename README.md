# Snake — Terminal Edition

A classic Snake game that runs entirely in the terminal. Built in Python with no external libraries — just the standard library and clean separation across four modules.

---

## Demo

```
┌────────────────────────────────────────┐
│                                        │
│                  ●                     │
│                                        │
│          ◉ ■ ■ ■ ■                     │
│                                        │
│                                        │
└────────────────────────────────────────┘
  Score : 40   Best : 40   Level : Medium
  W A S D to move  |  Q to quit
```

**Menu screen:**
```
  ╔══════════════════════════════╗
  ║            SNAKE             ║
  ║       Terminal Edition       ║
  ╚══════════════════════════════╝

  Choose Difficulty:
    1 → Easy
    2 → Medium
    3 → Hard
```

---

## Features

- Three difficulty levels — Easy, Medium, Hard — with different move speeds
- Live score display and persistent high score across rounds
- Cross-platform keyboard input (Windows via `msvcrt`, Unix via `tty`/`termios`)
- Flicker-free rendering by building the full frame and printing it in one call
- Collision detection for walls and self-intersection
- Play again loop without restarting the program

---

## Project Structure

```
snake-terminal/
│
├── main.py       # Game loop — input, movement, collision, scoring
├── models.py     # Snake and Food classes
├── ui.py         # Rendering, keyboard input, menu and game over screens
└── settings.py   # Grid size, speeds, symbols, directions
```

---

## Getting Started

**Requirements:** Python 3.7+, no external libraries needed.

```bash
# Clone the repository
git clone https://github.com/your-username/snake-terminal.git
cd snake-terminal

# Run the game
python main.py
```

> **Windows users:** runs as-is.  
> **Linux/macOS users:** run in a proper terminal (not inside an IDE terminal) for best keyboard responsiveness.

---

## Controls

| Key | Action |
|---|---|
| `W` | Move Up |
| `S` | Move Down |
| `A` | Move Left |
| `D` | Move Right |
| `Q` | Quit game |

---

## Settings

All constants live in `settings.py` and can be tweaked without touching game logic:

| Setting | Default | Description |
|---|---|---|
| `WIDTH` | 20 | Grid columns |
| `HEIGHT` | 15 | Grid rows |
| `DELAY_EASY` | 0.25s | Seconds per move on Easy |
| `DELAY_MEDIUM` | 0.15s | Seconds per move on Medium |
| `DELAY_HARD` | 0.08s | Seconds per move on Hard |
| `SNAKE_HEAD` | `◉` | Head symbol |
| `SNAKE_BODY` | `■` | Body segment symbol |
| `FOOD` | `●` | Food symbol |

---

## Architecture

The game loop in `main.py` follows a straightforward cycle each tick:

1. **Input** — read a non-blocking keypress
2. **Direction** — update snake direction if valid (no 180° reversal)
3. **Move** — shift the snake one step forward
4. **Food** — check if head landed on food; if so, grow and respawn food
5. **Collision** — check wall and self-hit; break loop if true
6. **Draw** — render the full frame to terminal
7. **Wait** — sleep for the difficulty delay
