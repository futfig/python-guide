# Python Tic-Tac-Toe Learning Guide

This guide walks you through learning Python basics by building a command-line Tic-Tac-Toe game. Each step introduces a core concept and immediately applies it to the project so you can see how fundamentals power a real program.

## 1) Set up your environment
- Install Python 3.11+.
- Create a project folder and a virtual environment: `python -m venv .venv && source .venv/bin/activate`.
- Add a `main.py` file where you will write the game.

## 2) Represent the game board with lists
- Start with a 1D list of nine strings to hold the squares: `board = [" "] * 9`.
- Use indices `0-8` to map to positions; later you can map user-friendly positions (1-9) to these indices.
- Practice reading and writing list items: `board[0] = "X"`.

### Printing the board
- Write a helper `print_board(board)` that formats the 1D list into a 3x3 grid using `print()` and string joins.
- Example formatting idea:
  ```python
  def print_board(board):
      rows = [" | ".join(board[i:i+3]) for i in range(0, 9, 3)]
      print("\n-+-+-\n".join(rows))
  ```
- Call `print_board(board)` after each move to visualize state.

## 3) Take input from the CLI
- Use `input("Choose a position (1-9): ")` to read a string from the user.
- Convert to an integer and to a board index: `choice = int(user_input) - 1`.
- Validate input with `if` statements: ensure the value is between 0 and 8 and the square is empty.
- Loop until valid: `while True: ... break` once a good move is placed.

## 4) Apply moves with simple control flow
- Use `if/else` to decide whose turn it is and to handle invalid moves.
- Alternate players with a variable like `current_player = "X" if current_player == "O" else "O"`.
- When a user picks a square, set `board[index] = current_player` and reprint the board.

## 5) Add win and draw detection
- Store winning index combinations in a list of tuples:
  ```python
  WIN_LINES = [
      (0, 1, 2), (3, 4, 5), (6, 7, 8),  # rows
      (0, 3, 6), (1, 4, 7), (2, 5, 8),  # columns
      (0, 4, 8), (2, 4, 6),             # diagonals
  ]
  ```
- After each move, loop through `WIN_LINES` and check if all three positions match the current player: `if board[a] == board[b] == board[c] == current_player`.
- Detect draws by checking if no spaces remain: `if " " not in board`.

## 6) Add a simple computer opponent
- Start basic: pick the first available square with a loop and `break` when you place `"O"`.
- Use `if/elif/else` to add slightly smarter logic:
  - If you can win on this turn, take that square.
  - Else if the opponent can win next turn, block that square.
  - Else take the center, a corner, or the first open spot.
- Keep the AI logic in a function like `computer_move(board)` for clarity.

## 7) Organize code into functions
- Suggested functions:
  - `print_board(board)`
  - `get_player_move(board)`
  - `computer_move(board)`
  - `check_winner(board)`
  - `play_game()` (contains the main loop)
- Keeping logic in functions makes the program easier to test and expand.

## 8) Play loop
- In `play_game()`, alternate between the human and computer:
  ```python
  def play_game():
      board = [" "] * 9
      current_player = "X"
      while True:
          print_board(board)
          if current_player == "X":
              get_player_move(board)
          else:
              computer_move(board)
          winner = check_winner(board)
          if winner:
              print_board(board)
              print(f"{winner} wins!")
              break
          if " " not in board:
              print_board(board)
              print("It's a draw!")
              break
          current_player = "O" if current_player == "X" else "X"
  ```
- Run the game with `python main.py` and play a few rounds.

## 9) Experiments to deepen understanding
- Replace the list with a list of lists (2D board) to compare indexing.
- Add input error handling with `try/except` around `int()` conversion.
- Store moves in a history list so you can undo.
- Add a replay loop that asks whether to play again.
- Write unit tests for `check_winner` using `pytest`.

## 10) Next steps
- Refactor the board into a small class to practice methods and encapsulation.
- Swap the simple AI with the minimax algorithm to see recursion and scoring.
- Explore type hints (`list[str]`, `Optional[str]`) and docstrings to document your functions.
- Add color output with libraries like `colorama` to improve the CLI experience.

Following this plan will give you hands-on practice with Python lists, conditionals, loops, functions, input/output, and simple game logic—all while building a complete Tic-Tac-Toe game.
