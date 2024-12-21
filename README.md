# Maximize Goodness Puzzle Solver

## Overview
This project implements a JavaScript algorithm to solve the "Maximize Goodness Puzzle" problem, where the goal is to maximize the goodness of a matrix by performing a sequence of clockwise rotations on sub-squares.

The solution successfully passed **all 20 test cases**, demonstrating its efficiency and correctness for handling large input sizes.

---

## Problem Statement
Given an **n x n** matrix where each cell contains a unique integer, the task is to maximize the "goodness" of the matrix by performing up to **500 moves**. A move consists of:
1. Selecting a **k x k** sub-square.
2. Rotating the selected sub-square **clockwise**.

### Goodness Definition
Goodness is defined based on "good pairs" of cells:
- Two cells in the **same row** where the left cell's value is less than the right cell's value.
- Two cells in the **same column** where the top cell's value is less than the bottom cell's value.

The algorithm attempts to maximize the number of such good pairs.

---

## Features
- Efficient calculation of goodness using **flat loops**.
- Optimized in-place **layer-wise rotation** for sub-squares to avoid excessive memory usage.
- Early exit strategy and a maximum move limit to prevent **timeout errors**.
- Supports matrices up to **22 x 22** as verified by test cases.

---

## Input Format
```
n
matrix[0][0] matrix[0][1] ... matrix[0][n-1]
...
matrix[n-1][0] matrix[n-1][1] ... matrix[n-1][n-1]
```
- **n**: Size of the matrix (1 ≤ n ≤ 30).
- Each matrix cell contains a **unique integer** (1 ≤ value ≤ n²).

### Sample Input
```
3
8 6 9
7 2 5
1 4 3
```

---

## Output Format
```
m
x1 y1 k1
x2 y2 k2
...
```
- **m**: Number of moves performed.
- Each move specifies the **top-left coordinates (x, y)** and size **k** of the rotated sub-square.

### Sample Output
```
3
1 1 2
2 2 2
1 1 3
```

---

## Algorithm Optimizations
1. **Efficient Goodness Calculation**:
   - Combined row and column checks to reduce redundant loops.
2. **In-Place Rotation**:
   - Implemented layer-wise rotation to minimize memory usage.
3. **Dynamic Sub-square Size**:
   - Limited maximum sub-square size to **6** to ensure faster processing.
4. **Early Exit Strategy**:
   - Used a **500-move limit** and avoided re-processing visited sub-squares.

---

## Performance
- Passed **all 20 test cases**, including edge cases with **22 x 22 matrices**.
- Handles **large inputs** efficiently by prioritizing moves with the highest improvement in goodness.

---

## Usage
1. **Prerequisites**:
   - Install [Node.js](https://nodejs.org/) if not already installed.
   - Install Visual Studio Code if not already installed.

2. **Setup the Project**:
   - Save the solver code as `goodness_puzzle_solver.js` in your project folder.
   - Open the folder in Visual Studio Code.

3. **Run the Program**:
   - Open a terminal in Visual Studio Code (Terminal > New Terminal).
   - Run the following command:
     ```bash
     node goodness_puzzle_solver.js < input.txt > output.txt
     ```
   - Replace `input.txt` with your test input file.
   - Output will be written to `output.txt`.

4. **Debugging in VSCode**:
   - Create a `launch.json` file under `.vscode/` folder.
   - Add the following configuration:
     ```json
     {
         "version": "0.2.0",
         "configurations": [
             {
                 "type": "node",
                 "request": "launch",
                 "name": "Run Goodness Puzzle Solver",
                 "program": "${workspaceFolder}/goodness_puzzle_solver.js",
                 "args": ["<", "input.txt", ">", "output.txt"]
             }
         ]
     }
     ```
   - Press `F5` to start debugging.

---

## Author
This project demonstrates advanced algorithmic optimization techniques and efficient JavaScript implementation for competitive programming challenges.

