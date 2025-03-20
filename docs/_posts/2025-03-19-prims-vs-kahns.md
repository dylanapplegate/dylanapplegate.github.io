---
layout: post
title: "Prim's Algorithm vs. Kahn's Algorithm: A Comparison with JavaScript"
date: 2025-03-19
author: "Dylan Applegate"
tags: algorithms, graphs, computer science, JavaScript
---

## **Introduction**

Graph algorithms play a vital role in solving complex computational problems. Two well-known algorithms, **Prim's Algorithm** and **Kahn's Algorithm**, serve very different purposes in graph theory. Let's compare them with **JavaScript implementations**.

---

## **Prim’s Algorithm (Minimum Spanning Tree)**

Prim’s Algorithm is a **greedy algorithm** that finds the **Minimum Spanning Tree (MST)** for a weighted, connected graph. The MST is a subset of edges that connects all vertices with the **minimum possible total edge weight**.

### **How It Works**

1. Start from an arbitrary node.
2. Select the smallest edge that connects the current tree to a new node.
3. Repeat until all nodes are connected.

### **JavaScript Implementation**

```js
class MinHeap {
  constructor() {
    this.heap = [];
  }

  insert(node) {
    this.heap.push(node);
    this.heap.sort((a, b) => a[0] - b[0]); // Sort by weight
  }

  extractMin() {
    return this.heap.shift(); // Remove the smallest element
  }

  isEmpty() {
    return this.heap.length === 0;
  }
}

function prim(graph, start) {
  const visited = new Set();
  const minHeap = new MinHeap();
  let mstCost = 0;

  minHeap.insert([0, start]); // [weight, node]

  while (!minHeap.isEmpty()) {
    const [weight, node] = minHeap.extractMin();

    if (visited.has(node)) continue;
    visited.add(node);
    mstCost += weight;

    for (const [neighbor, cost] of graph[node]) {
      if (!visited.has(neighbor)) {
        minHeap.insert([cost, neighbor]);
      }
    }
  }

  return mstCost;
}

// Example graph as adjacency list
const graph = {
  A: [
    ["B", 1],
    ["C", 3],
  ],
  B: [
    ["A", 1],
    ["C", 1],
    ["D", 6],
  ],
  C: [
    ["A", 3],
    ["B", 1],
    ["D", 4],
  ],
  D: [
    ["B", 6],
    ["C", 4],
  ],
};

console.log(prim(graph, "A")); // Output: Minimum spanning tree cost
```

### **Time Complexity**

- **O(E log V)** using a priority queue.
- **O(V²)** for an adjacency matrix (without a priority queue).

### **Use Cases**

- **Network design** (e.g., electrical grids, road networks).
- **Clustering in machine learning**.
- **Approximate solutions** for **Traveling Salesman Problem (TSP)**.

---

## **Kahn’s Algorithm (Topological Sorting)**

Kahn’s Algorithm is used to **find a topological order** in a **Directed Acyclic Graph (DAG)**. This is crucial in **task scheduling** and **dependency resolution**.

### **How It Works**

1. Identify nodes with **zero in-degree** (no incoming edges).
2. Remove these nodes and update in-degrees of their neighbors.
3. Repeat until all nodes are processed (or detect a cycle if nodes remain).

### **JavaScript Implementation**

```js
function kahnTopologicalSort(graph) {
  const inDegree = {};
  const queue = [];
  const topOrder = [];

  // Initialize in-degree for each node
  for (const node in graph) {
    inDegree[node] = 0;
  }
  for (const node in graph) {
    for (const neighbor of graph[node]) {
      inDegree[neighbor] = (inDegree[neighbor] || 0) + 1;
    }
  }

  // Enqueue nodes with zero in-degree
  for (const node in inDegree) {
    if (inDegree[node] === 0) {
      queue.push(node);
    }
  }

  while (queue.length > 0) {
    const node = queue.shift();
    topOrder.push(node);

    for (const neighbor of graph[node]) {
      inDegree[neighbor]--;
      if (inDegree[neighbor] === 0) {
        queue.push(neighbor);
      }
    }
  }

  // If graph has a cycle, return an error
  if (topOrder.length !== Object.keys(graph).length) {
    throw new Error("Graph has a cycle, topological sorting is not possible.");
  }

  return topOrder;
}

// Example DAG
const dag = {
  A: ["B", "C"],
  B: ["D"],
  C: ["D"],
  D: [],
};

console.log(kahnTopologicalSort(dag)); // Output: Topological order
```

### **Time Complexity**

- **O(V + E)** using an adjacency list.

### **Use Cases**

- **Task scheduling** (e.g., **compilation of source code dependencies**).
- **Resolving package dependencies** in **package managers (npm, pip, etc.)**.
- **Course scheduling** (e.g., determining prerequisite sequences).

---

## **Key Differences**

| Feature             | Prim's Algorithm                      | Kahn's Algorithm                 |
| ------------------- | ------------------------------------- | -------------------------------- |
| **Purpose**         | Finds **Minimum Spanning Tree (MST)** | Finds **Topological Order**      |
| **Graph Type**      | **Weighted, Undirected**              | **Directed Acyclic Graph (DAG)** |
| **Approach**        | Greedy                                | BFS-based                        |
| **Time Complexity** | **O(E log V)** (Heap)                 | **O(V + E)**                     |
| **Common Use Case** | Network optimization                  | Task scheduling                  |

---

## **Conclusion**

Prim's and Kahn’s algorithms tackle different **graph problems**, but both are essential tools in a software engineer’s toolkit. Whether optimizing a network or scheduling dependencies, knowing when to apply each can greatly improve efficiency.

🚀 **What’s your favorite graph algorithm? Drop a comment!**
