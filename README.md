# Comparison of Two Shortest Path Algorithms

**Dijkstra vs A***

📘 **COMP 303 – Analysis of Algorithms**

🏫 **MEF University, Department of Computer Engineering**

👨‍🎓 **Student:** Kerem Ataç

👨‍🏫 **Instructor:** Prof. Dr. Adem Karahoca

---

## 📌 Project Overview

This project presents a **theoretical and experimental comparison** of two classical shortest path algorithms:

* **Dijkstra’s Algorithm**
* **A* (A-Star) Search Algorithm**

Both algorithms are analyzed in terms of:

* Algorithmic behavior
* Theoretical time complexity
* Practical (measured) running time
* Space complexity
* Strengths and weaknesses

The experiments are conducted on a **sparse graph** where each node is connected to neighbors satisfying:

```
|i − j| ≤ 3
```

with edge weights defined as:

```
w(i, j) = i + j
```

---

## 🧠 Part 1: Dijkstra’s Algorithm

### 🔹 Description

Dijkstra’s algorithm is a **greedy shortest-path algorithm** that computes the minimum distance from a source node to all other nodes in a graph with **non-negative edge weights**.

It uses a **priority queue (min-heap)** to repeatedly select the unvisited node with the smallest known distance and relax its edges.

---

### ⏱ Theoretical Time Complexity

Using a binary min-heap:

```
O((N + E) log N)
```

Since the graph is sparse (`E ≈ 6N`):

```
O(N log N)
```

---

### 🧪 Example Execution

**Parameters**

* Number of nodes: `N = 10`
* Source: `S = 1`
* Destination: `D = 8`

**Result**

* **Shortest Path:** `1 → 2 → 5 → 8`
* **Total Cost:** `23`

---

### 🧩 Implementation

* Implemented in **Python**
* Uses `heapq` for priority queue operations
* Stores distances and predecessors for path reconstruction

---

### 📊 Performance Measurement

To analyze real behavior:

* Counters were added to track:

  * Node extractions
  * Edge relaxations
* Experiments were run for:

```
N = [10, 50, 100, 200, 500, 1000, 2000]
```

---

### 📈 Results Interpretation

* Measured repetitions grew **linearly (O(N))**
* This is because each node has at most **6 neighbors**
* Theoretical `O(N log N)` curve grows faster due to heap operation costs
* Loop-counting does not capture `log N` cost directly

---

## 🧠 Part 2: A* Search Algorithm

### 🔹 Description

A* is an **informed search algorithm** that improves upon Dijkstra by using a heuristic:

```
f(n) = g(n) + h(n)
```

Where:

* `g(n)` = cost from start to node `n`
* `h(n)` = estimated cost from `n` to destination

**Heuristic used in this project:**

```
h(i, j) = |i − j|
```

---

### ⏱ Theoretical Time Complexity

Worst case (weak heuristic):

```
O((N + E) log N) ≈ O(N log N)
```

A* degenerates to Dijkstra when the heuristic provides little guidance.

---

### 🧪 Example Execution

**Parameters**

* `N = 8`, `S = 1`, `D = 8`

**Result**

* **Shortest Path:** `1 → 2 → 5 → 8`
* **Total Cost:** `23`

A* followed nearly the **same expansion order** as Dijkstra due to a weak heuristic.

---

### 🧩 Implementation

* Implemented in **Python**
* Priority queue ordered by `f(n)`
* Parent tracking used for path reconstruction

---

### 📊 Performance Measurement

Same methodology as Dijkstra:

* Node processing and edge checks counted
* Tested with increasing `N`

---

### 📈 Results Interpretation

* Actual repetitions grew **linearly (O(N))**
* The heuristic `|i − j|` is **too small** compared to edge weights `i + j`
* A* failed to significantly prune the search space

---

## ⚖️ Part 3: Algorithm Comparison

### ⏱ Time Complexity

| Algorithm | Theoretical | Measured |
| --------- | ----------- | -------- |
| Dijkstra  | O(N log N)  | O(N)     |
| A*        | O(N log N)  | O(N)     |

> Both algorithms behaved almost identically in this problem.

---

### 💾 Space Complexity

Both algorithms require:

```
O(N)
```

* Distance / cost arrays
* Parent pointers
* Priority queue storage

---

### ✅ Advantages & ❌ Disadvantages

#### Dijkstra

✅ Simple and reliable
✅ Guaranteed optimal solution
❌ Inefficient for single-destination queries

#### A*

✅ Faster with a good heuristic
✅ Directed search toward goal
❌ Performance depends heavily on heuristic quality

---

## 🏁 Conclusion

In this project:

* **Dijkstra and A*** performed almost identically
* The heuristic used in A* was **too weak**
* As a result, A* could not outperform Dijkstra
* Both algorithms showed **linear growth in measured operations**

🔧 **Future Improvement:**
Using a stronger admissible heuristic (e.g., scaling by minimum edge weight) would allow A* to significantly reduce node expansions.

---

## 📎 Additional Notes

* Graph visualizations were created for small `N` values
* Results were plotted using `matplotlib`
* All experiments were conducted under identical conditions
