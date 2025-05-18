MIPS Pipeline Simulator
A comprehensive educational tool for understanding MIPS pipeline execution, data hazards, and performance optimization techniques.

Notice: This simulator is primarily for educational purposes. The code may produce incorrect output in some edge cases. Use with caution and please report any issues you encounter.

Overview
This MIPS Pipeline Simulator provides a visual and analytical framework for understanding how instructions flow through a five-stage MIPS pipeline (IF, RR, EX, MA, WR) and how different hazard prevention techniques affect performance. The simulator demonstrates key computer architecture concepts including data hazards, stalling, forwarding, and instruction reordering.
Features

Instruction Parsing: Handles common MIPS instructions including arithmetic operations, memory access, and control flow
Pipeline Visualization: Displays cycle-by-cycle execution of instructions through the pipeline
Data Hazard Detection: Identifies and highlights potential data hazards
Multiple Hazard Mitigation Techniques:

No Prevention (shows where incorrect execution would occur)
Stalling
Data Forwarding
Instruction Reordering
Combined Reordering with Forwarding


Performance Analysis: Calculates and compares metrics like CPI, IPC, and execution time
Configurable Clock Rate: Adjust clock frequency to see impact on execution time

Usage
Compile the program using any C++ compiler that supports C++11 or later:
bashg++ -std=c++11 pipeline_simulator.cpp -o pipeline_simulator
./pipeline_simulator
The interactive menu allows you to:

Visualize pipeline execution with various hazard prevention techniques
Adjust the processor clock rate
Compare performance metrics across all techniques

Sample Output
--- Pipeline with Forwarding and Stalls ---
Instruction              | C1     | C2     | C3     | C4     | C5     | C6     | C7     | C8     | C9     | C10    
--------------------------------------------------------------------------------------------------------------
lw r1,0(r2)              | IF     | RR     | EX     | MA     | WR     |        |        |        |        |        
lw r3,4(r2)              |        | IF     | RR     | EX     | MA     | WR     |        |        |        |        
add r4,r1,r3             |        |        | IF     | --     | RR     | EX     | MA     | WR     |        |        
sw r4,12(r2)             |        |        |        | IF     | --     | RR     | EX     | MA     | WR     |        
lw r5,8(r2)              |        |        |        |        | IF     | RR     | EX     | MA     | WR     |        
add r6,r1,r5             |        |        |        |        |        | IF     | RR     | EX     | MA     | WR     
--------------------------------------------------------------------------------------------------------------

Performance Metrics:
-------------------
CPI: 1.67
IPC: 0.60
Clock rate: 2.00 GHz
Execution time: 5.00 ns
Performance Comparison
The simulator can analyze the effectiveness of different optimization techniques:
=== Performance Comparison ===
Technique                    CPI       IPC       Exec Time (ns)
--------------------------------------------------------------------------------
No Prevention                0.83      1.20      2.50
Stalling Only                1.67      0.60      5.00
Forwarding with Stalling     1.17      0.86      3.50
Reordering Only              1.50      0.67      4.50
Reordering and Forwarding    1.00      1.00      3.00

Speedup compared to Stalling Only:
--------------------------------------------------------------------------------
No Prevention                2.00x (Not safe - produces incorrect results)
Forwarding with Stalling     1.43x
Reordering Only              1.11x
Reordering and Forwarding    1.67x

Best safe performing technique: Reordering and Forwarding
Educational Value
This simulator is ideal for:

Computer Architecture students learning about pipelining
Instructors demonstrating pipeline hazards and mitigation techniques
Self-study of processor optimization techniques
Understanding the performance tradeoffs of different hazard prevention methods

Limitations and Known Issues

This is a simplified model of a MIPS pipeline and may not accurately represent all real-world pipeline implementations
The simulator may produce incorrect results in complex instruction sequences or with certain combinations of hazards
The instruction reordering algorithm is a heuristic approach and may not produce optimal reordering in all cases
Branch instructions and control hazards are implemented in a simplified manner

Implementation Details
The simulator implements a classic 5-stage MIPS pipeline:

IF: Instruction Fetch
RR: Register Read
EX: Execute
MA: Memory Access
WR: Write Back

Data hazards detected include:

RAW (Read After Write)
WAR (Write After Read)
WAW (Write After Write)
Load-Use hazards

Future Enhancements
Possible improvements to consider:

Support for custom instruction sets via text file input
Branch prediction simulation
Cache performance modeling
Multi-issue pipeline simulation
Graphical user interface
Fix known edge cases producing incorrect output

Contributing
Contributions are welcome! Please feel free to submit a Pull Request, especially for fixing any incorrect outputs or edge cases.
