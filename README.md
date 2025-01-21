#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Function to generate random choices for the computer
int get_computer_choice() {
    return rand() % 3; // 0 = Snake, 1 = Water, 2 = Gun
}

// Function to determine the winner
void determine_winner(int user_choice, int computer_choice) {
    if (user_choice == computer_choice) {
        printf("It's a tie!\n");
    } else if ((user_choice == 0 && computer_choice == 1) || // Snake beats Water
               (user_choice == 1 && computer_choice == 2) || // Water beats Gun
               (user_choice == 2 && computer_choice == 0)) { // Gun beats Snake
        printf("You win!\n");
    } else {
        printf("Computer wins!\n");
    }
}

int main() {
    int user_choice, computer_choice;
    char *choices[] = {"Snake", "Water", "Gun"};

    // Seed the random number generator
    srand(time(0));

    printf("Welcome to Snake, Water, and Gun game!\n");
    printf("Enter your choice:\n");
    printf("0 for Snake, 1 for Water, 2 for Gun\n");

    // Loop for continuous play
    while (1) {
        printf("Your choice: ");
        scanf("%d", &user_choice);

        // Check for valid input
        if (user_choice < 0 || user_choice > 2) {
            printf("Invalid choice! Please choose a valid option.\n");
            continue;
        }

        // Generate computer's choice
        computer_choice = get_computer_choice();

        printf("You chose: %s\n", choices[user_choice]);
        printf("Computer chose: %s\n", choices[computer_choice]);

        // Determine the winner
        determine_winner(user_choice, computer_choice);

        // Ask if the user wants to play again
        char play_again;
        printf("Do you want to play again? (y/n): ");
        scanf(" %c", &play_again);

        if (play_again == 'n' || play_again == 'N') {
            printf("Thanks for playing!\n");
            break;
        }
    }

    return 0;
}
