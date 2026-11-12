# Ping Pong Match (GBA)

An interactive, graphical Ping Pong game built from scratch in C for the Game Boy Advance (GBA) hardware. 

This project was developed as part of CS 2110 (Computer Organization and Programming). It demonstrates low-level hardware programming, memory-mapped I/O, Direct Memory Access (DMA), and working within the resource constraints of the ARM7 processor.

## Features

- **Custom Graphics:** Includes a full-screen title screen, an in-game background, and a custom sprite for the paddles/ball, all rendered using DMA.
- **Smooth Gameplay:** Implements 2D movement with collision detection between the ball and paddles/walls.
- **State Machine:** Cleanly transitions between the Title Screen, Gameplay, and Game Over/Win states. 
- **Dynamic UI:** Uses text rendering to display the current score during gameplay.
- **No Tearing:** Optimized drawing routines to ensure graphics update smoothly without visual distortion.

## Controls

Because the game runs on an emulator, the GBA buttons are mapped to your keyboard:

| GBA Button | Keyboard Key |
| :--- | :--- |
| **D-Pad** (Up/Down/Left/Right) | Arrow Keys |
| **Start** | Enter |
| **Select** (Resets to Title Screen) | Backspace |
| **A** | Z |
| **B** | X |

## Technical Architecture

The project is written in C and adheres strictly to the GBA coding guidelines:
- **`main.c`**: Contains the core state machine and main game loop.
- **`main.h`**: Holds structs, function prototypes, and `#define` macros.
- **`gba.c` / `gba.h`**: Implements hardware-level graphics functions, including `drawImageDMA` and `waitForVBlank`.
- **No Floating Point:** All math uses fixed-point/integer arithmetic to maximize performance on the GBA's ARM7 processor (which lacks an FPU).
- **Memory Management:** No dynamic allocation (`malloc`); uses static arrays and structs to store game state.

## How to Build and Run

This project requires **Docker** and **Java 11+** to run the custom GBA emulator environment.

### 1. Start the Docker Container
Run the provided script for your operating system in your terminal:

**macOS and Linux:**
```bash
./cs2110docker-gba.sh
