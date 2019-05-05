# PiMaze: Teaching Programming through Tangible Interfaces
## ESTEeM 2019

This handout is also available online at <https://github.com/5uperdan/maze-esteem2019>

In this workshop we will introduce you to the python programming language and use it to develop maze solving algorithms.

## How the activity works

- A maze is represented on the 32x32 LED grid.
- Walls are shown in red.
- Your player is shown in green, but you can change the colour if you choose.
- The direction your player is facing is shown in blue.
- Your player is green, but you may change the colour of your player.
- The goal is to escape the maze by moving your player to the exit.
- You might find it helpful to write code in your favourite code/ text editor and then paste it into the activity's webpage.

## Useful basic python syntax

### Comments

```Python
"""
Single or multiple line comments
can be between quotation marks
"""
# Single line comments can be written after a hash (#)
```

### Imports

```Python
# Import functions from the mazectl module
# helps us send commands to the maze
from mazectl import start_esteem, move_forward, turn_left, turn_right, get_position, start_random
```

### Load a maze

```Python
# functions are called by using their name
# followed by brackets that contain arguments.
# 1 corresponds to the id of the maze we want to load
start_esteem(1)
```

### Set Player Colour

You can change your player's colour on the maze and set it to any valid rgb colour, where r, g & b values are in the range 0-255.

```Python
# sets player's colour to white
set_player_colour(255, 255, 255)
```

### Get your player's location in the maze

```Python
# assign the value 5 to the variable x
x = 5
```

Functions can also return values that can be assigned to variables

```Python
# not a real function
apples = count_apples()
```

```Python
# the get_position function returns 4 values
success, x, y, heading = get_position()
```

- x and y are integers that represent your player's position
- heading (N, E, S or W)

### Move your player

```Python
# move, turn and get_position functions return the same 4 values
success, x, y, heading = move_forwards()
```

The first value returned by move_forwards(), stored in the value _success_ in our examples, is True if your player is able to move forwards and False if your player's path forwards is blocked by a wall. _success_ is always true from turn and get_position functions (because they're always successful).

```Python
# move, turn and get_position functions return the same 4 values
success, x, y, heading = get_position()
success, x, y, heading = turn_left()
success, x, y, heading = move_forwards()
```

### Python while loops

With the while loop we can execute a set of statements as long as a condition is true.

```Python
# this loop would keep your player turning right forever
success, x, y, heading = get_position()
while success:
    success, x, y, heading = turn_left()
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

Examples:

```Python
success, x, y, heading = get_position()
# while player is not blocked from moving forwards
# and their x coordinate is less than 5
# continue moving forward
while success and x < 5:
    success, x, y, heading = move_forward()

```

```Python
success, x, y, heading = get_position()
# turn player until they face either east or west
while heading != 'E' or heading != 'W':
    success, x, y, heading = turn_right()
```

### Underscore ###

It's not necessary to use it, but if you're not interested in all the values returned by a function then it's customary to assign the ones you're not interested in to _ (underscore).

```Python
# the first value (success) is always true when turning
# x will be unchanged when turning
# y will be unchanged when turning
# the only value that will have changed is the player's heading
_, _, _, heading = turn_right()
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
success, x, y, heading = get_position()

# move forwards until the move attempt is blocked by a wall
while success:
    success, x, y, heading = move_forward()

# turn 180°
_, _, _, heading = turn_right()
_, _, _, heading = turn_right()

# move forward until the player is back where they started
while (x is not start_x) and (y is not start_y):
    _, x, y, heading = move_forward()

# turn until the player's heading is the same as it started
while heading is not start_heading:
    _, _, _, heading = turn_left()

```

## Getting started

Each pi maze setup runs its own wireless network. Connect a wireless device to get started and navigate to <http://192.168.4.1:8000/python/>. Note that you will lose internet access when you connect the raspberry pi.

## The Activity

- Danny will introduce the handout.
- Participants will be given some time to work through the mazes.
- (optional: participants may explore other maze features, like _start\_random_)
- Feedback/ discussion/ comments.
