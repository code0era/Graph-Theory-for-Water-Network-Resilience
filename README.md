
-----

# Graph Theory for Water Network Resilience

This project simulates a water distribution network using **Graph Theory** to analyze robustness and implement automated recovery strategies. Using Python's `networkx` library, it models the flow from a central pump to residential homes, simulates a critical infrastructure failure, and algorithmically reconnects affected nodes to ensure service continuity.

 
link : https://colab.research.google.com/drive/14581Zw8xamqoti-7W_XE89-RlfpGZna-

## 📌 Project Overview

Water distribution networks are critical infrastructure systems where connectivity is paramount. This simulation performs three main tasks:

1.  **Topology Generation:** Creates a directed, weighted graph representing a radial water network.
2.  **Failure Simulation:** Simulates the catastrophic failure of a distribution junction.
3.  **Resilience & Recovery:** Uses pathfinding algorithms (Dijkstra) to identify the most efficient alternative routes to reconnect cut-off homes.

## 📸 Simulation Stages

### 1\. The Normal Network Topology

**File:** 

<img width="1420" height="1443" alt="i0" src="https://github.com/user-attachments/assets/8c389c62-e75a-4ae2-a70f-b826bc9f6be0" />

  * **Root:** Central Pump (Orange).
  * **Distribution:** 3 Channels (Blue) feeding into 6 Junctions (Green).
  * **End-Users:** 30 Homes (Gray), with 5 homes assigned to each junction.
  * **Weights:** Edges are weighted to represent distance or pipe resistance.

### 2\. Failure Simulation

**File:** 
<img width="1420" height="1443" alt="i1" src="https://github.com/user-attachments/assets/1601e1d9-711d-4b43-b560-549d1d3ce882" />


  * **Scenario:** `Junction3` fails completely and is removed from the graph.
  * **Impact:** Homes 11, 12, 13, 14, and 15 (highlighted in Yellow) are severed from the main network and lose water supply.

### 3\. Automated Reconnection (Recovery)

**File:**

<img width="1420" height="1443" alt="i2" src="https://github.com/user-attachments/assets/bd6d7f8f-009d-4005-96fc-977df5b29c93" />


  * **Solution:** The algorithm scans for surviving neighboring junctions (`Junction1`, `Junction2`, `Junction4`, etc.).
  * **Optimization:** It calculates the lowest-cost path from the Pump to potential alternate junctions using **Dijkstra's Algorithm**.
  * **Result:** New connections (Blue edges) are established, restoring service to the affected homes with the most efficient available route.

## 🛠️ Technologies Used

  * **Python 3.x**
  * **NetworkX:** For graph creation, manipulation, and algorithmic analysis.
  * **Matplotlib:** For visualizing the network states.
  * **NumPy:** For coordinate calculations in the radial layout.

## ⚙️ How It Works

The simulation follows this logic flow found in the Jupyter Notebook:

1.  **Graph Construction:**

      * A `DiGraph` (Directed Graph) is initialized.
      * Nodes are added in layers: Pump $\to$ Channels $\to$ Junctions $\to$ Homes.
      * Weighted edges are created to define the cost of flow between nodes.

2.  **Visualization Layout:**

      * A custom `circular_positions` function places nodes in concentric rings (radial tree layout) to clearly visualize the hierarchy of the network.

3.  **Disaster Modeling:**

      * `G_failure = G.copy()` creates a simulation instance.
      * `G_failure.remove_node("Junction3")` mimics the infrastructure breakage.

4.  **Resilience Algorithm:**

      * The script iterates through the isolated homes.
      * It checks distances to all remaining active junctions.
      * It selects the junction with the minimum distance from the Pump:
        $$\text{Cost} = \min(\text{DijkstraPath}(\text{Pump} \to \text{CandidateJunction}))$$
      * A new edge is created to bridge the gap.

## 🚀 Getting Started

### Prerequisites

Ensure you have Python installed, then install the required packages:

```bash
pip install networkx matplotlib numpy
```

### Running the Simulation

1.  Download the notebook file: `Graph_Theory_for_Water_Network_Resilience_Against_Pipe_Failures.ipynb`.
2.  Open it in Jupyter Notebook, Google Colab, or VS Code.
3.  Run all cells sequentially.
4.  The output will generate the three visualizations shown above inline.

## 📈 Future Improvements

  * **Capacity Constraints:** Limit the number of homes a single junction can support to prevent overloading during reconnection.
  * **Flow Analysis:** Implement Max-Flow Min-Cut algorithms to analyze throughput.
  * **Dynamic Weights:** Adjust edge weights based on pipe pressure or elevation.

-----

**Author:**  code0era: Shubham Yadav
