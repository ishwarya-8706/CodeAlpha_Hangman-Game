# CodeAlpha_Hangman-Game
import random

def hangman():
    print("==== Welcome to Hangman Game ====\n")

    # 5 predefined words
    words = ["python", "github", "hangman", "random", "console"]

    # Select a random word
    secret_word = random.choice(words)

    # Create a list to store guessed letters (initially all _ )
    guessed = ["_"] * len(secret_word)

    # Keep track of incorrect guesses
    incorrect_guesses = 0
    max_incorrect = 6

    used_letters = []   # store letters already guessed

    while incorrect_guesses < max_incorrect:
        print("\nWord:", " ".join(guessed))
        print("Incorrect guesses:", incorrect_guesses, "/", max_incorrect)
        print("Used letters:", ", ".join(used_letters))

        guess = input("Guess a letter: ").lower()

        # Validate input
        if len(guess) != 1 or not guess.isalpha():
            print("Please enter only one letter.")
            continue

        if guess in used_letters:
            print("You already guessed that letter!")
            continue

        used_letters.append(guess)

        # Check if guess is in the secret word
        if guess in secret_word:
            print("✔ Good guess!")

            # Update guessed list where the letter appears
            for i in range(len(secret_word)):
                if secret_word[i] == guess:
                    guessed[i] = guess
        else:
            print("✘ Wrong guess!")
            incorrect_guesses += 1

        # Check for win condition
        if "_" not in guessed:
            print("\n🎉 CONGRATULATIONS! You guessed the word:", secret_word)
            break

    else:
        # Runs only when loop ends without break (player loses)
        print("\n💀 GAME OVER! You ran out of guesses.")
        print("The correct word was:", secret_word)


# Run the game
if __name__ == "__main__":
    hangman()
