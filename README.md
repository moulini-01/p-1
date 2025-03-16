//# p-1
//project on gaming application
#include <stdio.h>

// Function to display the Tic-Tac-Toe board
void displayBoard(char board[3][3]) {
    printf("\n");
    for (int i = 0; i < 3; i++) {
        printf(" %c | %c | %c \n", board[i][0], board[i][1], board[i][2]);
        if (i < 2) {
            printf("---|---|---\n");
        }
    }
    printf("\n");
}

// Function to check if a player has won
int checkWin(char board[3][3], char player) {
    // Check rows and columns
    for (int i = 0; i < 3; i++) {
        if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) ||
            (board[0][i] == player && board[1][i] == player && board[2][i] == player)) {
            return 1; // Player wins
        }
    }
    // Check diagonals
    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player)) {
        return 1; // Player wins
    }
    return 0; // No winner yet
}

// Function to check if the board is full (draw)
int checkDraw(char board[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] == ' ') {
                return 0; // Board is not full
            }
        }
    }
    return 1; // Board is full (draw)
}

int main() {
    char board[3][3] = {
        {' ', ' ', ' '},
        {' ', ' ', ' '},
        {' ', ' ', ' '}
    };
    int row, col;
    char currentPlayer = 'X'; // Player X starts first
    int moveCount = 0;

    printf("Welcome to Tic-Tac-Toe!\n");
    printf("Player 1: X | Player 2: O\n");

    while (1) {
        // Display the board
        displayBoard(board);

        // Get the current player's move
        printf("Player %c's turn. Enter row (1-3) and column (1-3): ", currentPlayer);
        scanf("%d %d", &row, &col);

        // Adjust to 0-based indexing
        row--;
        col--;

        // Validate the move
        if (row < 0 || row > 2 || col < 0 || col > 2 || board[row][col] != ' ') {
            printf("Invalid move! Try again.\n");
            continue;
        }

        // Update the board
        board[row][col] = currentPlayer;
        moveCount++;

        // Check if the current player has won
        if (checkWin(board, currentPlayer)) {
            displayBoard(board);
            printf("Player %c wins! Congratulations!\n", currentPlayer);
            break;
        }

        // Check if the game is a draw
        if (checkDraw(board)) {
            displayBoard(board);
            printf("It's a draw! Good game!\n");
            break;
        }

        // Switch players
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    return 0;
}
