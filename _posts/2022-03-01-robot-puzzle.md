---
title: "Robot Puzzle"
layout: post
categories: University
---

![RobotPuzzle_Thumbnail](/assets/img/robot-puzzle/Screenshot_1.png){: width="50%" }


## Summary

Project written in Python for one of the Artificial Intelligence assignments. The task was to program a simple heuristic function to guide a robot through a few user-defined levels.

In my interpretation, the robot starts in room 0 and has to put all items in their corresponding rooms in the fewest moves possible. Each action counts as a move - pick up an item, drop an item, open a door, move to another room etc. The puzzle was made harder by locking some of the pathways. The robot needs to first unlock a door to access any rooms behind it. Each item has a weight value assigned to it - the robot was only allowed to carry a fixed weight at any time. To introduce more confusion, I added some useless items which do not contribute to the solution.

I decided to put in extra work and implemented a procedural level generator as well as a machine-learning-based heuristic function which allowed the robot to solve even very difficult scenarios. I utilised the concept of parallel programming for evaluating the performance and tweaking the parameters of the solver.

I found it especially interesting to work on a recursive key placement function for the level generator - every room needed to be accessible by the robot:

```python
# helper function used when placing keys; it randomly traverses n rooms and returns (resultant room, bypassed locked doors list)
def traverse_random(start_room, doors, n, doors_not_to_use):
    result = start_room
    locked_doors_bypassed = list()
    went_through = list()  # ensures no going backwards
    for _ in range(n):
        choices = find_doors_for_room(result, doors, doors_not_to_use + went_through)
        locked_choices = [x for x in choices if x.locked]
        if len(choices) > 0:
            # prioritize going through locked doors
            choice = choices[randint(0, len(choices) - 1)] if len(locked_choices) == 0 else locked_choices[
                randint(0, len(locked_choices) - 1)]
            went_through.append(choice)
            if choice.locked:
                locked_doors_bypassed.append(choice)
            result = choice.other_loc[result]
        else:
            return result, locked_doors_bypassed

    return result, locked_doors_bypassed


# recursively places keys (at least 1) so that all the rooms locked by these keys can be accessed
# modifies keys_already_placed on the go
def place(key, door, start_room, doors, n, room_contents, keys_already_placed=list(), doors_not_to_use=list()):
    if len(doors_not_to_use) == 0:
        doors_not_to_use = [door]

    room, bypassed_doors = traverse_random(start_room, doors, n, doors_not_to_use)

    if room not in room_contents:
        room_contents[room] = list()
    room_contents[room].append(key)
    keys_already_placed.append(key)

    for bypassed_door in bypassed_doors[::-1]:
        doors_not_to_use.append(bypassed_door)

        if bypassed_door.doorkey in keys_already_placed:
            continue

        place(bypassed_door.doorkey, bypassed_door, start_room, doors, n, room_contents, keys_already_placed,
              doors_not_to_use)


def generate(robot_capacity, rooms_count, additional_doors_count, locked_doors_count,
             goal_items_count, useless_items_count, max_item_weight, visualise=False, save=True, file_name='level'):
    # ...

    # place all keys in rooms randomly but the puzzle will still remain solvable
    not_placed = list(keys.keys())
    placed = list()
    while len(not_placed) > 0:
        place(not_placed[0], keys[not_placed[0]], 'Room 0', doors, rooms_count - 1, room_contents, placed)
        not_placed = [x for x in not_placed if x not in placed]

    # ...
```

More details about the project can be found in the submission [document](https://gitlab.com/Pawel_Wilczewski/comp2611cwk1/-/blob/main/comp2611cwk1%20robot.pdf).

## Gallery

![RobotPuzzle_Screenshot_1](/assets/img/robot-puzzle/diagram.png)

![RobotPuzzle_Screenshot_3](/assets/img/robot-puzzle/Screenshot_2.png)
*It takes the robot 50 moves on average to solve this level - a 100% success rate*

![RobotPuzzle_Screenshot_4](/assets/img/robot-puzzle/Screenshot_3.png)
*80 moves on average with an 84% solution success rate*
