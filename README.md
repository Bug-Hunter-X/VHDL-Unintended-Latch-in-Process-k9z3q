# VHDL Unintended Latch Bug

This repository demonstrates a common, yet subtle, bug in VHDL code: an unintended latch created by a missing default assignment in a process. 

The bug is in the file `bug.vhdl`. The solution is provided in `bugSolution.vhdl`.

## Bug Description
The VHDL code in `bug.vhdl` contains a process that updates the `data_out` signal based on the `data_in` signal. However, the `internal_data` signal, which acts as an intermediary, is not assigned a default value outside the `if rising_edge(clk)` condition.  This results in a latch being unintentionally created, causing the output `data_out` to retain its previous value if `data_in` does not change on a clock edge. This is a classic case where the synthesis tool will infer a latch, often causing unpredictable results.

## Solution
The solution, found in `bugSolution.vhdl`, includes a default assignment for `internal_data` outside the `if` statement, eliminating the unintentional latch. The process now clearly shows that `internal_data` will retain its previous value if the `clk` is not rising.  However, this is an explicit choice, not an accidental latch.
