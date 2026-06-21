# Tic-Tac-Toe-Game-in-C-
#include <iostream>
using namespace std;

char board[3][3];

// Initialize Board
void initializeBoard() {
    char value = '1';

    for(int i = 0; i < 3; i++) {
        for(int j = 0; j < 3; j++) {
            board[i][j] = value++;
        }
    }
}

// Display Board
void displayBoard() {
    cout << "\n";

    for(int i = 0; i < 3; i++) {
        cout << " ";
        for(int j = 0; j < 3; j++) {
            cout << board[i][j];

            if(j < 2)
                cout << " | ";
        }

        if(i < 2)
            cout << "\n-----------\n";
    }

    cout << "\n";
}

// Check Winner
char checkWinner() {

    // Rows
    for(int i = 0; i < 3; i++) {
        if(board[i][0] == board[i][1] &&
           board[i][1] == board[i][2])
            return board[i][0];
    }

    // Columns
    for(int i = 0; i < 3; i++) {
        if(board[0][i] == board[1][i] &&
           board[1][i] == board[2][i])
            return board[0][i];
    }

    // Diagonals
    if(board[0][0] == board[1][1] &&
       board[1][1] == board[2][2])
        return board[0][0];

    if(board[0][2] == board[1][1] &&
       board[1][1] == board[2][0])
        return board[0][2];

    return ' ';
}

// Check Draw
bool isDraw() {
    for(int i = 0; i < 3; i++) {
        for(int j = 0; j < 3; j++) {
            if(board[i][j] != 'X' &&
               board[i][j] != 'O')
                return false;
        }
    }

    return true;
}

// Player Move
void playerMove(char player) {
    int choice;
    bool validMove = false;

    while(!validMove) {

        cout << "\nPlayer " << player
             << ", enter position (1-9): ";
        cin >> choice;

        if(choice < 1 || choice > 9) {
            cout << "Invalid position!\n";
            continue;
        }

        int row = (choice - 1) / 3;
        int col = (choice - 1) % 3;

        if(board[row][col] != 'X' &&
           board[row][col] != 'O') {

            board[row][col] = player;
            validMove = true;
        }
        else {
            cout << "Position already occupied!\n";
        }
    }
}

int main() {

    char replay;

    do {

        initializeBoard();
        char currentPlayer = 'X';
        char winner = ' ';

        while(true) {

            displayBoard();

            playerMove(currentPlayer);

            winner = checkWinner();

            if(winner == 'X' || winner == 'O') {
                displayBoard();
                cout << "\nPlayer "
                     << winner
                     << " Wins!\n";
                break;
            }

            if(isDraw()) {
                displayBoard();
                cout << "\nGame Draw!\n";
                break;
            }

            currentPlayer =
                (currentPlayer == 'X') ? 'O' : 'X';
        }

        cout << "\nPlay Again? (Y/N): ";
        cin >> replay;

    } while(replay == 'Y' || replay == 'y');

    cout << "\nThanks for Playing!\n";

    return 0;
}
