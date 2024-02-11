## Overview

The algorithm computes the number of intersections among chords within a circle. It is based on the [Bentley–Ottmann algorithm](https://en.wikipedia.org/wiki/Bentley%E2%80%93Ottmann_algorithm).However, it was modifyed to handle the geometry of the circle (original algorithm is used for line segments on cartesian plane.)
The code also includes visualization, edge test cases, generation of test cases and experimental proof of the runtime estimation using simulation. 

### Key Steps

1. **Preprocessing**: Converts input radians and identifiers into a structured representation of each chord's start and end points.

2. **Sweep Line Simulation**: Conceptually moves a sweep line along the circle's circumference, maintaining an active set of chords and updating it as their endpoints are encountered.

3. **Intersection Detection**: Checks for intersections between a newly added chord and its immediate neighbors in the active set.


### Requirements 
You will need sortedcontainers Python package to run the code.
    ```bash
    pip install sortedcontainers

I am using SortedDict from sortedcontainers for this assignmnet. 
This is a dictionary-like data structure that maintains its keys in sorted order. It offers similar functionality to Python's built-in dictionary, but with the added benefit of keeping keys sorted. 
It is implemented using a combination of a binary search tree and an array so the time complexities for inserting, search and deleting and element are O(logn) 
   

## Big-O Estimation
The estimated time complexity of this algorithm is O(n^2), where n is the number of chord endpoints (or, equivalently, half the number of total input elements since each chord has two endpoints).

### Key Factors:
Preprocessing (Step 1) -> O(n)
Unpacking the input data and extracting 's' or 'e' and the radian value for each chord involves iterating over each element in the input data takes O(n) time, where n is the number of chord endpoints.

Counting Intersections (Step 2) -> n^2
Iterating over each event in the sorted events list takes O(n) time.
inserting start of the chord in the SortedDict is O(logn) due to binary tree logic under the hood. 
Same applies for deleting the element from the SortedDict once we got to the end point of the chord as we sweep the circle. It will be O(logn)
The bottleneck lies in the intersection check loop when we traversed a circle with the imaginative plane from the start point of the chord till the end point. 
This loop iterates over each start point of all the active chords (those chords which end points we did not encounter yet) and checks if it forms an intersection with the current chord examined (the one that just ended). 
Since this loop runs over all currently active chords for each 'end' chord, in the worst case, this leads to a nested loop scenario, resulting in O(n^2) time complexity.
Therefore, the overall time complexity of the counting intersections step is O(n^2), due to the intersection check bottleneck.

Overall, considering both preprocessing and counting intersections, the code's time complexity is dominated by the O(n^2) complexity of the intersection check loop.

I have tried numerous imlementations for reducing the time complexity of the bottle neck part, mainly using geometrical properties of the lines/circle. I managed to achieve nlogn solution but it did not manage to undergo more sophisticated tests which is why I decided to prioritize quality solution over speed. 

