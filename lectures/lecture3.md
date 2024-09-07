<style TYPE="text/css">
code.has-jax {font: inherit; font-size: 100%; background: inherit; border: inherit;}
</style>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
    tex2jax: {
        inlineMath: [['$','$'], ['\\(','\\)']],
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'] // removed 'code' entry
    }
});
MathJax.Hub.Queue(function() {
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-AMS_HTML-full"></script>


# Lecture 3 - Interview Techniques / Testing and Defensive Programming



## Interview Techniques


### Interviewee

- Understand the problem
    - Resolve any ambiguities
    - Ask for clarifications of data types, resource limits, error handling, ...

- Talk out the problem
    - Thought process
    - Pros and cons of multiple approaches


### Interviewer

- Give the questions in the order assigned
- State the question clearly and concisely
    - Interviewee is supposed to ask for clarifications

- Give hints if stuck
    - Ask interviewee to think about alternative approaches
    - Give a *small* piece of the solution

- Watch the time
    - Do not start on a new question if near the *lower* time limit
    - Speed along the current question if neaar the *higher* time limit
        - Give more hints
        - Ask about the portions completed
        - Skip the actual coding on second/third questions; Assign N/A for 
    



### Interviewee Rubrics

| Question-Specific | 
| ----------------- |
| Did the student state the assumptions they are making about the problem and design of the solution verbally or in writing, including drawing diagrams as appropriate? |
| Did the student “talk-out” (verbally express) their thought process as they were implementing the solution? |
| Ask the student to explain why some portion of their code is important to solving the problem. Are they able to provide a brief, understandable, and compelling explanation? |
| Were the solutions syntactically correct for Java (7/8), Python, or Javascript, as appropriate? |
| Ask for an explanation of the solution they provide and why they think it is best. How well is the student able to explain it to you? |



| Entire Interview | 
| ---------------- |
| Was the student attentive and focused on the interview? |
| How knowledgeable or confident did the student appear to you? |
| Was the student polite and amiable? (5 = exellent to 0 = poor) |
| Did the student seem like they would be a good team player? (i.e. were they willing to explore alternative suggestions?) |
| How many hints did the student need over the entire interview? (5 = none, 4 = one or two, 3 = 3-4, 2 = 5-6, 1 = more than six) |


---

## Testing and Defensive Programming

### Testing
- Make the program work when programming
- Make the code FAIL when testing
    - Think of unusual or unexpected inputs


### Unit Testing
- **Unit testing** is the process of writing automated tests to verify that individual pieces (units) of code, such as functions or methods, work correctly in isolation.


### Boundary Conditions / Edge Cases
- Extremes
    - Empty input
    - Extremely large input
    - Smallest valid value
    - Largest valid value

- Error conditions
    - Division by zero
    - Overflow
    - Array index out of bound



### Black Box Testing & White Box Testing

- Black Box Testing: Only sees inputs and expected outputs, internal code is hidden.
- White Box Testing: Can see internal code, logic, and structure, along with inputs and outputs.


---


### Defensive Programming

- **Defensive programming** involves writing code that actively prevents errors during runtime by anticipating and handling unexpected conditions.

    1. **Check inputs**
        - Numbers: valid range?
            ```java
            int factorial(int n) {
                if (n == 1) return 1; // What if `n < 1`?
                return n * factorial(n-1);
            }
            ```
        - Strings and Arrays: empty?
        - Objects: null?
            ```java
            void inorderTrav(Node root) {
                inorderTrav(root.left); // What if `root == null`?
                System.out.println(root.v);
                inorderTrav(root.right);
            }
            ```

    2. **Check intermediate results**

        ```java
        int funcA() {
            int value = funcB(); // What if funcB fails? What if funcB returns value not valid?
            ...
        }
        ```


### The Robustness Principle
**The Robustness Principle**, a.k.a. Postel's Law, is a design guideline for software and systems, particularly in networking, which states:

    "Be conservative in what you send, be liberal in what you accept."

- When generating output (e.g., sending data), adhere strictly to protocol or specification to avoid creating ambiguous or invalid data that might cause errors for other systems or software.

- When receiving input, be tolerant and flexible, gracefully handle imperfect or unexpected input to avoid crashing or malfunctioning.row-major



### 2D Array Performance in Java

- Java arrays are stored in a **row-major** order, meaning that the elements in each row are stored sequentially in memory.

    - Efficient (row-major)
        ```java
        for (int[] row : a) {          // Iterates through each row
            for (int element : row) {  // Iterates through each element in the row
                ...
            }
        }
        ```

    - Inefficient (column-major)
        ```java
        for (int col = 0; col < numCols; col++) {
            for (int row = 0; row < numRows; row++) {
                int element = array[row][col];
                // Do something with element
            }
        }
        ```


---


## Multi-Threading

- **Race condition**: occurs when two or more threads access shared data or resources concurrently, and the outcome of the execution depends on the sequence or timing of these threads.

- Fixing data races
    - The `volatile` keyword ensures that the value of a variable is always read from and written to main memory, rather than being cached in the thread’s local memory (cache).
        - Ensures visibility

    - The `synchronized` keyword enforces mutual exclusion, ensuring that only one thread can access a critical section of code (such as a method or block) at a time.
        - Ensures atomicity

    - Both `volatile` and `synchronized` slow down the program; Use when neccessary to ensure correctness
        - `volatile` prevents various optimizations, forces memory accesses
        - `synchronized` prevents parallelism on multi-core machines






---

[Back to Home](../index.html)
[Next Lecture](./lecture4.html)