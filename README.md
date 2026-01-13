# Sokoban-Solver
# 📦 Sokoban AI Solver & Performance Demo

A Python-based interactive Sokoban game featuring a real-time comparison between human players and various Artificial Intelligence search algorithms.

![Project Status](https://img.shields.io/badge/status-active-brightgreen)
![Python Version](https://img.shields.io/badge/python-3.x-blue)
![Library](https://img.shields.io/badge/library-pygame-yellow)

## 🎮 Overview

This project is not just a game; it is an educational tool designed to visualize and benchmark how different pathfinding algorithms solve constraint satisfaction problems.

Users can play the classic puzzle game manually while simultaneously running an AI agent to solve the same board. The application tracks and compares performance metrics such as **execution time**, **steps taken**, and **nodes explored**.

## ✨ Features

* **Dual Play Mode:** Play manually using the keyboard while the AI solves the puzzle in a separate window section.
* **Multiple AI Algorithms:**
    * **A* (A-Star):** Optimized search using heuristics (Manhattan distance + Deadlock detection).
    * **BFS (Breadth-First Search):** Guarantees shortest path but uses more memory.
    * **DFS (Depth-First Search):** Fast exploration but produces non-optimal paths.
* **Adaptive Difficulty:** 3 difficulty tiers (Easy, Medium, Hard) with curated levels.
* **Visualizer:** Smooth animations for player and crate movements built with `pygame`.
* **Real-time Metrics:** Live display of move counts, push counts, and solving time.
* **Safety Fallbacks:** Includes a greedy fallback strategy to prevent the AI from crashing on extremely complex puzzles.

## 🛠️ Installation

### Prerequisites
* Python 3.8 or higher
* pip (Python package manager)

### Setup

1.  **Clone the repository**
    ```bash
    git clone [https://github.com/yourusername/sokoban-solver.git](https://github.com/yourusername/sokoban-solver.git)
    cd sokoban-solver
    ```

2.  **Install dependencies**
    The only external dependency is `pygame`.
    ```bash
    pip install pygame
    ```

3.  **Run the application**
    ```bash
    python main.py
    ```

## 🕹️ Controls

| Key / Button | Action |
| :--- | :--- |
| **Arrow Keys / WASD** | Move the Human Player |
| **"PLAY (YOU)"** | Start/Pause Human input |
| **"PLAY AI"** | Start/Pause AI Solver |
| **RESET** | Reset the current level |
| **EASY / MED / HARD** | Change Difficulty (Loads new map) |
| **A* / BFS / DFS** | Switch AI Algorithm |

## 🧠 Technical Details

### The AI Agent (`ai_agent.py`)
The core logic resides in the `AIController` class. It employs different search strategies based on user selection:

1.  **A* Search (Recommended):**
    * Uses a `PriorityQueue` to explore the most promising nodes first.
    * **Heuristic:** Sum of Manhattan distances from crates to nearest targets + penalties for corner deadlocks.
    * **Optimization:** Checks for "corner deadlocks" (crates pushed into corners without targets) and assigns a high penalty (500) to prune those branches.

2.  **BFS:**
    * Explores level by level. Guaranteed to find the solution with the minimum number of moves, though not necessarily the minimum number of pushes.

3.  **DFS:**
    * Uses Iterative Deepening to prevent infinite loops on deep branches. It finds solutions quickly but often results in "wandering" paths that are far from optimal.

### State Management
The game uses a hashed state representation `(player_pos, frozenset(crate_positions))` to efficiently track visited states and prevent cycles during the search process.

## 📂 Project Structure

```text
sokoban-solver/
├── main.py           # Entry point. Handles exception handling and startup.
├── frontend.py       # Pygame GUI, sprite animations, and event handling.
├── game_engine.py    # Core logic: rules, collision detection, and level parsing.
├── ai_agent.py       # AI implementation (A*, BFS, DFS, Heuristics).
└── README.md         # Documentation.
