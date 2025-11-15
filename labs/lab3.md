# University of Guyana
## Faculty of Natural Sciences
### Department of Computer Science
#### CSE 4101 – Artificial Intelligence I
##### Lab Exercise: Informed Search Algorithms

---

#### **Instructions**
Answer all questions. For Questions 1-2, provide detailed written responses showing your problem formulations and analysis. For Question 3, complete the Python code as instructed to implement informed search algorithms (A*, Greedy Best-First Search, and IDA*).

---

### **Question 1: Two Friends Meeting Problem (40 Marks)**

Suppose two friends live in different cities on a map, such as the Romania map. On every turn, we can simultaneously move each friend to a neighboring city on the map. The amount of time needed to move from city $i$ to neighbor $j$ is equal to the road distance $d(i,j)$ between the cities, but on each turn the friend that arrives first must wait until the other one arrives (and calls the first on his/her cell phone) before the next turn can begin. We want the two friends to meet as quickly as possible.

#### **Part 1.1: Problem Formulation (10 marks)**
Write a detailed formulation for this search problem. (You will find it helpful to define some formal notation here.)

*Provide a complete problem formulation including states, initial state, actions, transition model, goal test, and path cost. Use formal notation to clearly define your formulation.*

---

#### **Part 1.2: Heuristic Admissibility Analysis (10 marks)**
Let $D(i,j)$ be the straight-line distance between cities $i$ and $j$. Which of the following heuristic functions are admissible?

1. $h(n) = D(i,j)$ where $i$ and $j$ are the positions of the two friends
2. $h(n) = 2 \cdot D(i,j)$  
3. $h(n) = \frac{D(i,j)}{2}$

*For each heuristic, determine if it is admissible and provide a clear justification for your answer.*

---

#### **Part 1.3: Solution Existence (10 marks)**
Are there completely connected maps for which no solution exists?

*Analyze whether it's possible for no solution to exist in a completely connected map. Provide reasoning and examples if applicable.*

---

#### **Part 1.4: Revisiting Cities (10 marks)**
Are there maps in which all solutions require one friend to visit the same city twice?

*Consider whether there are map configurations where optimal solutions necessarily involve revisiting cities. Provide examples or counterexamples.*

---

### **Question 2: True or False Analysis (30 Marks)**

Which of the following are true and which are false? Explain your answers with detailed justification.

#### **2.1** (6 marks)
**Statement**: Depth-first search always expands at least as many nodes as A* search with an admissible heuristic.

**Answer**: True / False  
**Justification**: *Provide a detailed explanation with examples if needed.*

---

#### **2.2** (6 marks)
**Statement**: h(n) = 0 is an admissible heuristic for the 8-puzzle.

**Answer**: True / False  
**Justification**: *Explain why this is or isn't admissible, and discuss its practical utility.*

---

#### **2.3** (6 marks)
**Statement**: A* is of no use in robotics because percepts, states, and actions are continuous.

**Answer**: True / False  
**Justification**: *Discuss the relationship between continuous domains and A* search applicability.*

---

#### **2.4** (6 marks)
**Statement**: Breadth-first search is complete even if zero step costs are allowed.

**Answer**: True / False  
**Justification**: *Analyze BFS completeness when step costs can be zero.*

---

#### **2.5** (6 marks)
**Statement**: Assume that a rook can move on a chessboard any number of squares in a straight line, vertically or horizontally, but cannot jump over other pieces. Manhattan distance is an admissible heuristic for the problem of moving the rook from square A to square B in the smallest number of moves.

**Answer**: True / False  
**Justification**: *Consider the relationship between Manhattan distance and actual rook movement constraints.*

---

### **Question 3: Implementing Informed Search Algorithms (80 Marks)**

#### **Problem Description**
Implement **A* Search**, **Greedy Best-First Search**, and **Iterative Deepening A* (IDA*)** algorithms for pathfinding in a grid world with obstacles and varying terrain costs. 🎯

* The world is represented as a 2D grid with terrain costs and obstacles
* Different terrain types have different movement costs
* Algorithms should use appropriate heuristics (Manhattan distance, Euclidean distance)
* Compare performance and solution quality of different approaches

#### **Your Task**
Complete the Python implementations below for all three informed search algorithms. Your implementations should:
1. Use appropriate heuristics for pathfinding
2. Handle varying terrain costs correctly
3. Return optimal paths (for A*) or any valid paths (for Greedy)
4. Track performance metrics (nodes expanded, time taken)

---

### **Part 3.1: A* Search Implementation (30 Marks)**

```python
import heapq
import math
import time
from typing import List, Tuple, Optional, Dict, Set

class GridWorldInformed:
    """Enhanced grid world for informed search algorithms."""
    
    # Terrain cost mapping
    TERRAIN_COSTS = {
        0: 1.0,    # Normal terrain
        1: float('inf'),  # Wall (impassable)
        2: 3.0,    # Rough terrain
        3: 0.5,    # Highway
        4: 2.0,    # Hills
        'S': 1.0,  # Start
        'G': 1.0   # Goal
    }
    
    def __init__(self, grid: List[List]):
        """Initialize the grid world."""
        self.grid = grid
        self.rows = len(grid)
        self.cols = len(grid[0]) if grid else 0
        self.start = None
        self.goal = None
        
        # Find start and goal positions
        for i in range(self.rows):
            for j in range(self.cols):
                if grid[i][j] == 'S':
                    self.start = (i, j)
                elif grid[i][j] == 'G':
                    self.goal = (i, j)
    
    def get_neighbors(self, position: Tuple[int, int]) -> List[Tuple[int, int]]:
        """Get valid neighboring positions (8-directional movement)."""
        row, col = position
        neighbors = []
        
        # 8-directional movement (including diagonals)
        directions = [(-1, -1), (-1, 0), (-1, 1), (0, -1), 
                     (0, 1), (1, -1), (1, 0), (1, 1)]
        
        for dr, dc in directions:
            new_row, new_col = row + dr, col + dc
            new_pos = (new_row, new_col)
            
            if self.is_valid(new_pos):
                neighbors.append(new_pos)
        
        return neighbors
    
    def is_valid(self, position: Tuple[int, int]) -> bool:
        """Check if a position is valid."""
        row, col = position
        
        if row < 0 or row >= self.rows or col < 0 or col >= self.cols:
            return False
        
        return self.grid[row][col] != 1  # Not a wall
    
    def get_cost(self, position: Tuple[int, int]) -> float:
        """Get the cost of entering a position."""
        row, col = position
        if not self.is_valid(position):
            return float('inf')
        
        terrain = self.grid[row][col]
        return self.TERRAIN_COSTS.get(terrain, 1.0)
    
    def manhattan_distance(self, pos1: Tuple[int, int], pos2: Tuple[int, int]) -> float:
        """Calculate Manhattan distance between two positions."""
        # === YOUR CODE GOES HERE ===
        pass
        # ===========================
    
    def euclidean_distance(self, pos1: Tuple[int, int], pos2: Tuple[int, int]) -> float:
        """Calculate Euclidean distance between two positions."""
        # === YOUR CODE GOES HERE ===
        pass
        # ===========================
    
    def diagonal_distance(self, pos1: Tuple[int, int], pos2: Tuple[int, int]) -> float:
        """Calculate diagonal distance (Chebyshev distance)."""
        # === YOUR CODE GOES HERE ===
        # Useful for 8-directional movement
        pass
        # ===========================


def a_star_search(grid_world: GridWorldInformed, heuristic_type: str = 'manhattan') -> Tuple[Optional[List], float, Dict]:
    """
    Implement A* search algorithm.
    
    Args:
        grid_world: The grid world to search
        heuristic_type: Type of heuristic ('manhattan', 'euclidean', 'diagonal')
        
    Returns:
        tuple: (path, cost, stats) where stats contains performance metrics
    """
    # === YOUR CODE GOES HERE ===
    # Initialize:
    # - Priority queue with (f_score, g_score, position)
    # - g_score dictionary (cost from start)
    # - f_score dictionary (g_score + heuristic)
    # - parent dictionary for path reconstruction
    # - closed set for explored nodes
    # - performance statistics
    
    # Choose heuristic function based on heuristic_type
    
    # A* main loop:
    # While frontier not empty:
    #   - Pop node with lowest f_score
    #   - If goal reached, reconstruct path
    #   - Add to closed set
    #   - For each neighbor:
    #     - Calculate tentative g_score
    #     - If better path found, update scores and parent
    #     - Add to frontier if not in closed set
    
    # Return path, cost, and statistics
    
    pass
    # ===========================


def reconstruct_path(parent: Dict, start: Tuple[int, int], goal: Tuple[int, int]) -> List[Tuple[int, int]]:
    """Reconstruct path from parent dictionary."""
    # === YOUR CODE GOES HERE ===
    pass
    # ===========================
```

---

### **Part 3.2: Greedy Best-First Search Implementation (25 Marks)**

```python
def greedy_best_first_search(grid_world: GridWorldInformed, heuristic_type: str = 'manhattan') -> Tuple[Optional[List], float, Dict]:
    """
    Implement Greedy Best-First Search algorithm.
    
    Args:
        grid_world: The grid world to search
        heuristic_type: Type of heuristic to use
        
    Returns:
        tuple: (path, cost, stats) where stats contains performance metrics
    """
    # === YOUR CODE GOES HERE ===
    # Similar to A* but only uses heuristic (h_score) for node ordering
    # Priority queue with (h_score, position)
    # 
    # Key difference from A*:
    # - Only considers heuristic for node expansion order
    # - Does not guarantee optimal solution
    # - Usually faster but may find suboptimal paths
    
    # Initialize:
    # - Priority queue with (h_score, position)
    # - visited set
    # - parent dictionary
    # - performance statistics
    
    # Greedy main loop:
    # While frontier not empty:
    #   - Pop node with lowest h_score
    #   - If goal, reconstruct path
    #   - Mark as visited
    #   - Add unvisited neighbors to frontier
    
    pass
    # ===========================
```

---

### **Part 3.3: Iterative Deepening A* (IDA*) Implementation (25 Marks)**

```python
def ida_star_search(grid_world: GridWorldInformed, heuristic_type: str = 'manhattan') -> Tuple[Optional[List], float, Dict]:
    """
    Implement Iterative Deepening A* (IDA*) algorithm.
    
    Args:
        grid_world: The grid world to search
        heuristic_type: Type of heuristic to use
        
    Returns:
        tuple: (path, cost, stats) where stats contains performance metrics
    """
    def search_recursive(node: Tuple[int, int], g_score: float, threshold: float, 
                        path: List, visited: Set) -> Tuple[str, float, Optional[List]]:
        """
        Recursive helper function for IDA*.
        
        Returns:
            tuple: (status, min_threshold, path)
            status: 'FOUND', 'NOT_FOUND', or 'THRESHOLD'
        """
        # === YOUR CODE GOES HERE ===
        # Calculate f_score = g_score + heuristic
        # If f_score > threshold, return 'THRESHOLD' with new minimum
        # If goal reached, return 'FOUND' with path
        # If already visited, return 'NOT_FOUND'
        # 
        # For each neighbor:
        #   - Calculate new g_score
        #   - Recursively search with updated path and g_score
        #   - Handle different return statuses appropriately
        
        pass
        # ===========================
    
    # === YOUR CODE GOES HERE ===
    # Main IDA* algorithm:
    # 
    # Initialize threshold with heuristic from start to goal
    # Repeat until solution found or threshold becomes infinite:
    #   - Perform depth-limited search with current threshold
    #   - If solution found, return it
    #   - If not found, increase threshold to next minimum f-value encountered
    #   - Track performance statistics
    
    pass
    # ===========================
```

---

### **Part 3.4: Algorithm Comparison and Testing (Bonus 10 Marks)**

```python
def compare_search_algorithms(grid_world: GridWorldInformed) -> None:
    """Compare all three search algorithms on the same problem."""
    
    print(f"\n{'='*80}")
    print(f"SEARCH ALGORITHM COMPARISON")
    print(f"{'='*80}")
    print(f"Grid Size: {grid_world.rows}×{grid_world.cols}")
    print(f"Start: {grid_world.start}, Goal: {grid_world.goal}")
    
    algorithms = [
        ("A* (Manhattan)", lambda: a_star_search(grid_world, 'manhattan')),
        ("A* (Euclidean)", lambda: a_star_search(grid_world, 'euclidean')),
        ("A* (Diagonal)", lambda: a_star_search(grid_world, 'diagonal')),
        ("Greedy BFS (Manhattan)", lambda: greedy_best_first_search(grid_world, 'manhattan')),
        ("Greedy BFS (Euclidean)", lambda: greedy_best_first_search(grid_world, 'euclidean')),
        ("IDA* (Manhattan)", lambda: ida_star_search(grid_world, 'manhattan')),
    ]
    
    results = []
    
    for name, algorithm in algorithms:
        print(f"\nRunning {name}...")
        start_time = time.time()
        path, cost, stats = algorithm()
        end_time = time.time()
        
        result = {
            'name': name,
            'path': path,
            'cost': cost,
            'time': end_time - start_time,
            'stats': stats
        }
        results.append(result)
        
        if path:
            print(f"  ✓ Solution found!")
            print(f"    Path length: {len(path)} steps")
            print(f"    Path cost: {cost:.2f}")
            print(f"    Nodes expanded: {stats.get('nodes_expanded', 'N/A')}")
            print(f"    Time: {result['time']:.4f}s")
        else:
            print(f"  ✗ No solution found")
    
    # === YOUR CODE GOES HERE (BONUS) ===
    # Create a comprehensive comparison table
    # Analyze which algorithm performs best in different scenarios
    # Discuss optimality vs. efficiency trade-offs
    
    pass
    # ===========================


def visualize_search_path(grid_world: GridWorldInformed, path: List[Tuple[int, int]], 
                         algorithm_name: str) -> None:
    """Visualize the search path on the grid."""
    
    # === YOUR CODE GOES HERE (BONUS) ===
    # Create a visual representation of the grid with the path
    # Use different symbols for different terrain types
    # Mark the path clearly
    # Include legend for symbols
    
    pass
    # ===========================


# Test cases
if __name__ == "__main__":
    # Test Grid 1: Simple maze with mixed terrain
    test_grid_1 = [
        ['S', 0, 2, 0, 3],
        [1, 0, 2, 0, 3],
        [4, 0, 0, 0, 3],
        [4, 1, 1, 0, 0],
        [0, 0, 0, 0, 'G']
    ]
    
    # Test Grid 2: Complex terrain
    test_grid_2 = [
        ['S', 2, 2, 3, 3, 3, 0],
        [0, 2, 1, 1, 1, 3, 0],
        [0, 2, 4, 4, 1, 3, 0],
        [0, 0, 4, 0, 0, 3, 0],
        [1, 1, 1, 0, 2, 2, 0],
        [0, 0, 0, 0, 2, 1, 0],
        [0, 4, 4, 0, 0, 0, 'G']
    ]
    
    # Test Grid 3: Challenging pathfinding
    test_grid_3 = [
        ['S', 1, 1, 1, 1, 1, 1, 1],
        [0, 1, 0, 0, 0, 0, 0, 1],
        [3, 1, 0, 1, 1, 1, 0, 1],
        [3, 1, 0, 1, 2, 1, 0, 1],
        [3, 1, 0, 1, 2, 1, 0, 1],
        [3, 1, 0, 1, 2, 1, 0, 1],
        [3, 0, 0, 1, 2, 0, 0, 1],
        [1, 1, 1, 1, 1, 1, 1, 'G']
    ]
    
    test_grids = [test_grid_1, test_grid_2, test_grid_3]
    
    for i, grid in enumerate(test_grids, 1):
        print(f"\n{'='*80}")
        print(f"TEST CASE {i}")
        print(f"{'='*80}")
        
        world = GridWorldInformed(grid)
        compare_search_algorithms(world)
```

---

#### **Analysis Questions**

After implementing and testing your algorithms, answer the following:

1. **Heuristic Comparison**: Which heuristic works best for 8-directional movement? Why?

2. **Optimality vs. Speed**: Compare A* and Greedy Best-First Search in terms of:
   - Solution quality (path cost)
   - Computational efficiency (nodes expanded, time)
   - When would you choose one over the other?

3. **IDA* Performance**: How does IDA* compare to A* in terms of:
   - Memory usage
   - Time complexity
   - When is IDA* preferred over A*?

4. **Heuristic Admissibility**: 
   - Verify that your heuristics are admissible for the given problem
   - What happens if you use a non-admissible heuristic?
   - Design a non-admissible heuristic and test its effect on optimality

5. **Real-world Applications**: Give three examples of real-world problems where each algorithm (A*, Greedy, IDA*) would be most appropriate.

---

#### **Submission Guidelines**
1. Submit your written responses for Questions 1-2 in a PDF document
2. Submit your Python code file with all implementations complete
3. Include test outputs demonstrating your algorithms work correctly
4. Answer all analysis questions based on your experimental results
5. Include any visualizations or additional analysis you performed

---

#### **Grading Rubric**
- **Question 1** (40 points): Completeness and correctness of problem formulation and analysis
- **Question 2** (30 points): Accuracy of true/false answers with clear justifications
- **Question 3.1** (30 points): A* implementation correctness and efficiency
- **Question 3.2** (25 points): Greedy Best-First Search implementation
- **Question 3.3** (25 points): IDA* implementation
- **Analysis Questions** (20 points): Quality of experimental analysis and insights
- **Bonus** (10 points): Algorithm comparison and visualization features

**Total: 170 points (+ 10 bonus)**

---

#### **Programming Notes**
- Use appropriate data structures (priority queues, sets, dictionaries)
- Handle edge cases (no path, invalid inputs)
- Implement efficient node expansion and path reconstruction
- Track performance metrics for comparison
- Write clean, well-documented code
- Test thoroughly with the provided test cases