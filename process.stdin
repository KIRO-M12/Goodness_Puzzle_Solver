const fs = require('fs');

function processData(input) {
    const lines = input.split('\n');
    const k = parseInt(lines[0], 10); // Grid size
    const initialState = [];

    // Reading the grid
    for (let i = 1; i <= k * k; i++) {
        initialState.push(parseInt(lines[i], 10));
    }

    const goalState = [];
    for (let i = 0; i < k * k; i++) {
        goalState.push(i);
    }

    // Function to calculate Manhattan distance heuristic
    function calculateHeuristic(state) {
        let distance = 0;
        for (let i = 0; i < state.length; i++) {
            if (state[i] !== 0) {
                const targetRow = Math.floor(state[i] / k);
                const targetCol = state[i] % k;
                const currentRow = Math.floor(i / k);
                const currentCol = i % k;
                distance += Math.abs(targetRow - currentRow) + Math.abs(targetCol - currentCol);
            }
        }
        return distance;
    }

    // Generate possible moves
    function generateMoves(state) {
        const moves = [];
        const zeroIndex = state.indexOf(0);
        const zeroRow = Math.floor(zeroIndex / k);
        const zeroCol = zeroIndex % k;

        const directions = [
            { row: -1, col: 0, move: 'UP' },
            { row: 1, col: 0, move: 'DOWN' },
            { row: 0, col: -1, move: 'LEFT' },
            { row: 0, col: 1, move: 'RIGHT' },
        ];

        for (const { row, col, move } of directions) {
            const newRow = zeroRow + row;
            const newCol = zeroCol + col;
            if (newRow >= 0 && newRow < k && newCol >= 0 && newCol < k) {
                const newZeroIndex = newRow * k + newCol;
                const newState = [...state];
                [newState[zeroIndex], newState[newZeroIndex]] = [newState[newZeroIndex], newState[zeroIndex]];
                moves.push({ state: newState, move });
            }
        }
        return moves;
    }

    // A* Algorithm
    function solvePuzzle(initialState, goalState) {
        const openSet = [];
        const closedSet = new Set();
        const cameFrom = new Map();

        openSet.push({ state: initialState, g: 0, h: calculateHeuristic(initialState), moves: [] });

        while (openSet.length > 0) {
            openSet.sort((a, b) => (a.g + a.h) - (b.g + b.h)); // Sort by f = g + h
            const current = openSet.shift();

            if (JSON.stringify(current.state) === JSON.stringify(goalState)) {
                return current.moves;
            }

            closedSet.add(JSON.stringify(current.state));

            for (const { state: neighborState, move } of generateMoves(current.state)) {
                const neighborKey = JSON.stringify(neighborState);

                if (closedSet.has(neighborKey)) {
                    continue;
                }

                const gScore = current.g + 1;

                const existingNode = openSet.find((node) => JSON.stringify(node.state) === neighborKey);

                if (!existingNode || gScore < existingNode.g) {
                    const hScore = calculateHeuristic(neighborState);
                    const newNode = {
                        state: neighborState,
                        g: gScore,
                        h: hScore,
                        moves: [...current.moves, move],
                    };

                    if (!existingNode) {
                        openSet.push(newNode);
                    } else {
                        Object.assign(existingNode, newNode);
                    }
                }
            }
        }

        return null; // No solution found
    }

    const solution = solvePuzzle(initialState, goalState);

    if (solution) {
        console.log(solution.length);
        console.log(solution.join('\n'));
    } else {
        console.log("No solution found");
    }
}

// Read the input from the file
const input = fs.readFileSync('input.txt', 'utf-8');
processData(input);
