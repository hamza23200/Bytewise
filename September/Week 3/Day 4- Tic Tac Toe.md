```python
winner = None
current_player = 'X'
game_still_going = True

def display_board():
    print(board[0]+ "|" + board[1] + "|"+ board[2])
    print(board[3]+ "|" + board[4] + "|"+ board[5])
    print(board[6]+ "|" + board[7] + "|"+ board[8])

def play_game():
    display_board()

    while game_still_going:

        handle_turn(current_player)
        check_if_gameover()
        flip_player()

    if winner == 'X' or winner == "0":
        print(winner + " won the match")
    elif winner == None:
        print("Tie")

def handle_turn(player):
    print(player + "'s turn")
    position = input("Throw your move from 1-9 ")
    valid = False
    while not valid:
        while position not in ["1","2","3","4","5","6","7","8","9"]:
            position = input("please choose your position between 1-9 : ")
        position = int(position) - 1

        if board[position] == "-":
            valid = True
        else:
            print("You can't go there man!! it's already filled")
    board[position] = player

    display_board()

def check_if_gameover():
    check_if_win()
    check_if_tie()
def check_if_win():
    global winner
    row_win = check_rows()
    column_win = check_columns()
    diagnol_win = check_diagnols()
    if row_win:
        winner = row_win
    elif column_win:
        winner = column_win
    elif diagnol_win:
        winner = diagnol_win

def check_rows():
    global game_still_going
    row_1 = board[0] == board[1] == board[2] != "-"
    row_2 = board[3] == board[4] == board[5] != "-"
    row_3 = board[6] == board[7] == board[8] != "-"
    if row_1 or row_2 or row_3:
        game_still_going = False
    if row_1:
        return board[0]
    if row_2:
        return board[3]
    if row_3:
        return board[6]
    else:
        return None
def check_columns():
    global game_still_going
    col_1 = board[0] == board[3] == board[6] != "-"
    col_2 = board[1] == board[4] == board[7] != "-"
    col_3 = board[2] == board[5] == board[8] != "-"
    if col_1 or col_2 or col_3:
        game_still_going = False
    if col_1:
        return board[0]
    if col_2:
        return board[1]
    if col_3:
        return board[2]
    else:
        return None
def check_diagnols():
    global game_still_going
    diag_1 = board[0] == board[4] == board[8] != "-"
    diag_2 = board[6] == board[4] == board[2] != "-"
    if diag_1 or diag_2:
        game_still_going = False
    if diag_1:
        return board[0]
    if diag_2:
        return board[6]
    else:
        return None
def check_if_tie():
    global game_still_going
    if "-" not in board:
        game_still_going = False
        #return True
    else:
        return False
def flip_player():
    global current_player
    if current_player == "X":
        current_player = "O"
    elif current_player == "O":
        current_player = "X"
play_game()
```
