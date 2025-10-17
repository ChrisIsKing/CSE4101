# University of Guyana
## Faculty of Natural Sciences
### Department of Computer Science
#### CSE 4101 – Artificial Intelligence I
##### Lab Exercise: Intelligent Agents

---

#### **Instructions**
Answer all questions. For Question 1, provide a clear justification for your "True" or "False" answer. For Question 2, provide a complete PEAS description and characterize the task environment for each activity. For Question 3, complete the Python code as instructed.

---

### **Question 1: True or False (18 Marks)**

*For each of the following assertions, state whether it is **true** or **false** and support your answer with a brief explanation, example, or counterexample.*

1.  An agent that senses only partial information about the state cannot be perfectly rational.
    

2.  There exist task environments in which no pure reflex agent can behave rationally.
    

3.  There exists a task environment in which every agent is rational.
    

4.  The input to an agent program is the same as the input to the agent function.
    

5.  Every agent function is implementable by some program/machine combination.
    

6.  Suppose an agent selects its action uniformly at random from the set of possible actions. There exists a deterministic task environment in which this agent is rational.
    

7.  It is possible for a given agent to be perfectly rational in two distinct task environments.
    

8.  Every agent is rational in an unobservable environment.
    

9.  A perfectly rational poker-playing agent never loses.
    

---

### **Question 2: PEAS Descriptions (32 Marks)**

*For each activity, provide a **PEAS** (Performance, Environment, Actuators, Sensors) description and characterize the task environment in terms of its properties (e.g., Fully/Partially Observable, Single/Multi-agent, etc.).*

| Activity                      | Performance | Environment | Actuators | Sensors | Environment Characterization |
| :---------------------------- | :---------- | :---------- | :-------- | :------ | :--------------------------- |
| **Playing soccer** |             |             |           |         |                              |
| **Exploring Titan's oceans** |             |             |           |         |                              |
| **Shopping for used AI books** |             |             |           |         |                              |
| **Playing a tennis match** |             |             |           |         |                              |
| **Practicing tennis against a wall**|             |             |           |         |                              |
| **Performing a high jump** |             |             |           |         |                              |
| **Knitting a sweater** |             |             |           |         |                              |
| **Bidding on an item at an auction** |             |             |           |         |                              |

---

### **Question 3: Coding a Simple Reflex Agent (15 Marks)**

#### **Problem Description**
You are to implement a simple reflex agent for a vacuum-cleaner world. 🤖
* The world consists of two locations: **A** and **B**.
* Each location can be in one of two states: **'Clean'** or **'Dirty'**.
* The agent receives a **percept** as a tuple, e.g., `('A', 'Dirty')`, indicating its current location and the status of that location.
* The agent can perform one of three actions: **'Suck'**, **'Right'** (from A to B), or **'Left'** (from B to A).

#### **Your Task**
Complete the Python function `simple_reflex_agent` in the starter code below. The function should implement the following logic:
1.  If the current location is dirty, the agent should `Suck`.
2.  If the current location is clean and the location is A, the agent should move `Right`.
3.  If the current location is clean and the location is B, the agent should move `Left`.

#### **Starter Code**
```python
def simple_reflex_agent(percept):
    """
    Implements a simple reflex agent for the two-location vacuum world.

    Args:
        percept (tuple): A tuple containing the agent's current location ('A' or 'B')
                         and the status of that location ('Clean' or 'Dirty').
                         Example: ('A', 'Dirty')

    Returns:
        str: The action to be taken: 'Suck', 'Right', or 'Left'.
    """
    location, status = percept

    # === YOUR CODE GOES HERE ===

    pass

    # ===========================


# Test harness to verify your agent's behavior
# You can run this file to see the output of your agent on test cases.
if __name__ == "__main__":
    # Define a set of test percepts
    percepts = [
        ('A', 'Dirty'),
        ('A', 'Clean'),
        ('B', 'Dirty'),
        ('B', 'Clean')
    ]

    print("Testing the Simple Reflex Agent...")
    for p in percepts:
        action = simple_reflex_agent(p)
        print(f"Percept: {p} -> Action: {action}")
```

---

### **Question 4: Model-Based Reflex Agent (20 Marks)**

#### **Problem Description**
Extend the vacuum-cleaner world to implement a **model-based reflex agent**. 🧠
* The world still consists of two locations: **A** and **B**.
* Each location can be in one of two states: **'Clean'** or **'Dirty'**.
* The agent now needs to build an **internal model** of the environment to track:
  - The current state of both locations
  - The effects of its actions (e.g., 'Suck' cleans the current location, 'Right' moves from A to B)
* The agent receives a **percept** as a tuple, e.g., `('A', 'Dirty')`, indicating its current location and the status of that location.
* The agent can perform one of three actions: **'Suck'**, **'Right'** (from A to B), or **'Left'** (from B to A).

#### **Your Task**
Complete the Python class `ModelBasedReflexAgent` in the starter code below. The agent should:
1. Maintain an internal model of both locations' states
2. Update its model based on percepts and actions
3. Choose actions based on its current model to clean both locations efficiently

#### **Starter Code**
```python
class ModelBasedReflexAgent:
    """
    Implements a model-based reflex agent for the two-location vacuum world.
    The agent maintains an internal model of the world state.
    """
    
    def __init__(self):
        """Initialize the agent with an empty world model."""
        # === YOUR CODE GOES HERE ===
        # Initialize internal model to track state of locations A and B
        # Initialize current location
        pass
        # ===========================
    
    def update_model(self, percept, action):
        """
        Update the internal model based on the current percept and last action.
        
        Args:
            percept (tuple): Current location and status ('A'/'B', 'Clean'/'Dirty')
            action (str): Last action taken ('Suck', 'Right', 'Left', or None for first step)
        """
        # === YOUR CODE GOES HERE ===
        # Update current location based on percept
        # Update location state based on percept
        # If last action was 'Suck', mark current location as clean
        pass
        # ===========================
    
    def choose_action(self, percept):
        """
        Choose an action based on the current percept and internal model.
        
        Args:
            percept (tuple): Current location and status ('A'/'B', 'Clean'/'Dirty')
            
        Returns:
            str: The action to be taken: 'Suck', 'Right', or 'Left'
        """
        # === YOUR CODE GOES HERE ===
        # If current location is dirty, suck
        # If both locations are clean, stay put or move randomly
        # If current location is clean but other location might be dirty, move to it
        pass
        # ===========================

# Test harness for the model-based agent
if __name__ == "__main__":
    agent = ModelBasedReflexAgent()
    
    # Simulate a sequence of percepts
    percept_sequence = [
        ('A', 'Dirty'),
        ('A', 'Clean'),
        ('B', 'Dirty'),
        ('B', 'Clean'),
        ('A', 'Clean')
    ]
    
    print("Testing the Model-Based Reflex Agent...")
    last_action = None
    for percept in percept_sequence:
        agent.update_model(percept, last_action)
        action = agent.choose_action(percept)
        print(f"Percept: {percept} -> Action: {action}")
        last_action = action
```

---

### **Question 5: Table-Driven Agent (15 Marks)**

#### **Problem Description**
Implement a **table-driven agent** for the vacuum-cleaner world. 📋
* This agent uses a lookup table that maps every possible **percept sequence** to an action.
* The agent maintains a complete history of all percepts it has experienced.
* For each percept sequence, there is a predetermined action stored in the table.
* This exercise demonstrates the **impracticality** of table-driven agents for non-trivial environments.

#### **Your Task**
Complete the Python class `TableDrivenAgent` in the starter code below. The agent should:
1. Maintain a complete history of percepts (percept sequence)
2. Use a lookup table to determine actions based on the percept sequence
3. Handle cases where the percept sequence is not in the table

#### **Starter Code**
```python
class TableDrivenAgent:
    """
    Implements a table-driven agent for the two-location vacuum world.
    Uses a lookup table to map percept sequences to actions.
    """
    
    def __init__(self):
        """Initialize the agent with a predefined lookup table."""
        # === YOUR CODE GOES HERE ===
        # Initialize empty percept sequence history
        # Define the lookup table mapping percept sequences to actions
        # Note: This table will grow exponentially with sequence length!
        self.table = {
            # Example entries - you need to complete this
            (('A', 'Dirty'),): 'Suck',
            (('A', 'Clean'),): 'Right',
            (('B', 'Dirty'),): 'Suck',
            (('B', 'Clean'),): 'Left',
            # Add more sequences as needed...
        }
        pass
        # ===========================
    
    def lookup(self, percept_sequence):
        """
        Look up the action for a given percept sequence in the table.
        
        Args:
            percept_sequence (tuple): Sequence of percepts experienced so far
            
        Returns:
            str: The action to take, or 'NoOp' if sequence not found
        """
        # === YOUR CODE GOES HERE ===
        # Return the action from the table, or 'NoOp' if not found
        pass
        # ===========================
    
    def choose_action(self, percept):
        """
        Choose an action based on the complete percept sequence.
        
        Args:
            percept (tuple): Current percept ('A'/'B', 'Clean'/'Dirty')
            
        Returns:
            str: The action to be taken
        """
        # === YOUR CODE GOES HERE ===
        # Add current percept to the sequence
        # Look up action in table based on complete sequence
        # Return the action
        pass
        # ===========================

# Test harness for the table-driven agent
if __name__ == "__main__":
    agent = TableDrivenAgent()
    
    # Test with a short sequence
    percepts = [
        ('A', 'Dirty'),
        ('A', 'Clean'),
        ('B', 'Dirty'),
        ('B', 'Clean')
    ]
    
    print("Testing the Table-Driven Agent...")
    for percept in percepts:
        action = agent.choose_action(percept)
        print(f"Percept: {percept}, Sequence: {agent.percept_sequence} -> Action: {action}")
    
    # Demonstrate the exponential growth problem
    print(f"\nTable size: {len(agent.table)} entries")
    print("Note: Table size grows exponentially with sequence length!")

def demonstrate_exponential_growth():
    """
    Demonstrate the exponential growth problem with table-driven agents.
    This function shows why table-driven agents are impractical for non-trivial environments.
    """
    print("\n" + "="*50)
    print("TABLE-DRIVEN AGENT SCALABILITY ANALYSIS")
    print("="*50)
    print("With 4 possible percepts in our 2-location world:")
    print("('A','Clean'), ('A','Dirty'), ('B','Clean'), ('B','Dirty')")
    print()
    
    for length in range(1, 11):
        entries_needed = 4 ** length
        print(f"Sequence length {length:2d}: {entries_needed:,} table entries needed")
    
    print()
    print("Memory requirements for length 10: Over 1 MILLION entries!")
    print("This demonstrates why table-driven agents are impractical!")

# Run the exponential growth demonstration
if __name__ == "__main__":
    # Test the table-driven agent first
    agent = TableDrivenAgent()
    
    percepts = [
        ('A', 'Dirty'),
        ('A', 'Clean'),
        ('B', 'Dirty'),
        ('B', 'Clean')
    ]
    
    print("Testing the Table-Driven Agent...")
    for percept in percepts:
        action = agent.choose_action(percept)
        print(f"Percept: {percept}, Sequence: {agent.percept_sequence} -> Action: {action}")
    
    print(f"\nTable size: {len(agent.table)} entries")
    print("Note: Table size grows exponentially with sequence length!")
    
    # Now demonstrate the exponential growth problem
    demonstrate_exponential_growth()
```

#### **Reflection Questions**
1. **Scalability**: How does the size of the lookup table grow as the length of percept sequences increases?
2. **Practicality**: Why is the table-driven approach impractical for real-world environments?
3. **Memory Requirements**: Calculate how many table entries would be needed for sequences of length 10 in this simple 2-location world.
4. **Real-world Implications**: If a robot vacuum had 10 rooms instead of 2 locations, how would this affect the table size?

---