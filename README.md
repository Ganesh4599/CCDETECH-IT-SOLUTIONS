Tic-Tac-Toe Game:
In the above task I Developed a text-based Tic-Tac-Toe game where two players human and human or human and
computer 
In that they take turns placing their marks on a 3x3 grid. 
And The program will be checking for wins, draws, and handle invalid moves.

import random

def print_board(board):
    for row in board:
        print(" | ".join(row))
        print("-" * 5)

def is_winner(board, player):
    // Check rows, columns, and diagonals for a win
    for i in range(3):
        if all(board[i][j] == player for j in range(3)) or \
           all(board[j][i] == player for j in range(3)):
            return True
    if all(board[i][i] == player for i in range(3)) or \
       all(board[i][2 - i] == player for i in range(3)):
        return True
    return False

def is_board_full(board):
    // Check if the board is full
    return all(board[i][j] != ' ' for i in range(3) for j in range(3))

def is_valid_move(board, row, col):
   // Check if the move is within the board and the cell is empty
    return 0 <= row < 3 and 0 <= col < 3 and board[row][col] == ' '

def get_human_move():
    try:
        row = int(input("Enter the row (0, 1, or 2): "))
        col = int(input("Enter the column (0, 1, or 2): "))
        return row, col
    except ValueError:
        print("Invalid input. Please enter numbers for row and column.")
        return get_human_move()

def get_computer_move(board):
    // Simple computer player: Randomly choose an empty cell
    empty_cells = [(i, j) for i in range(3) for j in range(3) if board[i][j] == ' ']
    return random.choice(empty_cells)

def play_tic_tac_toe():
    board = [[' ' for _ in range(3)] for _ in range(3)]
    current_player = 'X'

    while True:
        print_board(board)

        if current_player == 'X':
            print("\nPlayer X's turn:")
            row, col = get_human_move()
        else:
            print("\nPlayer O's turn:")
            row, col = get_computer_move(board)

        if is_valid_move(board, row, col):
            board[row][col] = current_player
            if is_winner(board, current_player):
                print_board(board)
                print(f"\nPlayer {current_player} wins!")
                break
            elif is_board_full(board):
                print_board(board)
                print("\nIt's a draw!")
                break
            else:
                current_player = 'O' if current_player == 'X' else 'X'
        else:
            print("\nInvalid move. Try again.")

if __name__ == "__main__":
    play_tic_tac_toe()
