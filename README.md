# Classic Ping Pong (Game Boy Advance)

An interactive, graphical Ping Pong game built from scratch in C for the Game Boy Advance (GBA) hardware. 

This project was developed as part of CS 2110 (Computer Organization and Programming) at Georgia Tech. It demonstrates low-level hardware programming, memory-mapped I/O, Direct Memory Access (DMA), and working within the strict resource constraints of the ARM7 processor.

## Features

- **Custom Graphics Pipeline:** Renders full-screen title, win, and lose screens alongside dynamic in-game sprites using DMA.
- **Object-Oriented C Design:** Utilizes `struct` definitions (in `main.h`) to manage the state, position, and velocity of the player, the ball, and the AI opponent.
- **Collision Detection:** Implements AABB (Axis-Aligned Bounding Box) collision detection to handle ball physics against the paddles and screen boundaries.
- **Dynamic AI:** The enemy paddle tracks the ball's Y-coordinate and moves dynamically to intercept it.
- **State Machine Architecture:** Cleanly transitions between `START`, `PLAY`, `WIN`, and `LOSE` states. The game can be reset to the title screen at any time using the Select button.
- **No Tearing:** Uses `waitForVBlank()` and efficient `undraw`/`draw` routines to ensure smooth 60 FPS rendering without visual distortion.

## Controls

Because the game runs on an emulator, the GBA buttons are mapped to your keyboard:

| GBA Button | Keyboard Key |
| :--- | :--- |
| **D-Pad** (Up/Down) | Arrow Keys |
| **Start** | Enter |
| **Select** (Resets to Title Screen) | Backspace |
| **A** | Z |
| **B** | X |

## Technical Architecture

The project strictly adheres to the GBA coding guidelines and operates without an operating system:

- **`main.c` & `main.h`**: Contains the core state machine, game loop, and struct definitions.
- **`gba.c` & `gba.h`**: Implements hardware-level graphics functions, including `drawImageDMA`, `drawRectDMA`, and `waitForVBlank`. 
- **No Floating Point:** The ARM7 processor lacks a Floating-Point Unit (FPU). All position, velocity, and timer math use integer arithmetic to prevent massive performance hits.
- **No `malloc()`:** All memory is statically allocated using arrays and structs to avoid dynamic memory allocation overhead.
- **DMA Optimization:** Drawing images and rectangles bypasses the CPU using DMA channels to copy memory directly to the video buffer (`0x6000000`).

## How to Build and Run

This project requires **Docker** and **Java 11+** to run the custom GBA emulator environment.

### 1. Start the Docker Container
Run the provided script for your operating system in your terminal:

**macOS and Linux:**
```bash
./cs2110docker-gba.sh
