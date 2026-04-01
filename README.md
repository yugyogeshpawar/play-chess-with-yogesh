# Analytical Sanctuary - Chess Dashboard

A modern, fully-responsive chess dashboard and practice environment built with HTML, Tailwind CSS, and powered by JavaScript (using `chess.js` and `chessboard.js`).

## Overview

Analytical Sanctuary is designed as a high-fidelity mock application that gives players an advanced environment to track their tactical progression, solve puzzles, review their rankings, manage their profile, and directly play against a strategic computer engine. 

## Features

### 🤖 Play vs Bot Engine (`play_vs_bot.html`)
- **Interactive Chessboard**: Fully supports both "Click-to-Move" and "Drag-and-Drop". 
- **Valid Move Highlighting**: Clicking a piece highlights its valid destination squares (including captures) and safely prevents illegal moves if the King is in check.
- **Smart Bot Evaluation**: The built-in bot uses the Minimax algorithm with Alpha-Beta pruning, augmented by "Piece-Square Tables" to prioritize positional strategies like central control and knight development over purely random capture logic.
- **Game State Memory**: If you refresh or leave the page, your game (including the move log and the bot's difficulty setting) is restored seamlessly via browser `localStorage`.
- **Dynamic Move Log**: The interface logs every move using standard algebraic notation.
- **Live Match Data**: View the live material advantage (e.g. "+3") and a dynamically updating Engine Evaluation Bar showing who is currently favored.
- **Tools & Assits**: Features Undo, Redo, Restart, and a Hint functionality that suggests the next best move.

### 🧩 Puzzles & Practice (`practice.html`, `puzzles.html`, `mate_in_2.html`)
- Practice modules for varying depths (Mate in 1, Mate in 2, Mate in 3).
- Dedicated practice pages focused on tactical themes (e.g., Discovery Attacks, Deflections).
- Integrated puzzle boards providing interactive problem-solving interfaces.

### 🏆 Leaderboard (`leaderboard.html`)
- Global rankings page where players can view top grandmasters.
- Filters to view by Daily, Weekly, or All-Time.

### 👤 User Profile (`profile.html`)
- Profile overview displaying ELO rating, games played, win rate, and puzzle accuracy.
- Achievement badges displaying the player's milestones (e.g., Tactical Genius, First Win).

## Tech Stack
- **HTML5** structure.
- **Tailwind CSS** (via CDN) for rapid, modern, responsive styling.
- **jQuery** (via CDN) to interface smoothly with DOM manipulation needed by `chessboard.js`.
- **[chessboard.js](https://chessboardjs.com/)**: powers the visual rendering, dragging, and interactive logic of the chessboard.
- **[chess.js](https://github.com/jhlywa/chess.js/)**: a robust, headless chess engine running in JavaScript that calculates legal moves, check, checkmate, and game states.

## Setup & Running

This project is entirely front-end and runs directly in the browser. 

1. Ensure the files (`index.html`, `play_vs_bot.html`, etc.) are located in the same directory.
2. Open `index.html` in your favorite modern browser (Chrome, Firefox, Safari, Edge).
3. (Optional) Run using a local development server like `Live Server` in VS Code or `npx serve` to handle strict cross-origin policies.

## Project Structure
- `index.html`: The main entry point (Home Dashboard).
- `practice.html`: Main hub for tactical drills.
- `puzzles.html`: Daily puzzles overview and thematic tactics.
- `mate_in_2.html`: A specific puzzle problem interface.
- `play_vs_bot.html`: The full game interface against the AI engine.
- `leaderboard.html`: Displays player rankings.
- `profile.html`: The user's settings and statistical overview.
