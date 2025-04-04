+++
title = "Online Sudoku Game, Generator and Solver"
url = "sudoku"
summary = "Full-Stack WEB Application Using LAMP stack"
author = "silviafesta2"
draft = false
hero_thumb = "/images/sudoku-logo.png"
hero_thumb_height = 250       # Altezza visibile in pixel
hero_thumb_offset_y = 220
tags = ["università di pisa","web design"]
featured = true
+++
# Introduction
This project is a comprehensive web application built upon the LAMP stack (Linux, Apache, MySQL, PHP), enabling users to play, generate, and solve Sudoku puzzles interactively online. It leverages a dynamic approach to Sudoku puzzle generation, ensuring uniqueness and varied difficulty levels through advanced Sudoku-solving logic.

The platform provides 3 different game modes:
1. **Training**: a User select a puzzle of his choice
2. **Time Challenge**: a User is challenged to solve a sudoku within a certain time limit.
3. **Generate Sudoku**: a completely new puzzle is generated through a backtrace approach mixed with classical and advanced rules application. The puzzle is generated in such a way that it respects User's level

# System Architecture
The application follows a traditional LAMP stack architecture:
- Linux: Server operating system providing the environment.
- Apache: HTTP server responsible for handling client requests and serving web content.
- MySQL: Database management system handling persistent data storage.
- PHP: Server-side scripting language managing business logic and dynamic content generation.

{{< figure src="/images/LAMP.png" width="300" >}}


# Database Management
The database schema supports multiple functionalities:
- Users: Stores user accounts, credentials (secured using salted hashes), and game preferences.
- Sudoku Puzzles: Maintains pre-generated classic puzzles with guaranteed uniqueness and dynamically generated puzzles.
- Game Sessions: Tracks ongoing and past games, user statistics, and interactions.

# User Interface
The web interface provides intuitive interaction for users:
- Mouse Interaction: Users can select Sudoku cells directly with mouse clicks.
- Keyboard Input: Optimized for users preferring keyboard navigation and numeric inputs.
- Dynamic Feedback: Immediate validation of inputs and puzzle progression.
  
The interface is responsive, allowing comfortable gameplay across different devices and screen sizes.

# Gameplay and User management
Users have personalized experiences:
- Profile Management: User-specific settings, saved games, and favorite puzzles. Users can also advance in level
- Statistics and Community: Comprehensive tracking of user performance, game history, and community interactions.

# Sudoku Puzzle Handling
There are two main types of Sudoku puzzles in the system:

## Classic Puzzles
These puzzles are sourced from established Sudoku collections, pre-validated for uniqueness of solution. The application supports transformations including:
1. Number permutations
2. Rotations
3. Reflections
These transformations greatly expand puzzle variety without compromising the uniqueness of the solutions.

## Dynamically Generated Puzzles
Dynamic puzzle generation is achieved through iterative application of Sudoku-solving rules:
- Initially, an incomplete Sudoku board is generated.
- The solver applies classical Sudoku logic iteratively, including simple rules (single possibilities, row/column/box constraints) and advanced techniques (hidden pairs/triples, intersection removals).
- If the solver cannot resolve the puzzle uniquely using rule-based approaches, an additional number is placed strategically, and the solving process is repeated.
- Should the puzzle generation fail (no solutions or multiple solutions), the puzzle generation restarts completely with a new initial board.

Auxiliary data structures comprehend arrays 9x9x9 for every cell and arrays for every row, column and block in order to store are the possiblities for each specific cell.

{{< figure src="/images/generate1.png" width="400" >}}
  
Here is a representative snippet illustrating the Sudoku-solving algorithm:
  
```php
function risolvi_sudoku(&$schema){

    // Find the first empty cell
    $coordinate_primo_vuoto = trova_prima_casella_libera($schema);
    if(!$coordinate_primo_vuoto){
        return true; // Puzzle fully solved
    }

    // Coordinates of the first empty cell
    $x_primo_vuoto = $coordinate_primo_vuoto[0];
    $y_primo_vuoto = $coordinate_primo_vuoto[1];

    // Possible Sudoku digits
    $cifre_sudoku = [1,2,3,4,5,6,7,8,9];
    shuffle($cifre_sudoku); // Randomize digits to attempt diverse solutions

    // Try inserting each digit in the empty cell
    foreach($cifre_sudoku as $num){
        if(numero_inseribile($num, $schema, $x_primo_vuoto, $y_primo_vuoto)){
            // Insert number if valid according to Sudoku rules
            $schema[$x_primo_vuoto * NUM + $y_primo_vuoto] = $num;

            // Recursively attempt to solve the puzzle with the new number added
            if(risolvi_sudoku($schema)){
                return true;
            }
            // Reset the cell if no solution is found
            $schema[$x_primo_vuoto*NUM + $y_primo_vuoto] = -1;
        }
    }
    // Backtrack if no digit is suitable for this cell
    return false;
}
```


In this case the function `numero_inseribile()` checks, if by applying classical rules, from easy checks on rows and columns to more advanced techniques like hidden pairs/triplets


# Future Improvements
- Enhance Sudoku-solving algorithm with heuristic approaches or probabilistic methods.
- Integration of AI-driven puzzle generation for more diverse puzzle difficulties.
- Development of a competitive multiplayer Sudoku tournament system.


# Conclusion
This documentation provides an extensive overview and understanding of the Sudoku Web Application project, its internal mechanisms, and the user experience delivered through meticulous design and engineering.