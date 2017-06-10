# Artificial Intelligence Nanodegree
## Introductory Project: Diagonal Sudoku Solver

# Question 1 (Naked Twins)
Q: How do we use constraint propagation to solve the naked twins problem?  
A: In order to solve the problem of naked twins, I built the following algorithm.

    # for all values
    for value in values:
        # for all units which typical value belong to
        for unit in units[value]:
            # for all boxes which typical unit of typical value belong to
            for box in unit:
                # To get the value of typical box
                v_box = values[box]

                # To get the values of typical unit which the box belong to
                v_unit = [values[box] for box in unit]

                # To get the boxes which is the same as the typical box
                indexes = [unit[i] for i, x in enumerate(v_unit) if x == v_box]

                # We judge from the length of the value whether naked twin constraints can be applied.
                if len(indexes) > 1 and len(indexes) >= len(v_box):
                    # for all box in unit
                    for box in unit:
                        # if the box is already known as the twins, then continue
                        if box in indexes:
                            continue
                        # if not
                        else:
                            # if the length is 1, then the box doesn't need to eliminate
                            if len(values[box]) == 1:
                                continue
                            # if not, check each value in box to be able to eliminate
                            else:
                                # for all value in the box, replace value in box to null when the box has the value
                                for str in v_box:
                                    values[box] = values[box].replace(str, "")



# Question 2 (Diagonal Sudoku)
Q: How do we use constraint propagation to solve the diagonal sudoku problem?  
A: I added diagonal units to solve the diagonal sudoku problem.
Then I solved this problem in the same way as solving a simple sudoku problem.
Specifically, we first applied eliminate, picked out an impossible value from units already given values, and removed it from the box's options that have not yet been decided.
Next, only_choice was applied, and the place where the value was determined among each unit was filled with that value.
Finally, applying naked_twins to select a numerical value that can eliminate the value of other boxes, the value is not uniquely determined, and the value was excluded from the choices of other boxes.
In diagonal sudoku, after adding diagonal units, we solved the problem using this algorithm.

### Install

This project requires **Python 3**.

We recommend students install [Anaconda](https://www.continuum.io/downloads), a pre-packaged Python distribution that contains all of the necessary libraries and software for this project. 
Please try using the environment we provided in the Anaconda lesson of the Nanodegree.

##### Optional: Pygame

Optionally, you can also install pygame if you want to see your visualization. If you've followed our instructions for setting up our conda environment, you should be all set.

If not, please see how to download pygame [here](http://www.pygame.org/download.shtml).

### Code

* `solution.py` - You'll fill this in as part of your solution.
* `solution_test.py` - Do not modify this. You can test your solution by running `python solution_test.py`.
* `PySudoku.py` - Do not modify this. This is code for visualizing your solution.
* `visualize.py` - Do not modify this. This is code for visualizing your solution.

### Visualizing

To visualize your solution, please only assign values to the values_dict using the ```assign_values``` function provided in solution.py

### Submission
Before submitting your solution to a reviewer, you are required to submit your project to Udacity's Project Assistant, which will provide some initial feedback.  

The setup is simple.  If you have not installed the client tool already, then you may do so with the command `pip install udacity-pa`.  

To submit your code to the project assistant, run `udacity submit` from within the top-level directory of this project.  You will be prompted for a username and password.  If you login using google or facebook, visit [this link](https://project-assistant.udacity.com/auth_tokens/jwt_login) for alternate login instructions.

This process will create a zipfile in your top-level directory named sudoku-<id>.zip.  This is the file that you should submit to the Udacity reviews system.

