# Analytical Sanctuary - Tech Stack & Architecture

This document outlines the technical decisions, libraries, and frameworks used to construct the Analytical Sanctuary chess dashboard.

---

## 1. Core Front-End Technologies

### HTML5
The application uses semantic HTML5 markup, ensuring proper accessibility, structuring, and a base for rich graphical styling without heavy framework overhead.
- Features `data-icon` and structured ARIA attributes for screen readers where applicable.
- Employs `viewport` meta tags for robust mobile responsiveness.

### Tailwind CSS (via CDN)
The primary CSS framework. Tailwind is used extensively for rapid prototyping, offering utility-first CSS classes directly in the markup.
- **Custom Configuration**: The `tailwind-config` script in the `<head>` sets up an advanced custom color palette (`surface-container-low`, `primary-fixed`, etc.) inspired by Material Design 3 (M3).
- **Responsive Design**: Utilizing Tailwind's grid system (`grid-cols-1 md:grid-cols-12`) and flexible layout (`flex-col lg:flex-row`) to ensure the dashboard looks impeccable on both mobile and large-screen desktops.
- **Glassmorphism**: Combines arbitrary values in Tailwind (`bg-[rgba(...)]`) with `backdrop-blur` for sleek UI overlays.

---

## 2. JavaScript Libraries & Logic

The intelligence and interactive aspects of the application (specifically on the `play_vs_bot.html` page) are driven by a collection of robust JS libraries.

### [chess.js](https://github.com/jhlywa/chess.js/) (v0.10.3)
A headless, pure JavaScript chess engine used for move validation, game state tracking, and Forsyth-Edwards Notation (FEN) / Portable Game Notation (PGN) generation.
- **Responsibilities**:
  - Determining legal moves for a given position.
  - Detecting `Check`, `Checkmate`, `Draw`, and `Stalemate`.
  - Managing move history allowing for Undo/Redo tracking.

### [chessboard.js](https://chessboardjs.com/) (v1.0.0)
A UI library specifically designed to render chessboards and handle piece interactions via the DOM.
- **Responsibilities**:
  - Drawing the 64 squares and SVG pieces.
  - Processing "drag and drop" interactions.
  - Bound to `$(window).resize()` to maintain responsive aspect ratios dynamically.
  - Sourced directly from `unpkg.com` CDN to ensure assets (piece images) resolve perfectly without local hosting configurations.

### [jQuery](https://jquery.com/) (v3.5.1)
Utilized primarily because `chessboard.js` has a hard dependency on it for DOM manipulation, element selecting (`$('#board')`), and event listening.

---

## 3. Artificial Intelligence (The Bot)

The bot logic written inside the application is a custom implementation designed to mimic varying levels of human capability.

### Minimax Algorithm with Alpha-Beta Pruning
The bot computes its moves by constructing a game tree looking $N$ moves ahead (where $N$ is controlled by the "Difficulty" selector). 
- **Alpha-Beta Pruning**: Vastly decreases the number of nodes evaluated in the search tree, speeding up the bot's response time on the main thread.

### Positional Evaluation (Piece-Square Tables)
To ensure the bot does not just mindlessly grab pieces, an evaluation function applies **Piece-Square Tables**.
- **Material Evaluation**: Gives classic point values to pieces (`p: 100`, `n: 320`, `b: 330`, etc.).
- **Positional Evaluation**: Gives a positive or negative score to a piece depending on the square it occupies (e.g., Knights are heavily penalized on the edge of the board, Pawns are rewarded for moving toward the center).

---

## 4. State Management

To allow for a seamless user experience, the application utilizes standard Web APIs rather than complex state managers (like Redux or Zustand).

### `localStorage`
- **Persistence**: The game state (the current FEN, the PGN string, and the user's selected Bot Difficulty Depth) is saved to the browser's local storage upon every move.
- **Resumption**: When the page is loaded, the application checks `localStorage` and automatically updates the `chess.js` and `chessboard.js` objects to resume exactly where the user left off.

---

## 5. UI/UX Features & Assets

- **Google Fonts**: Uses `Space Grotesk` for sharp, high-tech headlines and `Manrope` for legible, clean body text.
- **Google Material Symbols**: Instead of SVG sprites, the application uses Google's latest Material Symbols Outlined font library for sleek, scalable, and customizable UI icons (such as the Undo, Redo, Hint, and Checkmate icons).
- **Dynamic Highlights**: Custom CSS classes dynamically injected via jQuery create glowing visual borders for valid moves (small dots), captured pieces (rings), and Check warnings (radial red gradients).
