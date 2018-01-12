#%%
import random

def drawBoard(board):
    # This function prints out the board that it was passed.

    # "board" is a list of 10 strings representing the board (ignore index 0)
    
    print(' ' + board[1] + ' | ' + board[2] + ' | ' + board[3])
    print('-----------')
    print(' ' + board[4] + ' | ' + board[5] + ' | ' + board[6])
    print('-----------')
    print(' ' + board[7] + ' | ' + board[8] + ' | ' + board[9])

def playerSelect():
    # Player to choose either 'X' or 'O'
    # Returns result as a list with the player's letter as the first item, and the computer's letter as the second.
    letter = ''
    while not (letter == 'X' or letter == 'O'):
        print('Select X or O?')
        letter = input().upper()

    if letter == 'X':
        return ['X', 'O']
    else:
        return ['O', 'X']

def firstServe():
    # Randomly choose the player who goes first.
    if random.randint(0, 1) == 0:
        return 'player'
    else:
        return 'computer'

def nextGame():
    # This function returns True if the player wants to play again, otherwise it returns False.
    print('Do you want to play again? (yes or no)')
    return input().lower().startswith('y')

def makeMove(board, letter, move):
    board[move] = letter

def winner(board, letter): 
    #returns true if player/computer won the game with the given letter and board
    return ((board[1] == board[2] == board[3] == letter) or # across the top
    (board[4] == board[5] == board[6] == letter) or # across the middle
    (board[7] == board[8] == board[9] == letter) or # across the bottom
    (board[1] == board[4] == board[7] == letter) or # down the left side
    (board[2] == board[5] == board[8] == letter) or # down the middle
    (board[3] == board[6] == board[9] == letter) or # down the right side
    (board[1] == board[5] == board[9] == letter) or # diagonal
    (board[3] == board[5] == board[7] == letter)) # diagonal

def boardCopy(board):
    # Make a duplicate of the board list and return it the duplicate.
    dupeBoard = []

    for i in board:
        dupeBoard.append(i)

    return dupeBoard

def isSpaceFree(board, move):
    # Return true if the passed move is free on the passed board.
    return board[move] == ' '

def getPlayerMove(board):
    # Let the player type in his move.
    move = ' '
    while move not in '1 2 3 4 5 6 7 8 9'.split() or not isSpaceFree(board, int(move)):
        print('What is your next move? (1-9)')
        move = input()
    return int(move)

def chooseRandomMoveFromList(board, movesList):
    # Returns a valid move from the passed list on the passed board.
    # Returns None if there is no valid move.
    possibleMoves = []
    for i in movesList:
        if isSpaceFree(board, i):
            possibleMoves.append(i)

    if len(possibleMoves) != 0:
        return random.choice(possibleMoves)
    else:
        return None

def getComputerMove(board, computerLetter):
    # Given a board and the computer's letter, determine where to move and return that move.
    if computerLetter == 'X':
        playerLetter = 'O'
    else:
        playerLetter = 'X'

    # Here is our algorithm for our Tic Tac Toe AI:
    # First, check if we can win in the next move
    for i in range(1, 10):
        copy = boardCopy(board)
        if isSpaceFree(copy, i):
            makeMove(copy, computerLetter, i)
            if winner(copy, computerLetter):
                return i

    # Check if the player could win on his next move, and block them.
    for i in range(1, 10):
        copy = boardCopy(board)
        if isSpaceFree(copy, i):
            makeMove(copy, playerLetter, i)
            if winner(copy, playerLetter):
                return i

    # Try to take one of the corners, if they are free.
    move = chooseRandomMoveFromList(board, [1, 3, 7, 9])
    if move != None:
        return move

    # Try to take the center, if it is free.
    if isSpaceFree(board, 5):
        return 5

    # Move on one of the sides.
    return chooseRandomMoveFromList(board, [2, 4, 6, 8])

def isBoardFull(board):
    # Return True if every space on the board has been taken. Otherwise return False.
    for i in range(1, 10):
        if isSpaceFree(board, i):
            return False
    return True


print('Welcome to Tic Tac Toe!')
print('\n')
print('Instructions to be followed: ')
print('-------------------------------')
print('Choose your letter to play in ','X',' or ','O',' when asked ')
print('Game is positioned as follows')
print('\n')
print(' 1 | 2 | 3 ')
print('-----------')
print(' 4 | 5 | 6 ')
print('-----------')
print(' 7 | 8 | 2 ')
print('\n')

while True:
    # Reset the board
    theBoard = [' '] * 10
    playerLetter, computerLetter = playerSelect()
    turn = firstServe()
    print('The ' + turn + ' will go first.')
    gameIsPlaying = True

    while gameIsPlaying:
        if turn == 'player':
            # Player's turn.
            drawBoard(theBoard)
            move = getPlayerMove(theBoard)
            makeMove(theBoard, playerLetter, move)

            if winner(theBoard, playerLetter):
                drawBoard(theBoard)
                print('Congo buddy! you have won the game... ')
                gameIsPlaying = False
            else:
                if isBoardFull(theBoard):
                    drawBoard(theBoard)
                    print('Uh no! The game is on tie...! ')
                    break
                else:
                    turn = 'computer'

        else:
            # Computer's turn.
            move = getComputerMove(theBoard, computerLetter)
            makeMove(theBoard, computerLetter, move)

            if winner(theBoard, computerLetter):
                drawBoard(theBoard)
                print('Sorry! You have lost the game... ')
                gameIsPlaying = False
            else:
                if isBoardFull(theBoard):
                    drawBoard(theBoard)
                    print('Uh no! The game is on tie...! ')
                    break
                else:
                    turn = 'player'

    if not nextGame():
        break
