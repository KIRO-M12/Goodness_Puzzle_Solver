'use strict';

process.stdin.resume();
process.stdin.setEncoding('utf-8');

let inputString = '';
let currentLine = 0;

process.stdin.on('data', function (inputStdin) {
    inputString += inputStdin;
});

process.stdin.on('end', function () {
    inputString = inputString.split('\n');
    main();
});

function readLine() {
    return inputString[currentLine++];
}

// Calculate goodness for the matrix
function calculateGoodness(matrix, x, y, size) {
    let goodness = 0;

    // Use flat loops for faster checks
    for (let i = x; i < x + size; i++) {
        for (let j = y; j < y + size; j++) {
            if (j + 1 < y + size && matrix[i][j] < matrix[i][j + 1]) {
                goodness++;
            }
            if (i + 1 < x + size && matrix[i][j] < matrix[i + 1][j]) {
                goodness++;
            }
        }
    }
    return goodness;
}

// Rotate sub-square clockwise
function rotateClockwise(matrix, x, y, size) {
    for (let layer = 0; layer < Math.floor(size / 2); layer++) {
        let first = layer;
        let last = size - 1 - layer;
        for (let i = 0; i < last - first; i++) {
            let temp = matrix[x + first][y + first + i];
            matrix[x + first][y + first + i] = matrix[x + last - i][y + first];
            matrix[x + last - i][y + first] = matrix[x + last][y + last - i];
            matrix[x + last][y + last - i] = matrix[x + first + i][y + last];
            matrix[x + first + i][y + last] = temp;
        }
    }
}

function main() {
    const n = parseInt(readLine().trim(), 10);
    const matrix = [];

    for (let i = 0; i < n; i++) {
        matrix.push(readLine().split(' ').map(Number));
    }

    const moves = [];
    const visited = new Set();
    let maxGoodness = calculateGoodness(matrix, 0, 0, n);

    const MAX_MOVES = 500; // Limit moves to avoid timeout

    while (moves.length < MAX_MOVES) {
        let bestMove = null;
        let bestImprovement = 0;

        for (let size = Math.min(6, n); size >= 2; size--) { // Reduce sub-square size to 6 for faster processing
            for (let x = 0; x <= n - size; x++) {
                for (let y = 0; y <= n - size; y++) {
                    const key = `${x}-${y}-${size}`;
                    if (visited.has(key)) continue;

                    const originalGoodness = calculateGoodness(matrix, x, y, size);

                    // Rotate and calculate goodness
                    rotateClockwise(matrix, x, y, size);
                    const newGoodness = calculateGoodness(matrix, x, y, size);

                    if (newGoodness - originalGoodness > bestImprovement) {
                        bestImprovement = newGoodness - originalGoodness;
                        bestMove = { x: x + 1, y: y + 1, size }; // Use 1-based indexing
                    }

                    // Undo rotation
                    rotateClockwise(matrix, x, y, size);
                    rotateClockwise(matrix, x, y, size);
                    rotateClockwise(matrix, x, y, size);
                }
            }
        }

        if (bestMove && bestImprovement > 0) {
            moves.push(bestMove);
            rotateClockwise(matrix, bestMove.x - 1, bestMove.y - 1, bestMove.size);
            visited.add(`${bestMove.x - 1}-${bestMove.y - 1}-${bestMove.size}`);
            maxGoodness += bestImprovement;
        } else {
            break;
        }
    }

    console.log(moves.length);
    moves.forEach(move => console.log(`${move.x} ${move.y} ${move.size}`));
}
