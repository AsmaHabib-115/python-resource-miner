Python Resource Miner Simulator

A terminal-based simulation of a mining extraction operation. This project uses weighted probability and grid-based pattern matching to simulate the discovery of rare minerals.



📝 Project Overview

This application demonstrates core programming concepts by simulating a multi-layer mining scan. Users manage an Energy Balance to scan different Grid Layers. If a scan identifies matching resources across a horizontal layer, the operation successfully extracts a "yield" based on the rarity of the resource found.



✨ Technical Features

Weighted Random Distribution: Implemented a resource frequency system where common materials (Stone) appear more often than rare ones (Diamonds).



Multi-Layer Grid Logic: Users can choose to scan 1, 2, or 3 layers simultaneously, increasing both the cost and the potential yield.



State Management: Real-time tracking of energy balances and extraction costs.



Robust Input Validation: Prevents program crashes by handling invalid user inputs for energy amounts and layer selections.



Modular Architecture: Cleanly organized into specific functions for grid generation, pattern checking, and UI display.



🛠️ Skills Demonstrated

Data Structures: Using Dictionaries for resource mapping and nested Lists for 2D grid representation.



Algorithms: Pattern matching logic to detect sequences within a matrix.



Control Flow: Sophisticated use of while loops, for-else blocks, and conditional branching.



🚀 How to Run

Ensure you have Python 3.x installed.



Download the main.py file.



Open your terminal and run:



python main.py



📸 Simulation Preview



Current Energy Balance: 100

Press Enter to begin extraction (q to quit).

Energy to spend per layer? 10

Scanning 3 layers. Total energy cost: 30



C | C | C

D | B | A

A | A | A



Extraction yielded: 55 resource units.

Success found on layers: 1 3

Current Energy Balance: 125
