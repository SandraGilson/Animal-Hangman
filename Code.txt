import random

def choose_word(word_list):
    return random.choice(word_list)

def display_hangman(tries):
    stages = [
        """
           -----
           |   |
           O   |
          /|\\  |
          / \\  |
               |
        ---------
        """,
        """
           -----
           |   |
           O   |
          /|\\  |
          /    |
               |
        ---------
        """,
        """
           -----
           |   |
           O   |
          /|\\  |
               |
               |
        ---------
        """,
        """
           -----
           |   |
           O   |
          /|   |
               |
               |
        ---------
        """,
        """
           -----
           |   |
           O   |
           |   |
               |
               |
        ---------
        """,
        """
           -----
           |   |
           O   |
               |
               |
               |
        ---------
        """,
        """
           -----
           |   |
               |
               |
               |
               |
        ---------
        """
    ]
    return stages[tries]

def play_hangman(word_list):
    word = choose_word(word_list)
    word_letters = set(word)
    guessed_letters = set()
    tries = 6

    print("Welcome to Hangman!")
    print(display_hangman(tries))
    print(f"Word: {'_ ' * len(word)}\n")
    hint_used = False

    while tries > 0 and word_letters:
        guess = input("Guess a letter or type 'hint' for a hint: ").lower()

        if guess == 'hint' and not hint_used:
            hint = random.choice(list(word_letters))
            print(f"Here's a hint! One of the letters is: {hint}")
            hint_used = True
            continue

        if guess in guessed_letters:
            print("You already guessed that letter.")
        elif guess in word_letters:
            word_letters.remove(guess)
            guessed_letters.add(guess)
            print("Correct guess!")
        else:
            tries -= 1
            guessed_letters.add(guess)
            print("Incorrect guess.")

        word_display = [letter if letter in guessed_letters else '_' for letter in word]
        print(display_hangman(tries))
        print(f"Word: {' '.join(word_display)}\n")

    if not word_letters:
        print(f"Congratulations! You guessed the word: {word}")
    else:
        print(f"Game Over! The word was: {word}")

def main():
    word_list = ['elephant', 'tiger', 'kangaroo', 'dolphin', 'giraffe', 'penguin', 'koala', 'hippopotamus', 'rhinoceros', 'alligator']
    games_played = 0
    play_again = 'y'

    while play_again.lower() == 'y':
        play_hangman(word_list)
        games_played += 1
        play_again = input("Do you want to play again? (y/n): ")

    print(f"Thanks for playing! You played {games_played} games.")

if __name__ == "__main__":
    main()
