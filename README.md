Copyright @lucabotez

# Bloxorz Solver

## Overview

**Bloxorz Solver** is a **Prolog-based** AI agent that finds solutions for the **Bloxorz puzzle game**, a logic-based game where a block must be navigated through a grid to reach a target hole without falling off. The solver utilizes **state-space search techniques**, including **depth-first search (DFS)**, to compute a valid sequence of moves.

## Features

- **Grid-based movement simulation** for the block (upright and laying positions).
- **Efficient state representation** and transition handling.
- **Collision detection** and valid move constraints.
- **Handling of special tiles** (fragile, switches, and goal locations).
- **Search-based pathfinding** using **DFS** to find optimal solutions.
- **Predefined levels and map parsing** for testing.

## Project Structure

- **`blox.pl`** – Core implementation of game state, movement, and solution search.
- **`files.pl`** – Loads external files and dependencies.
- **`levels.pl`** – Stores predefined game levels and grid configurations.
- **`util.pl`** – Utility predicates for movement, state visualization, and debugging.

## Implementation Details

### **1. State Representation (********`blox.pl`********)**

- The **game state** consists of:
  - A **grid** representing the level layout.
  - A **block position** (either upright or laying flat across two tiles).
- The solver tracks **legal moves**, **goal states**, and **tile properties** (e.g., normal, fragile, switches, goal tile).

### **2. Move Execution & Validity (********`blox.pl`********)**

- **Move Types:** `up (u)`, `down (d)`, `left (l)`, `right (r)`.
- Moves are validated based on:
  - **Block stability** (not falling into empty space).
  - **Fragile tile restrictions** (block cannot stand upright on these tiles).
  - **Switch activation mechanics** (opens/closes bridges dynamically).
- The solver computes **next valid states** and updates the game board accordingly.

### **3. Solving the Puzzle (********`blox.pl`********)**

- **Goal State:** The block is **upright on the goal tile (********`$`********)**.
- The solver applies **depth-first search (DFS)** to explore possible move sequences.
- Avoids **revisiting previously explored states** to optimize search efficiency.

### **4. Level Loading (********`levels.pl`********)**

- **Levels are defined as ASCII maps**, where:
  - `+` = Normal tile
  - `^` = Fragile tile
  - `$` = Goal tile
  - `B` = Block standing upright
  - `b` = Block laying down (part of it)
  - `o` / `x` = Switches controlling bridges
  - `-` = Active bridges
- Levels are parsed and loaded dynamically into the solver.

### **5. Utilities (********`util.pl`********)**

- Provides **movement calculations**, **neighbor detection**, and **debugging tools**.
- Implements `print_state/1` to visually display the **current grid** and block position.
- Defines **directional movement logic** for updating positions dynamically.

## Notes

- The solver **supports multiple levels**, each with unique tile constraints.
- Implements **search pruning** to improve solution performance.
- Bridges and switches introduce **dynamic gameplay mechanics** handled in Prolog.
