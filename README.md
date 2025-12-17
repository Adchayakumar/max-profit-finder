# 🏗️ Max Profit Scheduling Problem

---

## **Problem Overview**

*Mr. X owns a large strip of land* and can build **three types of buildings**. Each building takes a fixed amount of time to construct and then **earns money per unit time** once construction is complete.

### **Building Types & Earnings**

* **Theatre (T)**
  *Build Time:* `5` units
  *Earnings:* **1500 per time unit** (after completion)

* **Pub (P)**
  *Build Time:* `4` units
  *Earnings:* **1000 per time unit** (after completion)

* **Commercial Park (C)**
  *Build Time:* `10` units
  *Earnings:* **2000 per time unit** (after completion)

> **Constraint:** Only **one building** can be constructed at a time (no parallel construction).

For a given total time **`n`**, the objective is to determine:

* how many of each building to construct, and
* the order of construction,

so that the **total earnings at time `n` are maximized**.

---

## **Expected Output**

The algorithm returns:

* **Total Earnings**
* **Number of Theatres (T)**
* **Number of Pubs (P)**
* **Number of Commercial Parks (C)**

---

## **Example**

For **`n = 7`**, both of the following schedules produce the **same maximum earnings of 3000**:

* **One Theatre**
  Build: `0 – 5`
  Operational: `5 – 7` → `2 × 1500 = 3000`

* **One Pub**
  Build: `0 – 4`
  Operational: `4 – 7` → `3 × 1000 = 3000`

---

## **Approach Overview**

The solution uses **Dynamic Programming over time**.

### **Core Idea**

* Let the current time be **`t`**, where `0 ≤ t ≤ n`.
* From time `t`, you can either:

  * **Stop building**, or
  * **Start constructing** one of the three building types (only if it finishes by time `n`).

### **Profit Calculation**

For a building with:

* `build_time`
* `rate`

If started at time `t`:

* `finish = t + build_time`
* If `finish ≤ n`, then:

```
profit = (n - finish) × rate
```

### **Dynamic Programming Logic**

* For each time `t`, compute the **maximum profit achievable from `t` to `n`**.
* Try all valid options:

  * Build Theatre
  * Build Pub
  * Build Commercial Park
  * Stop building
* Store (memoize) results to avoid recomputation.
* Start from `t = 0` to get the final maximum profit.
* Reconstruct the chosen decisions to count **T, P, and C**.

---

## **Repository Structure**

### **MaxProfit.ipynb**

A Jupyter / Google Colab notebook containing:

* Implementation of `solve_max_profit(n)`
* An interactive helper function for user input
* Logic to generate multiple test cases and save them to a file

### **testcases.txt**

A text file with **10 sample test cases**, each including:

* Input time unit `n`
* Maximum earnings
* Counts of **T**, **P**, and **C`

---

## **Running the Project in Google Colab**

1. Open **`MaxProfit.ipynb`** in Google Colab.

2. Run the cell that defines:

```
solve_max_profit(n)
```

This function returns:

* `best_profit` → maximum total earnings
* `counts` → dictionary with keys **"T"**, **"P"**, **"C"**

3. Run the cell that defines the interactive function:

```
def run_interactive():
```
