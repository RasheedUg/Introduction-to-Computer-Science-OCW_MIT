# Introduction-to-Computer-Science-OCW_MIT
# Here i will occasionally post my code solutions to Introduction to Computer science problem sets
# problem set 3-hangman
import random

WORDLIST_FILENAME = "words.txt"

def loadWords():
    """
    Returns a list of valid words. Words are strings of lowercase letters.
    
    Depending on the size of the word list, this function may
    take a while to finish.
    """
    print("Loading word list from file...")
    # inFile: file
    inFile = open(WORDLIST_FILENAME, 'r')
    # line: string
    line = inFile.readline()
    # wordlist: list of strings
    wordlist = line.split()
    print("  ", len(wordlist), "words loaded.")
    return wordlist

def chooseWord(wordlist):
    """
    wordlist (list): list of words (strings)

    Returns a word from wordlist at random
    """
    return random.choice(wordlist)

# end of helper code
# -----------------------------------

# Load the list of words into the variable wordlist
# so that it can be accessed from anywhere in the program
wordlist = loadWords()

def isWordGuessed(secretWord, lettersGuessed):
    '''
    secretWord: string, the word the user is guessing
    lettersGuessed: list, what letters have been guessed so far
    returns: boolean, True if all the letters of secretWord are in lettersGuessed;
      False otherwise
    '''
    # FILL IN YOUR CODE HERE...
    
    
    for letter in secretWord:
        if letter not in lettersGuessed:
            return False
        else:
            return True
                
                

def getGuessedWord(secretWord, lettersGuessed):
    '''
    secretWord: string, the word the user is guessing
    lettersGuessed: list, what letters have been guessed so far
    returns: string, comprised of letters and underscores that represents
      what letters in secretWord have been guessed so far.
    '''
    # FILL IN YOUR CODE HERE...
    
    result = " "
    for letter in secretWord:
        if letter in lettersGuessed:
            result += letter
        else:
            result = result + '-'
    return result
            
            

def getAvailableLetters(lettersGuessed):
    '''
    lettersGuessed: list, what letters have been guessed so far
    returns: string, comprised of letters that represents what letters have not
      yet been guessed.
    '''
    # FILL IN YOUR CODE HERE...
    import string
    alphabet = string.ascii_lowercase
    alphabet_list=list(alphabet)
    for letter in lettersGuessed:
        if letter in alphabet_list:
            alphabet_list.remove(letter)
    new_alphabet = ''.join(alphabet_list)
    return new_alphabet           
    

def hangman(secretWord):
    '''
    secretWord: string, the secret word to guess.

    Starts up an interactive game of Hangman.

    * At the start of the game, let the user know how many 
      letters the secretWord contains.

    * Ask the user to supply one guess (i.e. letter) per round.

    * The user should receive feedback immediately after each guess 
      about whether their guess appears in the computers word.

    * After each round, you should also display to the user the 
      partially guessed word so far, as well as letters that the 
      user has not yet guessed.

    Follows the other limitations detailed in the problem write-up.
    '''
    # FILL IN YOUR CODE HERE...

    print('The secret word has', str(len(secretWord)), 'letters' )
    
    
    lettersGuessed = []
    numGuess= 8
    
    while numGuess > 0:
        guess=input('Guess a letter:')
        if guess not in secretWord:
            numGuess -=1
            print('Oops! letter guessed is not in', getGuessedWord(secretWord, lettersGuessed))
            print('Available letters:', getAvailableLetters(lettersGuessed))
        
        elif guess in secretWord:
            lettersGuessed.append(guess)
            numGuess -=1
            print('Correct guess' + getGuessedWord(secretWord, lettersGuessed))
            print ('Available letters:', getAvailableLetters(lettersGuessed))
            
        elif guess not in alphabet:
            numGuess -=1
            print('You have already guessed that letter!')
        
        
    if isWordGuessed(secretWord, lettersGuessed) == True:
        print('Congs! You have guessed the word',  secretWord)
    else:
        print('Gameover')
            
    




# When you've completed your hangman function, uncomment these two lines
# and run this file to test! (hint: you might want to pick your own
# secretWord while you're testing)

secretWord = chooseWord(wordlist).lower()
hangman(secretWord)

