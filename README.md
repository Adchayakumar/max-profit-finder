Title: Max Profit Scheduling Problem

Problem Overview  
Mr. X owns a large strip of land and can build three types of buildings: Theatres, Pubs, and Commercial Parks. Each type has a fixed build time and then earns money for every unit of time it is operational after construction completes.

- Theatre: build time = 5, earns 1500 per time unit when operational  
- Pub: build time = 4, earns 1000 per time unit when operational  
- Commercial Park: build time = 10, earns 2000 per time unit when operational  

Only one building can be constructed at a time (no parallel construction).  
For a given total time n, the goal is to choose how many of each building to construct, and in which order, to maximize the total earnings at time n.  

The output is:
- Total earnings  
- Number of Theatres (T)  
- Number of Pubs (P)  
- Number of Commercial Parks (C)

Example:  
For n = 7, both of these schedules give earnings 3000:  
- Build one Theatre: build 0–5, operational 5–7 → 2 units × 1500 = 3000  
- Build one Pub: build 0–4, operational 4–7 → 3 units × 1000 = 3000  

Short Description of the Approach  
The solution is based on dynamic programming over time.

Idea:
- Consider the current time t (0 ≤ t ≤ n).  
- From time t, you can either:
  - Stop building, or
  - Start constructing one of the three building types, as long as it finishes by time n.

If a building type has build_time and rate:
- It starts at time t and finishes at time finish = t + build_time.
- It earns money from finish to n.
- Profit from this single building = (n - finish) × rate (if finish ≤ n).

For each time t, we compute the best total profit from t to n by trying all valid choices (build Theatre, Pub, Commercial Park, or stop). We memoize the results to avoid recomputation. After computing the best profit from t = 0, we reconstruct the decisions to count how many T, P, and C were built.

Files in This Repository  
- MaxProfit.ipynb  
  Jupyter/Colab notebook that includes:
  - Implementation of the function solve_max_profit(n)
  - An interactive helper function to allow a user to type n and see the result
  - Code to generate multiple test cases and store them in a text file

- testcases.txt  
  A text file with 10 sample test cases. Each entry contains:
  - Input Time Unit (n)
  - Earnings
  - T, P, C counts

How to Run in Google Colab  

1. Open MaxProfit.ipynb in Google Colab.

2. Run the cell that defines the core function solve_max_profit(n).  
   This function returns:
   - best_profit (maximum total earnings)
   - counts (a dictionary with keys "T", "P", "C")

3. Run the cell that defines the interactive function:

   ```
   def run_interactive():
       n = int(input("Enter total time units (n): "))
       profit, counts = solve_max_profit(n)
       print("\n=== Result ===")
       print(f"Input Time Unit: {n}")
       print(f"Earnings: ${profit}")
       print("Solutions")
       print(f"T: {counts['T']} P: {counts['P']} C: {counts['C']}")
   ```

4. In a new cell, call:

   ```
   run_interactive()
   ```

5. When prompted, enter any value for n (for example: 7, 8, 13, 11, 20).  
   The notebook will print:
   - Input Time Unit  
   - Total Earnings  
   - T, P, C counts

Test Cases  

Inside the notebook there is a cell that:
- Defines a list of 10 different n values (including 7, 8, 13)
- Calls solve_max_profit(n) for each value
- Prints the results in a clear format
- Saves all test results into a file named testcases.txt

Format example inside testcases.txt:

Test Case 1  
Input: Time Unit: 7  
Earnings: $3000  
Solutions  
T: 1 P: 0 C: 0  
----------------------------------------  

You can download testcases.txt from Colab (Files panel) and add it to your GitHub repository along with the notebook.
