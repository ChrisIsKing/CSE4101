# University of Guyana
## Faculty of Natural Sciences
### Department of Computer Science
#### CSE 4101 – Artificial Intelligence I
##### Lab Exercise: Problem Solving with Search

---

#### **Instructions**
Answer all questions. For Questions 1-2, provide detailed written responses showing your problem formulations. For Questions 3-5, complete the Python code as instructed to implement search algorithms.

---

### **Question 1: Robot Maze Navigation (25 Marks)**

Your goal is to navigate a robot out of a maze. The robot starts in the center of the maze facing north. You can turn the robot to face north, east, south, or west. You can direct the robot to move forward a certain distance, although it will stop before hitting a wall.

1. **Formulate this problem. How large is the state space?** (6 marks)
   
   *Provide a complete problem formulation including: initial state, actions, transition model, goal test, and path cost. Calculate the size of the state space.*

2. **In navigating a maze, the only place we need to turn is at the intersection of two or more corridors. Reformulate this problem using this observation. How large is the state space now?** (6 marks)
   
   *Reformulate the problem with the reduced state space and explain how the size changes.*

3. **From each point in the maze, we can move in any of the four directions until we reach a turning point, and this is the only action we need to do. Reformulate the problem using these actions. Do we need to keep track of the robot's orientation now?** (7 marks)
   
   *Reformulate the problem with these new actions and discuss whether orientation is still necessary.*

4. **In our initial description of the problem we already abstracted from the real world, restricting actions and removing details. List three such simplifications we made.** (6 marks)
   
   *Identify and explain three simplifications made in the problem formulation.*

---

### **Question 2: Problem Formulations (40 Marks)**

Give a complete problem formulation for each of the following problems. Choose a formulation that is precise enough to be implemented.

For each problem, specify:
- **States**: What does each state represent?
- **Initial State**: What is the starting configuration?
- **Actions**: What actions are available in each state?
- **Transition Model**: What is the result of each action?
- **Goal Test**: How do we know if we've reached the goal?
- **Path Cost**: How do we measure the cost of a solution?

#### **2.1 Glass Boxes Problem (10 marks)**

There are six glass boxes in a row, each with a lock. Each of the first five boxes holds a key unlocking the next box in line; the last box holds a banana. You have the key to the first box, and you want the banana.

*Provide your complete problem formulation here.*

---

#### **2.2 Sequence Transformation Problem (10 marks)**

You start with the sequence ABABAECCEC, or in general any sequence made from A, B, C, and E. You can transform this sequence using the following equalities: AC = E, AB = BC, BB = E, and Ex = x for any x. For example, ABBC can be transformed into AEC, and then AC, and then E. Your goal is to produce the sequence E.

*Provide your complete problem formulation here.*

---

#### **2.3 Floor Painting Problem (10 marks)**

There is an n×n grid of squares, each square initially being either unpainted floor or a bottomless pit. You start standing on an unpainted floor square, and can either paint the square under you or move onto an adjacent unpainted floor square. You want the whole floor painted.

*Provide your complete problem formulation here.*

---

#### **2.4 Container Ship Unloading Problem (10 marks)**

A container ship is in port, loaded high with containers. There are 13 rows of containers, each 13 containers wide and 5 containers tall. You control a crane that can move to any location above the ship, pick up the container under it, and move it onto the dock. You want the ship unloaded.

*Provide your complete problem formulation here.*

---

### **Question 3: Implementing Breadth-First Search (35 Marks)**

#### **Problem Description**
Implement a **Breadth-First Search (BFS)** algorithm to solve pathfinding problems in a grid world. 🗺️

* The world is represented as a 2D grid where:
  - `0` represents a free cell (can move through)
  - `1` represents a wall (cannot move through)
  - `S` marks the start position
  - `G` marks the goal position
* The agent can move in four directions: up, down, left, right
* BFS explores nodes level by level, guaranteeing the shortest path in unweighted graphs

#### **Your Task**
Complete the Python functions in the starter code below to implement BFS. Your implementation should:
1. Use a queue (FIFO) for the frontier
2. Keep track of explored nodes to avoid cycles
3. Return the path from start to goal
4. Handle cases where no path exists

#### **Starter Code**
```python
from collections import deque

class GridWorld:
    """Represents a grid world for pathfinding problems."""
    
    def __init__(self, grid):
        """
        Initialize the grid world.
        
        Args:
            grid (list): 2D list where 0=free, 1=wall, 'S'=start, 'G'=goal
        """
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
    
    def get_neighbors(self, position):
        """
        Get valid neighboring positions (up, down, left, right).
        
        Args:
            position (tuple): Current position (row, col)
            
        Returns:
            list: List of valid neighboring positions
        """
        # === YOUR CODE GOES HERE ===
        # Define four directions: up, down, left, right
        # Check each direction and add valid neighbors (within bounds and not walls)
        # Return list of valid neighbor positions
        
        pass
        # ===========================
    
    def is_valid(self, position):
        """
        Check if a position is valid (within bounds and not a wall).
        
        Args:
            position (tuple): Position to check (row, col)
            
        Returns:
            bool: True if position is valid, False otherwise
        """
        # === YOUR CODE GOES HERE ===
        
        pass
        # ===========================


def breadth_first_search(grid_world):
    """
    Perform Breadth-First Search to find the shortest path from start to goal.
    
    Args:
        grid_world (GridWorld): The grid world to search
        
    Returns:
        list: Path from start to goal as a list of positions, or None if no path exists
    """
    # === YOUR CODE GOES HERE ===
    # Initialize:
    # - Queue (frontier) with start node
    # - Set of explored nodes
    # - Dictionary to track parent of each node (for reconstructing path)
    
    # BFS main loop:
    # While frontier is not empty:
    #   - Dequeue a node
    #   - If it's the goal, reconstruct and return the path
    #   - Mark it as explored
    #   - For each neighbor:
    #     - If not explored and not in frontier:
    #       - Add to frontier
    #       - Record its parent
    
    # If we exit the loop, no path exists
    
    pass
    # ===========================


def reconstruct_path(parent_map, start, goal):
    """
    Reconstruct the path from start to goal using the parent map.
    
    Args:
        parent_map (dict): Maps each node to its parent
        start (tuple): Start position
        goal (tuple): Goal position
        
    Returns:
        list: Path from start to goal
    """
    # === YOUR CODE GOES HERE ===
    # Start from goal and work backwards using parent_map
    # Reverse the path before returning
    
    pass
    # ===========================


# Test harness
if __name__ == "__main__":
    # Define test grids
    test_grid_1 = [
        ['S', 0, 0, 0],
        [1, 1, 0, 1],
        [0, 0, 0, 0],
        [0, 1, 1, 'G']
    ]
    
    test_grid_2 = [
        ['S', 0, 1, 0, 0],
        [0, 0, 1, 0, 1],
        [0, 0, 0, 0, 0],
        [1, 1, 0, 1, 0],
        [0, 0, 0, 1, 'G']
    ]
    
    test_grid_3 = [
        ['S', 0, 0],
        [1, 1, 0],
        [0, 0, 'G']
    ]
    
    # Test with impossible path
    test_grid_4 = [
        ['S', 0, 1],
        [1, 1, 1],
        [0, 0, 'G']
    ]
    
    grids = [test_grid_1, test_grid_2, test_grid_3, test_grid_4]
    
    for i, grid in enumerate(grids, 1):
        print(f"\n{'='*50}")
        print(f"Test Grid {i}:")
        print('='*50)
        for row in grid:
            print(row)
        
        world = GridWorld(grid)
        path = breadth_first_search(world)
        
        if path:
            print(f"\nPath found! Length: {len(path)}")
            print(f"Path: {path}")
        else:
            print("\nNo path exists!")
```

---

### **Question 4: Implementing Depth-First Search (35 Marks)**

#### **Problem Description**
Implement a **Depth-First Search (DFS)** algorithm for the same grid world problem. 🔍

* DFS explores as far as possible along each branch before backtracking
* Unlike BFS, DFS does not guarantee the shortest path
* DFS can be implemented using a stack (LIFO) or recursively

#### **Your Task**
Complete the Python function below to implement DFS. Compare its behavior to BFS on the same test cases.

#### **Starter Code**
```python
from collections import deque

def depth_first_search(grid_world):
    """
    Perform Depth-First Search to find a path from start to goal.
    Note: DFS does not guarantee the shortest path.
    
    Args:
        grid_world (GridWorld): The grid world to search
        
    Returns:
        list: A path from start to goal, or None if no path exists
    """
    # === YOUR CODE GOES HERE ===
    # Initialize:
    # - Stack (frontier) with start node - use a list and pop() for LIFO behavior
    # - Set of explored nodes
    # - Dictionary to track parent of each node
    
    # DFS main loop (similar to BFS but using stack instead of queue):
    # While frontier is not empty:
    #   - Pop a node from stack (LIFO)
    #   - If it's the goal, reconstruct and return the path
    #   - Mark it as explored
    #   - For each neighbor:
    #     - If not explored and not in frontier:
    #       - Add to frontier (push to stack)
    #       - Record its parent
    
    # If we exit the loop, no path exists
    
    pass
    # ===========================


def depth_first_search_recursive(grid_world):
    """
    Perform Depth-First Search using recursion.
    
    Args:
        grid_world (GridWorld): The grid world to search
        
    Returns:
        list: A path from start to goal, or None if no path exists
    """
    def dfs_helper(current, goal, explored, path):
        """
        Recursive helper function for DFS.
        
        Args:
            current (tuple): Current position
            goal (tuple): Goal position
            explored (set): Set of explored positions
            path (list): Current path being explored
            
        Returns:
            list: Path to goal if found, None otherwise
        """
        # === YOUR CODE GOES HERE ===
        # Base case: if current is goal, return path
        # Mark current as explored
        # For each neighbor:
        #   - If not explored:
        #     - Recursively call dfs_helper
        #     - If a path is found, return it
        # If no path found from any neighbor, return None
        
        pass
        # ===========================
    
    # === YOUR CODE GOES HERE ===
    # Initialize explored set and starting path
    # Call the recursive helper function
    
    pass
    # ===========================


# Test harness
if __name__ == "__main__":
    # Use the same GridWorld class from Question 3
    
    # Define test grids
    test_grid_1 = [
        ['S', 0, 0, 0],
        [1, 1, 0, 1],
        [0, 0, 0, 0],
        [0, 1, 1, 'G']
    ]
    
    test_grid_2 = [
        ['S', 0, 1, 0, 0],
        [0, 0, 1, 0, 1],
        [0, 0, 0, 0, 0],
        [1, 1, 0, 1, 0],
        [0, 0, 0, 1, 'G']
    ]
    
    grids = [test_grid_1, test_grid_2]
    
    for i, grid in enumerate(grids, 1):
        print(f"\n{'='*50}")
        print(f"Test Grid {i}:")
        print('='*50)
        for row in grid:
            print(row)
        
        world = GridWorld(grid)
        
        # Test iterative DFS
        print("\nIterative DFS:")
        path_iterative = depth_first_search(world)
        if path_iterative:
            print(f"Path found! Length: {len(path_iterative)}")
            print(f"Path: {path_iterative}")
        else:
            print("No path exists!")
        
        # Test recursive DFS
        print("\nRecursive DFS:")
        path_recursive = depth_first_search_recursive(world)
        if path_recursive:
            print(f"Path found! Length: {len(path_recursive)}")
            print(f"Path: {path_recursive}")
        else:
            print("No path exists!")
        
        # Compare with BFS from Question 3
        print("\nComparison with BFS:")
        path_bfs = breadth_first_search(world)
        if path_bfs:
            print(f"BFS path length: {len(path_bfs)}")
            print(f"DFS iterative path length: {len(path_iterative) if path_iterative else 'N/A'}")
            print(f"DFS recursive path length: {len(path_recursive) if path_recursive else 'N/A'}")
```

#### **Analysis Questions**
1. **Path Quality**: Compare the path lengths found by BFS and DFS. Which algorithm finds shorter paths? Why?
2. **Performance**: Which algorithm explores more nodes before finding the goal? Why?
3. **Memory Usage**: Which algorithm uses more memory in the worst case? Explain.
4. **Use Cases**: When would you prefer DFS over BFS? When would you prefer BFS over DFS?

---

### **Question 5: Implementing Uniform Cost Search (35 Marks)**

#### **Problem Description**
Implement **Uniform Cost Search (UCS)**, a variant of BFS that accounts for varying edge costs. 💰

* In this enhanced grid world, different terrain types have different costs:
  - Free cells (0): cost 1
  - Rough terrain (2): cost 5
  - Highway (3): cost 0.5
  - Walls (1): impassable
* UCS expands the node with the lowest path cost first
* UCS guarantees the optimal (lowest cost) path

#### **Your Task**
Implement UCS using a priority queue. The algorithm should find the lowest-cost path, not just the shortest path in terms of number of steps.

#### **Starter Code**
```python
import heapq

class EnhancedGridWorld(GridWorld):
    """Enhanced grid world with terrain costs."""
    
    # Terrain cost mapping
    TERRAIN_COSTS = {
        0: 1,      # Normal terrain
        2: 5,      # Rough terrain
        3: 0.5,    # Highway
        'S': 1,    # Start
        'G': 1     # Goal
    }
    
    def get_cost(self, position):
        """
        Get the cost of moving to a position.
        
        Args:
            position (tuple): Position (row, col)
            
        Returns:
            float: Cost of entering this cell
        """
        # === YOUR CODE GOES HERE ===
        
        pass
        # ===========================


def uniform_cost_search(grid_world):
    """
    Perform Uniform Cost Search to find the lowest-cost path.
    
    Args:
        grid_world (EnhancedGridWorld): The enhanced grid world to search
        
    Returns:
        tuple: (path, total_cost) where path is list of positions and total_cost is the path cost,
               or (None, float('inf')) if no path exists
    """
    # === YOUR CODE GOES HERE ===
    # Initialize:
    # - Priority queue (frontier) with (cost, position) tuples
    #   Use heapq.heappush() and heapq.heappop()
    # - Dictionary to track best cost to reach each node
    # - Dictionary to track parent of each node
    # - Set of explored nodes
    
    # UCS main loop:
    # While frontier is not empty:
    #   - Pop node with lowest cost
    #   - If it's the goal, reconstruct path and return (path, cost)
    #   - If already explored with lower cost, skip
    #   - Mark as explored
    #   - For each neighbor:
    #     - Calculate new cost = current cost + step cost
    #     - If this is a better path to neighbor:
    #       - Update cost and parent
    #       - Add to frontier with new cost
    
    # If we exit the loop, no path exists
    
    pass
    # ===========================


# Test harness
if __name__ == "__main__":
    # Define test grids with different terrain types
    # 0 = normal (cost 1), 2 = rough (cost 5), 3 = highway (cost 0.5), 1 = wall
    
    test_grid_1 = [
        ['S', 0, 0, 0],
        [1, 1, 0, 1],
        [2, 2, 0, 0],
        [2, 1, 1, 'G']
    ]
    
    test_grid_2 = [
        ['S', 3, 3, 3, 0],
        [0, 2, 1, 3, 1],
        [0, 2, 0, 3, 0],
        [1, 2, 0, 1, 0],
        [0, 0, 0, 1, 'G']
    ]
    
    test_grid_3 = [
        ['S', 2, 3],
        [0, 0, 3],
        [0, 0, 'G']
    ]
    
    grids = [test_grid_1, test_grid_2, test_grid_3]
    
    for i, grid in enumerate(grids, 1):
        print(f"\n{'='*50}")
        print(f"Test Grid {i}:")
        print('='*50)
        for row in grid:
            print(row)
        
        # Test UCS
        world = EnhancedGridWorld(grid)
        path_ucs, cost_ucs = uniform_cost_search(world)
        
        if path_ucs:
            print(f"\nUCS Path found!")
            print(f"Path length (steps): {len(path_ucs)}")
            print(f"Path cost: {cost_ucs:.2f}")
            print(f"Path: {path_ucs}")
        else:
            print("\nNo path exists!")
        
        # Compare with BFS (if you completed Question 3)
        print("\nComparison with BFS:")
        path_bfs = breadth_first_search(world)
        if path_bfs:
            # Calculate cost of BFS path
            bfs_cost = sum(world.get_cost(pos) for pos in path_bfs)
            print(f"BFS path length: {len(path_bfs)}, cost: {bfs_cost:.2f}")
            print(f"UCS path length: {len(path_ucs)}, cost: {cost_ucs:.2f}")
            print(f"Cost savings with UCS: {bfs_cost - cost_ucs:.2f}")
        else:
            print("BFS path: None")

def visualize_path(grid, path):
    """
    Visualize the path on the grid.
    
    Args:
        grid (list): The original grid
        path (list): Path as list of positions
    """
    # === YOUR CODE GOES HERE (OPTIONAL BONUS) ===
    # Create a copy of the grid
    # Mark the path with a special character (e.g., '*')
    # Print the grid with the path highlighted
    
    pass
    # ===========================
```

#### **Analysis Questions**
1. **Optimality**: Why does UCS guarantee the optimal (lowest cost) path?
2. **Comparison**: How do the paths found by UCS differ from those found by BFS?
3. **Efficiency**: In what scenarios is UCS significantly better than BFS?
4. **Priority Queue**: Why is a priority queue essential for UCS? What would happen if we used a regular queue?

---

#### **Submission Guidelines**
1. Submit your written responses for Questions 1-2 in a PDF document
2. Submit your Python code files for Questions 3-5
3. Include test outputs demonstrating your implementations work correctly
4. Answer all analysis questions for Questions 4-5

---

#### **Grading Rubric**
- **Question 1** (25 points): Completeness and correctness of problem formulations
- **Question 2** (40 points): Precision and implementability of formulations (10 points each)
- **Question 3** (35 points): BFS implementation correctness and completeness
- **Question 4** (35 points): DFS implementation and analysis
- **Question 5** (35 points): UCS implementation and analysis

**Total: 170 points**

---
