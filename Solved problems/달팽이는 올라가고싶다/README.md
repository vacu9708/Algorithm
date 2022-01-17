# Baekjoon 2869. 달팽이는 올라가고 싶다
* distance_in_daytime : The distance that the snail climbed in daytime
* distance_of_night : The distance that the snail slided at night
* day: Days taken to reach the top

~~~python
import sys
import math

# Enter 3 variables : distance_in_daytime, distance_at_night, height_of_tree
distance_in_daytime, distance_at_night, height_of_tree = map(int, sys.stdin.readline().split())
#-----
delta = distance_in_daytime - distance_at_night
day = (height_of_tree - distance_at_night) / delta # subtract distance_at_night because the snail doesn't slide once it has reached the top
print(math.ceil(day))

''' Inefficient code
def solution(distance_in_daytime, distance_at_night, height_of_tree):
    if distance_in_daytime >= height_of_tree: # Arriving without sliding
        return 1 # 1 day taken

    delta = distance_in_daytime - distance_at_night
    day = (height_of_tree - distance_in_daytime) // delta
    if (height_of_tree - distance_in_daytime) % delta == 0:
        return day + 1
    else:
        return day + 2

distance_in_daytime, distance_at_night, height_of_tree = map(int, sys.stdin.readline().split())
print(solution(distance_in_daytime, distance_at_night, height_of_tree))
'''
~~~
## Input
distance_in_daytime, distance_at_night, height_of_tree

## Output
Days taken to reach the top
