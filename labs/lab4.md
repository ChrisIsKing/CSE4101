# University of Guyana
## Faculty of Natural Sciences
### Department of Computer Science
#### CSE 4101 – Artificial Intelligence I
##### Lab Exercise: Constraint Satisfaction Problems and Knowledge Representation

---

#### **Instructions**
Answer all questions. For Questions 1-2, provide detailed written responses showing your problem formulations and analysis. For Question 3, complete the Python code as instructed to implement CSP algorithms and a knowledge-based inference system.

---

### **Question 1: Constraint Satisfaction Problem Formulation (40 Marks)**

Consider the problem of scheduling final exams for a university. There are four courses: **Math (M)**, **Physics (P)**, **Chemistry (C)**, and **Biology (B)**. Exams must be scheduled in one of three time slots: **Morning (9am)**, **Afternoon (2pm)**, or **Evening (6pm)**. The constraints are:

- Math and Physics cannot be at the same time (many students take both)
- Chemistry and Biology cannot be at the same time (many students take both)  
- Physics must be before Chemistry (Physics is a prerequisite)
- Math should not be in the evening slot (professor preference)

#### **Part 1.1: CSP Formulation (10 marks)**
Formulate this as a Constraint Satisfaction Problem. Clearly define:
1. **Variables**: $X = \{X_1, X_2, \ldots, X_n\}$
2. **Domains**: $D_i$ for each variable $X_i$
3. **Constraints**: Both unary and binary constraints

*Provide a complete formal specification of the CSP.*

---

#### **Part 1.2: Constraint Graph (10 marks)**
Draw the constraint graph for this CSP. For each edge, indicate what constraint it represents.

*Include a clear diagram with all variables as nodes and constraints as edges. Label each edge with its corresponding constraint.*

---

#### **Part 1.3: Arc Consistency Analysis (10 marks)**
Starting from the initial domains, apply the AC-3 algorithm to achieve arc consistency. Show your work step by step:

1. Initial queue of arcs
2. Processing of each arc
3. Domain reductions (if any)
4. Final consistent domains

*Demonstrate the complete AC-3 process with detailed steps.*

---

#### **Part 1.4: Search Strategy Analysis (10 marks)**
For solving this CSP with backtracking search, analyze:

1. What order would the **Minimum Remaining Values (MRV)** heuristic suggest for variable ordering?
2. What would the **Degree heuristic** suggest as a tie-breaker?
3. For the first variable chosen, what order would **Least Constraining Value (LCV)** suggest for values?

*Provide detailed reasoning for each heuristic application.*

---

### **Question 2: Knowledge Representation and Reasoning (30 Marks)**

Consider a simple family relationship knowledge base with the following facts:

**Facts:**
- John is the father of Mary
- John is the father of Tom  
- Mary is the mother of Alice
- Mary is the mother of Bob
- Tom is the father of Charlie
- Sue is the mother of Charlie
- Being a parent means being either a father or a mother
- Being a grandparent means being a parent of a parent
- Being a sibling means having the same parent

#### **Part 2.1: First-Order Logic Representation (10 marks)**
Represent the above knowledge in First-Order Logic (FOL). Use predicates such as:
- $\text{Father}(x, y)$: $x$ is the father of $y$
- $\text{Mother}(x, y)$: $x$ is the mother of $y$  
- $\text{Parent}(x, y)$: $x$ is a parent of $y$
- $\text{Grandparent}(x, y)$: $x$ is a grandparent of $y$
- $\text{Sibling}(x, y)$: $x$ and $y$ are siblings

*Write out all facts and rules in proper FOL notation with quantifiers where needed.*

---

#### **Part 2.2: Inference with Forward Chaining (10 marks)**
Using forward chaining, derive all possible facts from the knowledge base. Show the inference steps to answer:

1. Who are Alice's grandparents?
2. Who are Tom's siblings?
3. Who are Charlie's cousins (children of parent's siblings)?

*Show the step-by-step inference process using forward chaining.*

---

#### **Part 2.3: Resolution Proof (10 marks)**
Convert the following query to CNF and use resolution to prove it:
**Query**: "Is John a grandparent of Alice?"

Show:
1. Negation of the query
2. Conversion to CNF
3. Resolution steps
4. Derivation of the empty clause (or failure)

*Provide complete resolution proof with unification steps.*

---

### **Question 3: Implementing CSP Solver and Inference Engine (80 Marks)**

#### **Problem Description**
Implement a **Constraint Satisfaction Problem solver** with backtracking and constraint propagation, along with a simple **forward chaining inference engine** for propositional logic. 🧩

* CSP solver should handle various constraint types
* Implement smart variable and value ordering heuristics
* Forward chaining should derive all possible conclusions
* Compare performance with and without optimizations

#### **Your Task**
Complete the Python implementations below for the CSP solver and inference engine. Your implementations should:
1. Solve CSPs efficiently using backtracking with heuristics
2. Implement AC-3 algorithm for arc consistency
3. Perform forward chaining inference on propositional knowledge bases
4. Track performance metrics

---

### **Part 3.1: CSP Solver with Backtracking (35 Marks)**

```python
from typing import Dict, List, Set, Tuple, Callable, Optional, Any
import time
from collections import deque

class CSP:
    """
    Constraint Satisfaction Problem representation.
    """
    
    def __init__(self, variables: List[str], domains: Dict[str, List[Any]], 
                 constraints: List[Tuple[List[str], Callable]]):
        """
        Initialize a CSP.
        
        Args:
            variables: List of variable names
            domains: Dictionary mapping variables to their possible values
            constraints: List of (scope, constraint_function) tuples
                        scope is list of variables involved
                        constraint_function takes assignment dict and returns True/False
        """
        self.variables = variables
        self.domains = {v: list(domain) for v, domain in domains.items()}
        self.constraints = constraints
        self.neighbors = {v: set() for v in variables}
        
        # Build neighbor relationships from constraints
        for scope, _ in constraints:
            for v1 in scope:
                for v2 in scope:
                    if v1 != v2:
                        self.neighbors[v1].add(v2)
    
    def is_consistent(self, assignment: Dict[str, Any], var: str, value: Any) -> bool:
        """
        Check if assigning value to var is consistent with current assignment.
        
        Args:
            assignment: Current variable assignments
            var: Variable to assign
            value: Value to assign to var
            
        Returns:
            True if assignment is consistent, False otherwise
        """
        # === YOUR CODE GOES HERE ===
        # Create temporary assignment with new value
        # Check all constraints that involve var
        # Return True only if all relevant constraints are satisfied
        
        pass
        # ===========================
    
    def get_unassigned_variables(self, assignment: Dict[str, Any]) -> List[str]:
        """Get list of unassigned variables."""
        # === YOUR CODE GOES HERE ===
        pass
        # ===========================


def backtracking_search(csp: CSP, use_mrv: bool = False, 
                       use_lcv: bool = False, use_ac3: bool = False) -> Optional[Dict[str, Any]]:
    """
    Solve CSP using backtracking search with optional heuristics.
    
    Args:
        csp: The CSP to solve
        use_mrv: Whether to use Minimum Remaining Values heuristic
        use_lcv: Whether to use Least Constraining Value heuristic  
        use_ac3: Whether to use AC-3 for inference
        
    Returns:
        Solution assignment or None if no solution exists
    """
    
    def select_unassigned_variable(assignment: Dict[str, Any]) -> str:
        """
        Select next variable to assign.
        Uses MRV heuristic if enabled, with degree heuristic as tie-breaker.
        """
        # === YOUR CODE GOES HERE ===
        # If use_mrv is True:
        #   - Find variable with smallest domain (fewest legal values)
        #   - Use degree heuristic (most constraints) as tie-breaker
        # Otherwise:
        #   - Just return first unassigned variable
        
        pass
        # ===========================
    
    def order_domain_values(var: str, assignment: Dict[str, Any]) -> List[Any]:
        """
        Order domain values for variable.
        Uses LCV heuristic if enabled (prefer values that rule out fewest choices for neighbors).
        """
        # === YOUR CODE GOES HERE ===
        # If use_lcv is True:
        #   - For each value, count how many values it eliminates from neighbors
        #   - Sort by number of eliminations (ascending - least constraining first)
        # Otherwise:
        #   - Return domain values in original order
        
        pass
        # ===========================
    
    def backtrack(assignment: Dict[str, Any]) -> Optional[Dict[str, Any]]:
        """
        Recursive backtracking search.
        """
        # === YOUR CODE GOES HERE ===
        # Base case: if assignment is complete, return it
        
        # Select next variable to assign
        # For each value in ordered domain:
        #   - If value is consistent:
        #     - Add to assignment
        #     - If use_ac3, perform inference
        #     - Recursively backtrack
        #     - If result is not failure, return it
        #     - Remove assignment and restore domains
        
        # Return None if no solution found
        
        pass
        # ===========================
    
    # === YOUR CODE GOES HERE ===
    # Start with empty assignment
    # If use_ac3, run AC-3 first to reduce domains
    # Call backtrack and return result
    
    pass
    # ===========================
```

---

### **Part 3.2: AC-3 Algorithm Implementation (25 Marks)**

```python
def ac3(csp: CSP, queue: Optional[deque] = None) -> bool:
    """
    AC-3 algorithm for enforcing arc consistency.
    
    Args:
        csp: The CSP
        queue: Optional initial queue of arcs to process
        
    Returns:
        True if CSP is arc-consistent, False if inconsistency detected
    """
    # === YOUR CODE GOES HERE ===
    # Initialize queue with all arcs if not provided
    # An arc is (Xi, Xj) where Xi and Xj are neighboring variables
    
    # While queue is not empty:
    #   - Remove arc (Xi, Xj) from queue
    #   - If revise(Xi, Xj) removes values from Di:
    #     - If Di is empty, return False (inconsistent)
    #     - Add all arcs (Xk, Xi) to queue where Xk is neighbor of Xi (except Xj)
    
    # Return True (arc-consistent)
    
    pass
    # ===========================


def revise(csp: CSP, xi: str, xj: str) -> bool:
    """
    Make Xi arc-consistent with Xj.
    Remove values from Di that don't have a supporting value in Dj.
    
    Args:
        csp: The CSP
        xi: First variable
        xj: Second variable
        
    Returns:
        True if domain of Xi was revised (values removed)
    """
    # === YOUR CODE GOES HERE ===
    # revised = False
    # For each value vi in Di:
    #   - If no value vj in Dj satisfies constraint between Xi=vi and Xj=vj:
    #     - Remove vi from Di
    #     - revised = True
    # Return revised
    
    pass
    # ===========================
```

---

### **Part 3.3: Forward Chaining Inference Engine (20 Marks)**

```python
class KnowledgeBase:
    """
    Simple propositional logic knowledge base with forward chaining.
    """
    
    def __init__(self):
        """Initialize empty knowledge base."""
        self.facts = set()  # Known facts
        self.rules = []     # List of (premises, conclusion) tuples
        
    def tell_fact(self, fact: str):
        """Add a fact to the knowledge base."""
        self.facts.add(fact)
    
    def tell_rule(self, premises: List[str], conclusion: str):
        """
        Add a rule to the knowledge base.
        
        Args:
            premises: List of facts that must be true
            conclusion: Fact that follows from premises
        """
        self.rules.append((premises, conclusion))
    
    def ask(self, query: str) -> bool:
        """
        Query whether a fact can be derived.
        
        Args:
            query: Fact to query
            
        Returns:
            True if fact can be derived, False otherwise
        """
        # Run forward chaining first
        self.forward_chaining()
        return query in self.facts
    
    def forward_chaining(self) -> Set[str]:
        """
        Perform forward chaining to derive all possible facts.
        
        Returns:
            Set of all derived facts
        """
        # === YOUR CODE GOES HERE ===
        # Initialize agenda with current facts
        # While agenda is not empty:
        #   - Remove a fact from agenda
        #   - For each rule:
        #     - If all premises are in facts and conclusion not yet derived:
        #       - Add conclusion to facts
        #       - Add conclusion to agenda
        
        # Return all facts
        
        pass
        # ===========================
    
    def explain(self, query: str) -> List[str]:
        """
        Provide explanation for how a fact was derived.
        
        Args:
            query: Fact to explain
            
        Returns:
            List of inference steps
        """
        # === YOUR CODE GOES HERE (BONUS) ===
        # Track which rules were used to derive the fact
        # Build explanation chain backwards from query
        
        pass
        # ===========================
```

---

### **Part 3.4: Testing and Comparison (Bonus 10 Marks)**

```python
def test_csp_solver():
    """Test CSP solver on Map Coloring and N-Queens problems."""
    
    print("="*80)
    print("CSP SOLVER TESTS")
    print("="*80)
    
    # Test 1: Australia Map Coloring
    print("\nTest 1: Australia Map Coloring")
    print("-"*80)
    
    # Variables: Australian states/territories
    variables = ['WA', 'NT', 'SA', 'Q', 'NSW', 'V', 'T']
    
    # Domain: Three colors
    domains = {v: ['red', 'green', 'blue'] for v in variables}
    
    # Constraints: Adjacent regions must have different colors
    def different_colors(assignment, v1, v2):
        if v1 in assignment and v2 in assignment:
            return assignment[v1] != assignment[v2]
        return True
    
    constraints = [
        (['WA', 'NT'], lambda a: different_colors(a, 'WA', 'NT')),
        (['WA', 'SA'], lambda a: different_colors(a, 'WA', 'SA')),
        (['NT', 'SA'], lambda a: different_colors(a, 'NT', 'SA')),
        (['NT', 'Q'], lambda a: different_colors(a, 'NT', 'Q')),
        (['SA', 'Q'], lambda a: different_colors(a, 'SA', 'Q')),
        (['SA', 'NSW'], lambda a: different_colors(a, 'SA', 'NSW')),
        (['SA', 'V'], lambda a: different_colors(a, 'SA', 'V')),
        (['Q', 'NSW'], lambda a: different_colors(a, 'Q', 'NSW')),
        (['NSW', 'V'], lambda a: different_colors(a, 'NSW', 'V')),
    ]
    
    csp = CSP(variables, domains, constraints)
    
    # Test different configurations
    configs = [
        ("Basic Backtracking", False, False, False),
        ("Backtracking + MRV", True, False, False),
        ("Backtracking + MRV + LCV", True, True, False),
        ("Backtracking + MRV + LCV + AC3", True, True, True),
    ]
    
    for name, use_mrv, use_lcv, use_ac3 in configs:
        start_time = time.time()
        solution = backtracking_search(csp, use_mrv, use_lcv, use_ac3)
        end_time = time.time()
        
        print(f"\n{name}:")
        if solution:
            print(f"  Solution: {solution}")
            print(f"  Time: {end_time - start_time:.4f}s")
        else:
            print(f"  No solution found")
    
    # === YOUR CODE GOES HERE ===
    # Test 2: N-Queens problem
    # Test 3: Sudoku puzzle
    # Compare performance with different heuristics
    
    pass
    # ===========================


def test_inference_engine():
    """Test forward chaining inference engine."""
    
    print("\n" + "="*80)
    print("INFERENCE ENGINE TESTS")
    print("="*80)
    
    # Build family relationships knowledge base
    kb = KnowledgeBase()
    
    # Facts
    kb.tell_fact("father(john, mary)")
    kb.tell_fact("father(john, tom)")
    kb.tell_fact("mother(mary, alice)")
    kb.tell_fact("mother(mary, bob)")
    
    # Rules
    # Parent rule: father(X,Y) => parent(X,Y)
    kb.tell_rule(["father(john, mary)"], "parent(john, mary)")
    kb.tell_rule(["father(john, tom)"], "parent(john, tom)")
    kb.tell_rule(["mother(mary, alice)"], "parent(mary, alice)")
    kb.tell_rule(["mother(mary, bob)"], "parent(mary, bob)")
    
    # Grandparent rules
    kb.tell_rule(["parent(john, mary)", "parent(mary, alice)"], 
                 "grandparent(john, alice)")
    kb.tell_rule(["parent(john, mary)", "parent(mary, bob)"], 
                 "grandparent(john, bob)")
    
    # Test queries
    queries = [
        "parent(john, mary)",
        "grandparent(john, alice)",
        "grandparent(john, charlie)",
    ]
    
    print("\nQuery Results:")
    for query in queries:
        result = kb.ask(query)
        print(f"  {query}: {result}")
    
    # === YOUR CODE GOES HERE ===
    # Test more complex rule chains
    # Test with different knowledge bases
    
    pass
    # ===========================


if __name__ == "__main__":
    test_csp_solver()
    test_inference_engine()
```

---

#### **Analysis Questions**

After implementing and testing your algorithms, answer the following:

1. **Heuristic Effectiveness**: How much do MRV and LCV improve performance on the CSP problems? Provide concrete timing comparisons.

2. **AC-3 Impact**: When does AC-3 preprocessing help? When does it add unnecessary overhead?

3. **Problem Characteristics**: What CSP characteristics make backtracking difficult? What makes arc consistency effective?

4. **Forward Chaining Completeness**: Is forward chaining complete for propositional logic? What are its limitations?

5. **Real-world Applications**: 
   - Give two examples where CSPs are used in practice
   - Give two examples where rule-based inference systems are used

---

#### **Submission Guidelines**
1. Submit your written responses for Questions 1-2 in a PDF document
2. Submit your Python code file with all implementations complete
3. Include test outputs demonstrating your algorithms work correctly
4. Answer all analysis questions based on your experimental results
5. Include any additional test cases you created

---

#### **Grading Rubric**
- **Question 1** (40 points): CSP formulation, constraint graph, AC-3 analysis, heuristics
- **Question 2** (30 points): FOL representation, forward chaining, resolution proof
- **Question 3.1** (35 points): CSP solver with backtracking and heuristics
- **Question 3.2** (25 points): AC-3 algorithm implementation
- **Question 3.3** (20 points): Forward chaining inference engine
- **Analysis Questions** (20 points): Quality of experimental analysis and insights
- **Bonus** (10 points): Additional features and comprehensive testing

**Total: 170 points (+ 10 bonus)**

---

#### **Programming Notes**
- Use appropriate data structures (sets, queues, dictionaries)
- Handle edge cases (empty domains, unsatisfiable CSPs)
- Track assignments and domain reductions properly
- Write clean, well-documented code
- Test with various problem instances
- Compare algorithmic variations systematically
