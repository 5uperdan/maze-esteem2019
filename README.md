# PiMaze: Teaching Programming through Tangible Interfaces
## ESTEeM 2019

This handout is also available online at <https://github.com/5uperdan/maze-esteem2019>

In this workshop we will introduce you to the python programming language and use it to develop maze solving algorithms.

- A maze is represented on the 32x32 LED grid.
- Walls are shown in red.
- Your player is shown in green, but you can change the colour if you choose.
- The direction your player is facing is shown in blue.
- Your player is green, but you may change the colour of your player.
- The goal is to escape the maze by moving your player to the exit.
- You might find it helpful to write code in your favourite code/ text editor and then paste it into the activity's webpage.

## Useful Python

## Comments

```Python
"""
Single or multiple line comments
can be between quotation marks
"""
# Single line comments can be written after a hash (#)
```

## Imports

```Python
# Import functions from the mazectl module
# helps us send commands to the maze
from mazectl import start_esteem, move_forward, turn_left, turn_right, get_position, start_random
```

## Load a maze

```Python
# functions are called by using their name
# followed by brackets that contain arguments.
# 1 corresponds to the id of the maze we want to load
start_esteem(1)
```

## Set Player Colour

You can change your player's colour on the maze and set it to any valid rgb colour, where r, g & b values are in the range 0-255.

```Python
set_player_colour(255, 255, 255)  # white
set_player_colour(255, 0, 0)  # red
set_player_colour(0, 255, 0)  # green
set_player_colour(0, 0, 255)  # blue
```

## Variable Assignment

```Python
# assign the value 5 to the variable x
x = 5
```

Functions can also return values that can be assigned to variables

```Python
# not a real function
apples = count_apples()
```

## Print

This can be useful for debugging. The result of print statements will be output just below your code window.

```Python
success, x, y, heading, victory = get_position()
print(success)  # you can print the value of a variable
print(x, y)  # you can print the values of multiple variables
print(get_position())  # you can print the values returned by a function
```

## Get your player's location in the maze

```Python
# the get_position function returns 5 values
success, x, y, heading, victory = get_position()
```

- success is a boolean (True/ False) that indicates if the function was completed successfully
- x and y are integers that represent your player's position
- heading (N, E, S or W)
- victory is a boolean that is True when the the player has escaped the maze

### Move your player

```Python
# all maze control functions return the same 5 values
success, x, y, heading, victory = move_forward()
```

The first value returned by move_forward(), stored in the value _success_ in our examples, is True if your player is able to move forwards and False if your player's path forwards is blocked by a wall. _success_ is always true from turn and get_position functions (because they're always successful).

```Python
# all maze control functions return the same 5 values
success, x, y, heading, victory = get_position()
success, x, y, heading, victory = turn_left()
success, x, y, heading, victory = turn_right()
success, x, y, heading, victory = move_forward()
```

### Python while loops

With the while loop we can execute a set of statements as long as a condition is equal to _True_.

```Python
# this loop would keep your player turning right forever
success, x, y, heading, victory = get_position()
while success is True:
    success, x, y, heading, victory = turn_left()
```

```Python
# this is the same as above
success, x, y, heading, victory = get_position()
while success:
    success, x, y, heading, victory = turn_left()
```

```Python
# if you want to do something 5 times
count = 0
while count < 5:
    move_forward()
    count = count + 1
```

- It's important to notice that commands that are repeated by the while clause are indented compared to the while clause. You can do this with the space bar or using the tab key.

### And/ Or/ Not/ ==/ !=/ </>

You may find some of these terms helpful in creating _while_ clauses.

    Equals: a == b
    Not Equals: a != b
    Less than: a < b
    Less than or equal to: a <= b
    Greater than: a > b
    Greater than or equal to: a >= b

### Examples

```Python
success, x, y, heading, victory = get_position()
# while player is not blocked from moving forwards
# and their x coordinate is less than 5
# continue moving forward
while success and x < 5:
    success, x, y, heading, victory = move_forward()

```

```Python
success, x, y, heading, victory = get_position()
# turn player until they face either east or west
while heading != 'E' or heading != 'W':
    success, x, y, heading, victory = turn_right()
```

```Python
success, x, y, heading, victory = get_position()
# while facing south move forwards until the maze is complete 
while victory == False and heading == 'S':
    success, x, y, heading, victory = move_forward()
```

### Underscore ###

It's not necessary to use it, but if you're not interested in all the values returned by a function then it's customary to assign the ones you're not interested in to _ (underscore).

```Python
# the first value (success) is always true when turning
# x will be unchanged when turning
# y will be unchanged when turning
# the only value that will have changed is the player's heading
_, _, _, heading, _ = turn_right()
```

### Bringing everything together

```Python
"""
This script will move your player forward until the way is blocked.
Then your player will turn around and move back to its starting location.
Finally, your player will turn around to face the same way they were
facing at the start.
"""

from mazectl import start_esteem, move_forward, turn_left, turn_right, get_position, start_random

# generates a random maze
start_random()

# get the player's starting information
success, start_x, start_y, heading, victory = get_position()

# move forwards until the move attempt is blocked by a wall
while success and not victory:
    success, x, y, heading, victory = move_forward()

# turn 180°
_, _, _, heading, _ = turn_right()
_, _, _, heading, _ = turn_right()

# move forward until the player is back where they started
while (x is not start_x) and (y is not start_y):
    _, x, y, heading, _ = move_forward()

# turn until the player's heading is the same as it started
while heading is not start_heading:
    _, _, _, heading, _ = turn_left()

```

## Getting Started

Each pi maze setup runs its own wireless network. The passphrase is onetwothree and the networks are amazingpi#.
Connect a wireless device to get started and navigate to <http://192.168.4.1:8000/python/>. There are additional notes at the top of that page.
Note that you will lose internet access when you connect the raspberry pi.

Try and write a script that can complete the first maze. After the import lines, start your script with

```Python
# start the first esteem maze
start_esteem(1)

# get starting position
success, x, y, heading, victory = get_position()
while victory == False:
    # do something here
```

Once you have completed the first maze, try replacing start_esteem(1) with start_esteem(2) and run your script again.
There are four mazes in total to complete and you will likely have to modify your script each time to tackle new challenges.

- (optional: participants may explore other maze features, like _start\_random_ to see if their script can beat randomly generated mazes).

- Please feel free to give your feedback or comments as we go.

## Limitations - probably not important

There are some limitations to prevent you from breaking the mazes.

- The scripts can take no longer than roughly 20 seconds to execute in the browser.
- A single scripts can only generate 1000 maze updates (after this, some will be ignored).
- Roughly 2000 maze related function calls from a python script in any minute.
