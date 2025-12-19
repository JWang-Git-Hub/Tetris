# Tetris Reworked

#### Video Demo:  <https://youtu.be/-iheRQjksfg>

> **A revamped version of the classic game Tetris featuring explosive power-ups, leveling mechanics, and a mobile-friendly classic mode.**

## 📖 Overview

**Tetris Reworked** is a web-based implementation of the legendary tile-matching puzzle game, built entirely with vanilla HTML5, CSS3, and JavaScript. This repository contains two distinct versions of the game:

1.  **Power Tetris (Main Version):** A feature-rich "arcade" version with special bomb blocks, inventory-based power-ups, neon aesthetics, and a stats dashboard.
2.  **Classic Mobile (Lite Version):** A lightweight, touch-optimized version designed for mobile play with on-screen controls and a retro interface.

The project demonstrates advanced DOM manipulation, game loop logic without external game engines, and responsive design principles.

## Key Features

### Power Tetris (Desktop/Arcade Mode)

*Located in `index.html`*

This is the flagship version of the project, featuring a "Cyberpunk" aesthetic with gradient block designs and particle effects.

  * **Explosive Mechanics:**
      * **Bomb Blocks:** Rare red blocks that explode upon placement, clearing a 3x3 grid area. These count as 2 cleared lines and award bonus points.
      * **Strategic Inventory:** Collect power-ups by performing multi-line clears. You can store up to 3 Bombs and 5 Line Clears.
  * **Active Power-Ups:**
      * **Manual Line Clear:** Stuck with a mistake? Use a stored "Line Clear" to surgically remove the bottom-most completed line.
      * **Manual Bomb:** Deploy a bomb from your inventory to save yourself from a "Game Over" scenario.
  * **Progression System:**
      * **Dynamic Speed:** The game speed increases every 10 lines cleared.
      * **High Score Persistence:** Uses `localStorage` to save your personal best across sessions.
      * **Scoring Multipliers:** Rewards vary from 100 points (single line) to 800 points (Tetris/4 lines).

### Classic Mobile (Lite Mode)

*Located in `index2.html`*

A streamlined version optimized for touch devices and clean performance.

  * **Touch Controls:** Large, ergonomic on-screen buttons for Rotate, Down, Left, and Right.
  * **Gesture Support:** Supports long-press actions for movement on touch devices.
  * **Visual Preview:** Includes a clear "Next Piece" preview window.
  * **Responsive Layout:** Automatically centers and scales for different viewport sizes.

## Game Rules & Mechanics

### The "Power" System

Unlike standard Tetris, this game rewards aggressive play styles. The logic for spawning special blocks is probability-based:

1.  **Spawning Bombs:** There is a standard 2% chance for a Bomb Block to appear naturally. However, if your inventory is low (less than 3 bombs), the game drastically increases the spawn rate to **10%** to help you recover.
2.  **Earning Inventory:**
      * **Clear 2 Lines:** +1 "Line Clear" charge.
      * **Clear 3 Lines:** +1 "Bomb" charge.

### Scoring Table

| Action | Points | Effect |
| :--- | :--- | :--- |
| **1 Line** | 100 x Level | Basic clear |
| **2 Lines** | 300 x Level | +1 Line Clear Ammo |
| **3 Lines** | 500 x Level | +1 Bomb Ammo |
| **4 Lines** | 800 x Level | Max Points |
| **Bomb Explosion** | 500 | Clears 3x3 Area |

## Controls

### Desktop (Keyboard)

*Used primarily for `index.html`*

| Key | Action | Description |
| :--- | :--- | :--- |
| **← / →** | Move Left/Right | Slide the tetromino horizontally. |
| **↑** | Rotate | Rotate the piece 90 degrees clockwise. |
| **↓** | Soft Drop | Move the piece down faster. |
| **Space** | Hard Drop | Instantly drop the piece to the bottom. |
| **P** | Pause | Toggle Game Pause. |
| **R** | Reset | Restart the game immediately. |
| **Click UI** | Use Power-up | Click the icons in the sidebar to use items. |

### Mobile / Touch

*Used primarily for `index2.html`*

  * **↻ Button:** Rotate Piece.
  * **↓ Button:** Soft Drop.
  * **← / → Buttons:** Move Piece (Long press supported).
  * **Start Button:** Begin the game loop.

## Technical Implementation

This project is built using **Vanilla JavaScript** to ensure maximum performance and zero dependencies.

### Grid Rendering (DOM vs. Canvas)

Instead of using the HTML5 `<canvas>`, this project utilizes a **DOM-based Grid System**.

  * The board is generated as a CSS Grid (`display: grid`) with `div` elements representing individual cells.
  * This allows for easy styling via CSS classes (e.g., `.block-t`, `.block-bomb`) and CSS animations (like the `.clearing` flash effect) without complex canvas redraw logic.

### The Game Loop

The game uses a custom interval-based loop that adjusts dynamically based on difficulty:

```javascript
// Dynamic speed calculation based on level
const speed = Math.max(1000 - (level - 1) * 100, 100);
```

This ensures the game becomes progressively harder, capping at a 100ms update rate.

### Collision Detection

Collision is handled by "looking ahead." Before a piece moves or rotates, the `isValidMove` (or `checkCollision`) function verifies:

1.  **Boundaries:** Is the piece outside the 10x20 grid?
2.  **Stack:** Does the new coordinate overlap with an existing "locked" cell in the matrix?.

## Installation & Setup

Since this is a client-side web application, no build tools or package managers (npm/yarn) are required.

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/yourusername/tetris-reworked.git
    ```
2.  **Navigate to the folder:**
    ```bash
    cd tetris-reworked
    ```
3.  **Run the Game:**
      * Double-click `index.html` to play the **Power Edition**.
      * Double-click `index2.html` to play the **Mobile Edition**.

*Note: For the best experience, run this through a local server (like Live Server in VS Code) to ensure all assets load correctly, though it will work directly from the file system.*
