# snake-water-gun
import random
import os
import time

# Game Configuration
CHOICES = {
    "s": "Snake",
    "w": "Water",
    "g": "Gun"
}

WINNING_ROUNDS = 3


def clear_screen():
    os.system("cls" if os.name == "nt" else "clear")


def display_header():
    print("=" * 45)
    print("          SNAKE WATER GUN GAME")
    print("=" * 45)
    print("       Snake 🐍 | Water 💧 | Gun 🔫")
    print("-" * 45)


def display_rules():
    print("\nGAME RULES")
    print("1. Snake drinks Water.")
    print("2. Water damages Gun.")
    print("3. Gun kills Snake.")
    print("4. Same choices result in a Draw.")
    print(f"\nFirst player to win {WINNING_ROUNDS} rounds wins!")
    print("-" * 45)


def get_user_choice():
    while True:
        print("\nChoose your option:")
        print("S - Snake")
        print("W - Water")
        print("G - Gun")

        choice = input("\nYour choice: ").strip().lower()

        if choice in CHOICES:
            return choice

        print("Invalid input! Please enter S, W, or G.")


def determine_winner(user, computer):
    if user == computer:
        return "draw"

    winning_combinations = [
        ("s", "w"),
        ("w", "g"),
        ("g", "s")
    ]

    if (user, computer) in winning_combinations:
        return "user"

    return "computer"


def display_score(user_score, computer_score, draws):
    print("\n" + "-" * 45)
    print("                 SCOREBOARD")
    print("-" * 45)
    print(f"Player Score   : {user_score}")
    print(f"Computer Score : {computer_score}")
    print(f"Draws          : {draws}")
    print("-" * 45)


def play_game():
    user_score = 0
    computer_score = 0
    draws = 0
    round_number = 1

    while user_score < WINNING_ROUNDS and computer_score < WINNING_ROUNDS:

        print(f"\nROUND {round_number}")
        print("-" * 45)

        user = get_user_choice()
        computer = random.choice(list(CHOICES.keys()))

        print("\nYou chose      :", CHOICES[user])
        print("Computer chose :", CHOICES[computer])

        result = determine_winner(user, computer)

        if result == "draw":
            print("\nResult: It's a DRAW!")
            draws += 1

        elif result == "user":
            print("\nResult: YOU WIN THIS ROUND!")
            user_score += 1

        else:
            print("\nResult: COMPUTER WINS THIS ROUND!")
            computer_score += 1

        display_score(user_score, computer_score, draws)
        round_number += 1

        if user_score < WINNING_ROUNDS and computer_score < WINNING_ROUNDS:
            input("\nPress Enter for next round...")

    print("\n" + "=" * 45)

    if user_score == WINNING_ROUNDS:
        print("       CONGRATULATIONS! YOU WON!")
    else:
        print("          COMPUTER WINS THE GAME!")

    print("=" * 45)

    display_score(user_score, computer_score, draws)


def main():
    while True:
        clear_screen()
        display_header()
        display_rules()

        print("\n1. Start Game")
        print("2. Exit")

        option = input("\nEnter your choice: ").strip()

        if option == "1":
            clear_screen()
            display_header()
            play_game()

            replay = input("\nDo you want to play again? (y/n): ").strip().lower()

            if replay != "y":
                print("\nThanks for playing! Goodbye.")
                break

        elif option == "2":
            print("\nThanks for playing! Goodbye.")
            break

        else:
            print("\nInvalid option! Try again.")
            time.sleep(1)


if __name__ == "__main__":
    main()
    
