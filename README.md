#include <iostream>
#include <vector>

// Function to print the Tic-Tac-Toe board
void printBoard(const std::vector<std::vector<char>>& board) {
    for (const auto& row : board) {
        for (const auto& cell : row) {
            std::cout << cell << " ";
        }
        std::cout << std::endl;
    }
}

// Function to check if a player has won
bool checkWin(const std::vector<std::vector<char>>& board, char player) {
    // Check rows and columns
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == player && board[i][1] == player && board[i][2] == player)
            return true;
        if (board[0][i] == player && board[1][i] == player && board[2][i] == player)
            return true;
    }

    // Check diagonals
    if (board[0][0] == player && board[1][1] == player && board[2][2] == player)
        return true;
    if (board[0][2] == player && board[1][1] == player && board[2][0] == player)
        return true;

    return false;
}

// Function to play the game
void playGame() {
    std::vector<std::vector<char>> board(3, std::vector<char>(3, ' '));
    char currentPlayer = 'X';
    int row, col;

    std::cout << "Welcome to Tic-Tac-Toe!" << std::endl;

    while (true) {
        // Print the current board
        printBoard(board);

        // Get the player's move
        std::cout << "Player " << currentPlayer << ", enter your move (row col): ";
        std::cin >> row >> col;

        // Check if the move is valid
        if (row < 0 || row >= 3 || col < 0 || col >= 3 || board[row][col] != ' ') {
            std::cout << "Invalid move. Try again." << std::endl;
            continue;
        }

        // Make the move
        board[row][col] = currentPlayer;

        // Check if the current player has won
        if (checkWin(board, currentPlayer)) {
            std::cout << "Player " << currentPlayer << " wins!" << std::endl;
            break;
        }

        // Check if it's a draw
        bool isDraw = true;
        for (const auto& row : board) {
            for (const auto& cell : row) {
                if (cell == ' ') {
                    isDraw = false;
                    break;
                }
            }
        }
        if (isDraw) {
            std::cout << "It's a draw!" << std::endl;
            break;
        }

        // Switch to the other player
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }
}

int main() {
    playGame();
    return 0;
}
