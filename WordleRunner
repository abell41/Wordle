import java.io.File;
import java.io.FileNotFoundException;
import java.util.ArrayList;
import java.util.Scanner;
import java.util.Arrays;

public class WordleRunner {

    public static void main(String[] args) throws FileNotFoundException {

        System.out.println("Welcome to Wordle. \nYour objective is to guess a 5 letter word.");

        Scanner sc = new Scanner(System.in);
        ArrayList < String > possAns = new ArrayList < > ();
        Scanner sc_file = new Scanner(new File("PossibleWords.txt"));

        while (sc_file.hasNext()) {
            possAns.add(sc_file.nextLine());
        }

        // choose the word
        String actualWord = possAns.get(0 + (int) Math.floor(Math.random() * (possAns.size() - 1 - 0 + 1)));
        ArrayList < String > poss_guesses = new ArrayList < > ();
        sc_file = new Scanner(new File("PossibleGuesses.txt"));

        while (sc_file.hasNext()) {
            poss_guesses.add(sc_file.nextLine());
        }

        //2d-array
        String[][] guessSpace = new String[6][];
        guessSpace[0] = new String[]{"-","-","-","-","-"};
        guessSpace[1] = new String[]{"-","-","-","-","-"};
        guessSpace[2] = new String[]{"-","-","-","-","-"};
        guessSpace[3] = new String[]{"-","-","-","-","-"};
        guessSpace[4] = new String[]{"-","-","-","-","-"};
        guessSpace[5] = new String[]{"-","-","-","-","-"};

        System.out.println(Arrays.deepToString(guessSpace[0]) + "\n"
                + Arrays.deepToString(guessSpace[1]) + "\n"
                + Arrays.deepToString(guessSpace[2]) + "\n"
                + Arrays.deepToString(guessSpace[3]) + "\n"
                + Arrays.deepToString(guessSpace[4]) + "\n"
                + Arrays.deepToString(guessSpace[5]));

        System.out.println("Please enter a 5 letter word.");

        String MAKE_GREEN = "\u001B[32m";
        String MAKE_YELLOW = "\u001B[33m"; // 33
        String MAKE_GRAY = "\u001B[90m"; // 90
        String MAKE_RESET = "\u001B[0m";
        int ixGuess = 0;
        int guesses = 6;

        actualWord = "begin";
        System.out.println(actualWord);

        int[] usedLetters = new int[26]; // array to count letters in actualWord
        for (int i = 0; i < 26; i++) // sets the array values to 0
            usedLetters[i] = 0;


            // restrict number of guesses to 6
        while (ixGuess < 6) {
            String player_guess = sc.nextLine().toLowerCase();

            for(char letterSeen : actualWord.toCharArray()) // letter seen, add 1 for every appearance
                    usedLetters[letterSeen - 'a'] += 1;

            for (int i = 0; i< 26; i++) {
                System.out.print(usedLetters[i] + " ");
            }

            if (poss_guesses.contains(player_guess) || possAns.contains(player_guess)) {
                // "player_guess" is in the list "poss_guesses"
                // post: "player_guess" is exactly 5 chars in length
                for (int c = 0; c < 5; ++c) {
                    char letter = player_guess.charAt(c);

                    // process each char: check whether it's in the word, in the right place, etc.
                    if (letter == actualWord.charAt(c)) {
                        // correct place in word
                        usedLetters[letter - 'a'] -= 1; // subtract index that has that letter
                        // ROW index = player guess #
                        // COLUMN index = #th letter in word
                        guessSpace[ixGuess][c] = MAKE_GREEN + letter + MAKE_RESET;
                    }
                    else if (actualWord.indexOf(letter) != -1 && usedLetters[letter - 'a'] > 0) {
                        // condition: letter in word, but not in right place
                        usedLetters[letter - 'a'] -= 1; // subtract index that has that letter
                        guessSpace[ixGuess][c] = MAKE_YELLOW + letter + MAKE_RESET; // makes that index yellow in guessSpace
                    } else // letter not in word
                    {
                        guessSpace[ixGuess][c] = MAKE_GRAY + letter + MAKE_RESET;
                    }
                }
                ixGuess++;
                guesses--;
                System.out.println("You have " + guesses + " guesses left");

                // actualWord, player_guess
                if (player_guess.equals(actualWord)) {
                    // say the player won, and then break out of this loop
                    System.out.println(MAKE_GREEN + actualWord);
                    System.out.println("You win.");

                    break;

                } else {
                    for(String[] guess: guessSpace) {
                        for(String temp: guess) {
                            System.out.print(temp);
                        }
                        System.out.println("");
                    }
                }
            }
            else {
                // reject the guess
                System.out.println("Word not found.");
            }
            if (ixGuess > 5){
                System.out.println("You lose. \nThe actual word was " + actualWord + ".");
            }
        }
    }
}
/* Cases that I used to test, and it worked properly:
gamer
Didn't work when I set begin as word and my last guess was menge
 */
 
